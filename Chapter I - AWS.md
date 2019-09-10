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
