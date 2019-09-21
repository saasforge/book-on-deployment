# Chapter II. Heroku

### Everything starts from account

Signing up to Heroku is pretty straightforward process, everything is as usually as with any other service. 

You will probably have to verify your account. For example, if you want to host more than 5 apps, or use a custom domain. It's simple too and just requires you providing a credit card information. To do that, go to your account settings:
![Heroku account settings](https://github.com/saasforge/book-on-deployment/blob/master/Illustrations/Heroku_account.png)

Then click the **Billing** tab and click the **Add credit card** button.

### Concept of dynos

Heroku introduced "dynos" what are described as "lightweight Linux containers". Full information you can find in [Heroku docs](https://devcenter.heroku.com/articles/dynos). We, especially those who are from the Windows world, can consider a dyno as a type of applicatin (maybe it's wrong, but I can't find closer analogy). Dyno can be [free, hobby, standard, or performance](https://devcenter.heroku.com/articles/dyno-types). You always start from the free dyno. This type of dyno doesn't allow to link a custom domain and has other restrictions.

### Create an appplication and deploy

Let's create an application. We will use the web interface. Go to your dashboard and click the **New** button, then select **Create new app**:
![Heroku create new app](https://github.com/saasforge/book-on-deployment/blob/master/Illustrations/Heroku_create_app.png)

Enter the app's name and select a region.

We found the integration with Github very convenient and higly recommend to set it up. So, if you have your code in the Github, even in a private repository, you can connect it to the heroku app and the code will deployed automatically or when you are ready. To set up the integration, just open your app's page, click the **Deploy** tab, go to the **Deployment method** section, click **Connect to GitHub** and follow the instructions.

If you don't want to integrate your code with any remote remote, you will deploy manually using from your terminal. First, you need to download and install [Heroku CLI](https://devcenter.heroku.com/articles/heroku-command-line).

Then enter in your terminal:
```
heroku login
```
Enter your credentials. The next step is to create a remote repository because it's the only way to deploy your app. It means that you need to initialize your local folder. Do it as usually:

```
cd yourfolder
git init
heroku git:remote -a thenameofyourapp
```

Then commit your changes as you usually do:
```
git add .
git commit -am "First commit"
git push heroku master
```

When pushing to the Heroku repo, it may ask for credentials. And it's not the same as you already entered. What you should enter:
- username - leave blank
- password - heroku auth token (that can be obtained through *heroku auth:token* command)

You can find all details on it in the (Heroku docs)[https://devcenter.heroku.com/articles/git].

So, the pushing to the Heroku git actually runs deployment. But, before you deploy your code you need to do something more.

### Preparing app for a deployment (Flask-based apps)

#### Gunicorn
Before pushing application to the Heroku, create an empty file in the app's root folder and call it Procfile. Open it and add the following string into:

```
web: gunicorn module_name:variable_name
```

Find full description of using gunicorn utility [in the official docs](http://docs.gunicorn.org/en/stable/run.html).

So, for example you have app.py in the root folder which contains the application variable created with using factory approach:

```
application = create_app()
```

In this situation your command should look:

```
web: gunicorn app:application
```

Also you need provide the installation this package on Heroku. You can just add the corresponding line into your *requirements.txt* file, or just run these 2 commands:

```
pip install gunicorn
pip freeze > requirements.txt
```

#### Multiple buidpacks

If your app is written in Python but it uses webpack to install packages you need to run Node.js *before* running your Python app to prepare all NPM packages compiled and bundled. Heroku is smart enough to figure out that your app is in Python but it will not be able to guess to run *npm* command before. So you need to do 2 things:

1. Tell webpack to run the corresponding configuration (we assume you already have separate webpack config files for development and production). To do so, add the following strings into your *package.json* file:

```
"scripts": {
    "dev": "webpack --config webpack.dev.js",
    "prod": "webpack --config webpack.prod.js",
    "heroku-prebuild": "npm install",
    "heroku-postbuild": "webpack --config webpack.$env.js"
},
```

So, basically it just means you install all packages and then ask webpack to run the corresponding configuration.

:warning: Don't forget to provide a proper environment variable *env*, in our case it's *dev* or *prod*.

2. Tell Heroku that you want to run Node.js first, then Python. It can be done using [buildpacks](https://elements.heroku.com/buildpacks). To do so, open your app's page, click the **Settings** tab, scroll a little bit and find the **Buildpacks** section. Add buildpack, Node.js and Python:

![Heroku buildpacks](https://github.com/saasforge/book-on-deployment/blob/master/Illustrations/Heroku_buildpack.png)

### Custom domain and SSL

Start from registering your domain at some domain provider. We use Namecheap because they have a really great services (and great prices). 

:warning: Before you add a custom domain in Heroku, you should verify your account, see the **Everything starts from account** section. After you're done, open your application's page, click the **Settings** tab, scroll down to the **Domains and certificates** section. Click the **Add domain** button. Enter your registered domain, then open your domain provider's console and create the corresponding CNAME. Please refer the [Heroku docs](https://devcenter.heroku.com/articles/custom-domains#configuring-dns-for-subdomains) to see what you should provide in CNAME, but basically, it's your app heroku URL like *yourfullappurl.herokudns.com.*

:warning: The URL you should enter in your domain provider is not your heroku app URL like *yourapp.herokuapp.com*.
