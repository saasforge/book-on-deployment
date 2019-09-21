# Chapter II. Heroku

### Everything starts from account

Signing up to Heroku is pretty straightforward process, everything is as usually as with any other service. 

You will probably have to verify your account. For example, if you want to host more than 5 apps, or use a custom domain. It's simple too and just requires you providing a credit card information. To do that, go to your account settings:
![Heroku account settings](https://github.com/saasforge/book-on-deployment/blob/master/Illustrations/Heroku_account.png)

Then click the **Billing** tab and click the **Add credit card** button.

### Concept of dynos

Heroku introduced "dynos" what are described as "lightweight Linux containers". Full information you can find in [Heroku docs](https://devcenter.heroku.com/articles/dynos). We, especially those who are from the Windows world, can consider a dyno as a type of applicatin (maybe it's wrong, but I can't find closer analogy). Dyno can be [free, hobby, standard, or performance](https://devcenter.heroku.com/articles/dyno-types). You always start from the free dyno. This type of dyno doesn't allow to link a custom domain and has other restrictions.

### Application

Let's create an application. We will use the web interface. Go to your dashboard and click the **New** button, then select **Create new app**:
[Heroku create new app](https://github.com/saasforge/book-on-deployment/blob/master/Illustrations/Heroku_create_app.png)

Enter the app's name and select a region.

We found the integration with Github very convenient and higly recommend to set it up. So, if you have your code in the Github, even in a private repository, you can connect it to the heroku app and the code will deployed automatically or when you are ready. To set up the integration, just open your app's page, click the **Deploy** tab, go to the **Deployment method** section, click **Connect to GitHub** and follow the instructions.

