# Chapter I. Deployment to AWS Elastic Beanstalk
## Basics of deployment
### Everything starts from account
Before you start the deployment to AWS, you have to create an account. It's simple. 
All you need to enter is your email and password. Then they will ask you to provide more details: type of your account (personal or professional). They will also ask for credit card information (even if you are not going to pay). 

![AWS Account](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/aws-create-account.png)

*Does anybody know what's the difference between two these types of account? I see the company name you need to enter for the Professional account.*

![Select account](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/aws-select-account.png)

At the very end, they will require to verify your account by phone - using a voice message or SMS.

After all these steps are done you will able to choose from the plans: Basic (free), Developer, or Business. Don't worry about support - even on a free account, there are ways to use their support (for example, to leave feedback, or send an inquiry).

:warning: **Somewhere in the process AWS will ask you about the preferred region. You need to select it and then use it. I had a situation when AWS selected a region for me and I wasn't aware of it and was wondering why I couldn't find apps I already created (because they were not visible for the current region). Your current region is always on top:**

![The current account](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_Current_Region.png)

After you're finally done with creating an account, log in to the [AWS Console](https://aws.amazon.com/console).

Now you need to go to Elastic Beanstalk. The first time it can be tricky. Just use the search box at the top of your console:

![Elastic Beanstalk](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/elastic-beanstalk-find.png)

### Concepts: applications and environments

When you open the Beanstalk Console, you will see the invitation to get started. Don't rush! First check which region you have there. Change it, then proceed. As for we are describing the process of deployment from your terminal, let's proceed this way.

Click the Create New Application link on the right top, then enter its name.

:point_right: **Note. An application in terms of AWS is not what you use to think about. We found the terminology pretty confusing. What AWS says about the application: *"An Elastic Beanstalk application is a logical collection of Elastic Beanstalk components, including environments, versions, and environment configurations. In Elastic Beanstalk an application is conceptually similar to a folder."* And it's not a folder where you have your application's files as you may think, it's rather a folder where you have you multiple folders containing applications. So, probably the best way is to think about "application" is to consider it as a set of applications.**

Okay, to confuse you even more, AWS called the apps "environments". We are going to create one soon, but first, let's go back to your app's terminal.

We suppose you already have your app ready for deployment. We are currently working with Python/Flask apps, so let's assume you already have one.

### Elastic Beanstalk CLI
#### Init (create or select an application)
Install EB CLI from [this AWS Page](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install-advanced.html). Just pick your OS, download pip (if not installed yet), and use the instruction from there to install EB CLI.

After you've done, to check if it's installed, call in your terminal:

![EB CLI check](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/EB_CLI_check.png)

:point_right: **BTW, it should not be a command prompt. Many IDEs like VS Code or PyCharm have terminals.**

:point_right: **Wy don't we use the AWS interface to create an environment? Because I didn't find a way to create an environment without uploading the code right away. I found much more logical to create an environment, then upload/deploy the code - and it can be done easier via EB CLI.**

So, now in any terminal move to your working folder. For Flask app it's a root folder where you have your start application file.

**Start application file in Python should be called application.py**

In this folder in the terminal print the following command:

```
eb init
```
This command will ask you several questions and create eb config file when done. If you don't want to create SSH say **no** to the corresponding question and select a **classic** load balancer when asked.

First you have to choose a region. It should be the same region you created an application before:

![EB CLI select a region](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/EB_region.png)

Then CLI will ask for your credentials. You need to open your account and retrieve your access id and a secret key:
![AWS account](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_account.png)

It may then ask you where to proceed, click **Continue to Security Credentials**:

![Select credentials](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_console_question.png)

If it's not shown just click on the **Access Keys** tab and then click the **Create New Access Key**:

![Access Keys](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_console_create_access_key.png)

It will generate 2 keys for you, you can copy them or download:

![Get your keys](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_console_get_access_key.png)

Then you can enter keys in your terminal.

The next question will be an application to use (or to create). Select that already exists (or you may create a new one). 

Then it will ask a platform and if you want to set up SSH for your instances (say "no").

During the init process EB creates a folder called **.elasticbeanstalk** in the root folder with **config.yml** file inside:

![EB Config file, almost empty](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/EB_config.png)

#### Create a new environment

Now we should create a new environment (aka application in terms of AWS). Type in your terminal:

```
eb create
```
or
```
eb create <environment_name>
```
:warning: **Note. It's better to start with eb create command - it will ask you env name later, as well as a prefix that can be changed. If run _eb create env-name_ it will add a stupid prefix automatically.**

Creating a new environment may take some time (up to several minutes). After it's done, you can see your new application in the AWS Console:

![New application on AWS console](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/EB_env.png)

Now you need to configure your application. The minimal thing you probably would do is to set up the environment variables. 

Click on the green rectangle of the environment and you will see the Overview page:

![Environment overview](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/EB_env_overview.png)

Click on the **Config** link on the left, and then, when the console will be loaded, click the **Modify** link:

![Environment console](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/EB_env_vars.png)

Scroll the page down and enter your environment variables:

![Environment variables](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/EB_env_vars_config.png)

Don't forget to click the **Apply** button else data will not be saved.

#### If your application is Flask-based
The process is described [here](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create-deploy-python-flask.html).

It may be a little bit tricky to make it work but you just need to know several conventions:

1. The main application name should be application.py (not app.py or flask.py or main.py or anything else).
2. Do NOT add *FLASK_APP=application* to AWS environment variables.

#### Deployment to AWS

To deploy your application from the terminal,  just type:
```
eb init
```
During this process, the EB CLI will grab your code, pack it into the archive, save to the AWS S3 and deploy to the server.

:warning: **WARNING! If the local folder contains .git folder it should point to the right source. (In my case, I accidentally copied it from other folder and AWS gets the source code from there). So, you use a proper git folder or you shouldn't have .git folder at all.**

:point_right: **If your app uses NPM to install and bundle code, you would probably run the production configuration before deploying your prod version.**

### Viewing logs
Sometimes not everything is going right. If you see "Internal Server Error" in the browser instead of your nice looking app, you would like to look at the logs.

To view logs, go to your app's overview page, click Logs on the left and then request the last 100 rows (or the whole log):
![View logs](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_logs.png)

The link will be generated and you will see it in the table below. 

:warning: **If you click the link the log will be open in the browser what can make worse its performance. Instead, you would just download .txt file to your local computer.**

### Accessing app's versions archives
To look and / or download all app's versions that ever been deployed go to AWS S3 simple storage. To find the link, click the **Services** link on the left of your console and then click **S3**:

![S3 Access](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_S3.png)

Then you will see the content of your S3 account. Click the bucket with a name something like "elasticbeanstalk-region-4375839236", then a folder with your application's name, it contains all archived app's versions.

## Custom domain and SSL/HTTPS

### Register your domain and redirect

You can register your domain using any domain provider. We prefer use Namecheap because they have great prices and, what is more important, great service. So, your first step is to register your unique domain name with a provider on your choice.

Then we need to redirect from our web app hosted on AWS to our custom domain. It's very easy.

1. Open your Elastic Beanstalk console, navigate to the application and then to the environment page. You will find the link to your app on the top:

![You app url](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_app_url.png)

2. Open your domain provider's console, find the page to manage your domain, and add the following record:
- Type of records: CNAME
- Host: www
- Value: copied url to your application (:warning: Remove **https://** from the url when creating the record)

![Namecheap new record](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/domain_provider_new_record.png)


### SSL certificate on AWS

#### Obtain certificate
The first step is to obtain a free SSL certificate issued by AWS. Open your AWS console, and there, using search find **Certificate manager**. If you don't have any certificates yet when you click it you will see the following screen. Select **Provision certificates**.

![AWS Certificate Manager](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_certificate_manager.png)

Then you will be asked which certificate you want - public or private. Select **Request a public certificate** and then click the **Request a certificate** button.

If you think you may have a subdomain, it's a good idea to add a wild card subdomains. So, you need to provide 2 domains:
- yourdomain.com (for a bare domain)
- \*.yourdomain.com (a wildcard for subdomain)

![AWS Certificate Manager domains](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_certificate_manager_domains.png)

Use the **Add another name to this certificate** to add a new record. When done, click the **Next** button.

#### Validate
You will be asked the method of validation your request. Select the **Email validation** and click the **Review** button, then, after you make sure everything is fine, click the **Confirm and request** button.

You will see something like that:

![AWS Certificate manager validation](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_domain_certificate_validation.png)

Expand records to see details, also you can download the spreadsheet having the same data. Now you need to create new records in your domain provider console. Go there, and create separate records for each of your domains you want to get a certificate for.

- Type of record: CNAME
- Host: The first part of **Name** column from AWS table. (For example, if Name is \_f75fd16ce62eaaf911587618b1d8aba6.asdfas.com. you just copy \_f75fd16ce62eaaf911587618b1d8aba6)
- Value: Value from the AWS table
- TTL: automatic

Save your records. Then come back to the AWS console and click the **Continue** button. You will see your records pending validation:

![AWS Certificate Manager pending validation](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_certificate_manager_pending.png)

Then click the **Refresh** button to check if they validated your requests and issued the certificates. Usually, it takes from several minutes to several hours. If after several hours they are still pending validation, check if you entered CNAME records properly, saved data and all.

![AWS Certificate Manager refresh button](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_certificate_manager_refresh.png)

When the certificate is issued you will the "Issued" status.

#### Finish setting SSL

After the certificates are ready we need to set up the load balancer. Go to your application console, click the environment page, then click the **Configuration** link on the left, find the **Load balancer** square and click the **Modify** button.

On the **Modify load balancer page** (it should be classic one as described in **Init (create or select an application)**) page click the **Add listener** button and enter the following values:

![AWS Load balancer listener](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_load_balancer_listener.png)

In the **SSL certificate** dropdown select your certificate, if it's empty try to refresh (the button on the right). Save the new listener. Then scroll down the load balancer page and click the **Apply** button.


#### Redirecting from HTTP to HTTPS

Now we want our visitors to be redirected to https:// protocol automatically. It's pretty simple. You need to open your project's folder, create a **.ebextensions** folder and inside create one file called **01.config**. Add the following code to this file:

```
files:
    "/etc/httpd/conf.d/ssl_rewrite.conf":
        mode: "000644"
        owner: root
        group: root
        content: |
            RewriteEngine On
            <If "-n '%{HTTP:X-Forwarded-Proto}' && %{HTTP:X-Forwarded-Proto} != 'https'">
            RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R,L]
            </If>
```
This code will provide a smooth redirection.

That's it!
