You'll need at least 2 things:

- a Slackbot created in your Slack workspace that will let Number6 read all the messages from the public channels on a given date and also let it post back its analysis to a given channel in that workspace
- an AWS account to deploy and run all the resources for Number6
- you may need a bit more depending on how you're deploying it, but those 2 are essential

## Create a Slackbot/Slack App

- In your Slack workspace create a Number6 Slack app, Slack makes this pretty easy and has good documentation for this https://api.slack.com/apps
- You can name your app anything you want but "Number6" is a reasonable choice, there's an icon file [`No6Icon.jpg`](https://github.com/Number6App/number6app.github.io/blob/master/assets/images/No6Icon.jpg) in the project repo you can use to really run with the theme
- After creating an app with a name in your workspace the only 'features and functionality' you'll need is to assign permissions
- You'll need to assign it the following oauth Bot Token scopes:
  - channels:history
  - channels:read
  - channels:join
  - chat:write
- click 'install your app to your workspace'
- you won't need to distribute it, set up redirect URLs or any of the other things you can do with Slack apps
- you will need the OAuth token Slack creates for your app, though, you can find this in `OAuth and Permissions` in the `Features` side menu of your app's page in Slack

