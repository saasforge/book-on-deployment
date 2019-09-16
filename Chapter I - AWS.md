# Chapter I. Deployment to AWS Elastic Beanstalk
## Basics of deployment
### Everything starts from account
Before you start the deployment to AWS, you have to create an account. It's simple. 
All you need to enter is your email and password. Then they will ask you to provide more details: type of your account (personal or professional). They will also ask for a credit card information (even if you are not going to pay). 

![AWS Account](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/aws-create-account.png)

*Does anybody know what's the difference between two these types of account? I see the company name you need to enter for the Professional account.*

![Select account](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/aws-select-account.png)

At the very end they will require to verify your account by phone - using a voice message or SMS.

After all these steps done you will able to chose from the plans: Basic (free), Developer, or Business. Don't worry about support - even on a free account there are ways to use their support (for example, to leave a feedback, or send an inquiry).

:warning: **Somewhere in the process AWS will ask you about preferred region. You need to select it and then use it. I had a situation when AWS selected a region for me and I wasn't aware about it and was wondering why I couldn't find apps I already created (because they were not visible for the current region). Your current region is always on top:**

![The current account](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_Current_Region.png)

After you're finally done with creating an account, log in to the [AWS Console](https://aws.amazon.com/console).

Now you need to go to Elastic Beanstalk. The first time it can be tricky. Just use the search box at the top of your console:

![Elastic Beanstalk](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/elastic-beanstalk-find.png)

### Concepts: applications and environments

When you open the Beanstalk Console, you will see the invitation to get started. Don't rush! First check which region you have there. Change it, then proceed. As for we are describing the process of deployment from your terminal, let's proceed this way.

Click the Create New Application link on the right top, then enter its name.

:point_right: **Note. An application in terms of AWS is not what you use to think about. We found the terminology pretty confusing. What AWS says about application: "An Elastic Beanstalk application is a logical collection of Elastic Beanstalk components, including environments, versions, and environment configurations. In Elastic Beanstalk an application is conceptually similar to a folder." And it's not a folder where you have your applications's files as you may think, it's rather a folder where you have you multiple folders or apps containing applications. So, probably the best way is to think about "application" is to consider it as a set of applications.**

Okay, to confuse you even more, AWS called the apps "environments". We are going to create one soon, but first let's go back to your app's terminal.

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
This command will ask you several questions and create eb config file when done. If you don't want to create SSH say **no** to the corresponding question, and select a **classic** load balancer when asked.

First you have to choose a region. It should be the same region you created an application before:

![EB CLI select a region](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/EB_region.png)

Then CLI will ask for your credentials. You need to open your account and retrieve your access id and a secret key:
![AWS account](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_account.png)

It may then ask you where to proceed, click **Continue to Security Credentials**:

![Select credentials](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_console_question.png)

If it's not shown just click on Access Keys tab and then click the **Create New Access Key**:

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
:warning: **Note. It's better to start with eb create command - it will ask you env name later, as well as prefix that can be changed. If run _eb create env-name_ it will add a stupid prefix automatically.**

:warning: **WARNING! If the local folder contains .git folder it should point to the right source. (In my case, I accidentally copied it from other folder and AWS gets source from there). So, you use a proper git folder or you shouldn't have .git folder at all.**

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



