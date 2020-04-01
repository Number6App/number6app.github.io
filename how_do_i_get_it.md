[back](./)

# How do I get it for my Slack?

In order of increasing complicatedness you can:

1. Deploy it from the AWS Serverless Application Repository (see below)

2. Deploy [your own stand-alone version](./stand_alone.md)

   - you can deploy your own stand-alone version to AWS directly from a local copy of Number6. You might want to do this to be sure that the code being deployed is what you expect, you've made changes to Number6 or you just want to experiment.

3. deploy a [CD pipeline to AWS that is triggered by a GitHub web hook](./pipeline_deployment.md). 

   - This requires 2 AWS accounts

   - a "test" account to build the application on each push and a "production" account to deploy the new version to

   - deployment to the prod account is a manual accept/reject step

   - the 2 accounts can have different Slack channels to post their reports back to

     

## AWS Serverless Application Repository

This is simply a case of going to the SAR in the console (make sure you're using the intended account and in the intended region) and [searching for Number6](https://eu-west-1.console.aws.amazon.com/lambda/home?region=eu-west-1#/create/app?applicationId=arn:aws:serverlessrepo:eu-west-1:805721357281:applications/Number6) (you'll need to check the `Show apps that create custom IAM roles or resource policies` option for Number6 to show up) and choosing to deploy it. 

You will need to [manually store your Slack app's oauth token in AWS Secrets Manager](./slack_oauth_secret.md) first.

### Deploy from SAR:

You'll need to supply the following parameters in the console before it will let you deploy:

- **Application Name** - this will default to Number6 if you leave it but you can call it anything you like
- **SlackChannel** - this is the Slack id of the channel that Number6 will post back to ([what do I need](./what_do_i_need.md))
- **BlacklistedChannels** - this is a single CSV string of channel names (not ids e.g. `meta,announcements,trumptweets`) that shouldn't be analysed by Number6
  - This is useful if you have channels with just bot traffic or something similar where it doesn't make sense to perform any sentiment analysis. 
  - You'll probably want to include Number6's output channel name in this.
- **SlackTokenSecretName** - the is the name used to store the Slack oauth token in AWS Secrets Manager that you created in step 1
- **EnvType** - this must be either `prod` or `test`, creating a `prod` stack will run Number6 at 1am every day analysing the previous day's messages. If you create a `test` stack then it will only ever [run when manually triggered](./how_do_i_test_it.md) and analyse the messages from whatever date you give it

[back](./)