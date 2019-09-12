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

*Somewhere in the process AWS will ask you about preferred region. You need to select it and then use it. I had a situation when AWS selected a region for me and I wasn't aware about it and was wondering why I couldn't find apps I already created (because they were not visible for the current region). Your current region is always on top:*

![The current account](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/AWS_Current_Region.png)

After you're finally done with creating an account, log in to the [AWS Console](https://aws.amazon.com/console).

Now you need to go to Elastic Beanstalk. The first time it can be tricky. Just use the search box at the top of your console:

![Elastic Beanstalk](https://github.com/saasforge/deployment-to-aws-and-heroku-book/blob/master/Illustrations/elastic-beanstalk-find.png)

When you open the Beanstalk Console, you will see the invitation to get started. Don't rush! First check which region you have there. Change it, then proceed. As for we are describing the process of deployment from your terminal, let's proceed this way.

Click the Create New Application link on the right top, then enter its name.

*Note. An application in terms of AWS is not what you use to think about. We found the terminology pretty confusing. What AWS says about application: "An Elastic Beanstalk application is a logical collection of Elastic Beanstalk components, including environments, versions, and environment configurations. In Elastic Beanstalk an application is conceptually similar to a folder." And it's not a folder where you have your applications's files as you may think, it's rather a folder where you have you multiple folders or apps containing applications. So, probably the best way is to think about "application" is to consider it as a set of applications.*
