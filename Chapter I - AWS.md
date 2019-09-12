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

[EB CLI select a region](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/EB_region.png)

:warning: **WARNING! If the local folder contains .git folder it should point to the right source. (In my case, I accidentally copied it from other folder and AWS gets source from there). So, you use a proper git folder or you shouldn't have .git folder at all.**

Now, let's create an environment (an actual app). Execute:
```
eb create
```
or
```
eb create <environment_name>
```
:warning: **Note. It's better to start with eb create command - it will ask you env name later, as well as prefix that can be changed. If run _eb create env-name_ it will add a stupid prefix automatically.**


