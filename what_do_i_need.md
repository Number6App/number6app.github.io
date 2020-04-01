[back](./)

# What do I need to get it running?

You'll need at least:

- a Slack App created in your Slack workspace that will let Number6 read messages from public channels and also let it post back its analysis to a given channel in that workspace
- the id of a Slack channel for Number6 to post to. This is Slack's internal id of the channel, not its name, see below for how to get it
- an AWS account to deploy and run all the resources for Number6
- Some AWS knowledge is assumed in these instructions
- you may need a bit more depending on how you're deploying it

## Create a Slackbot/Slack App

1. In your Slack workspace create a Number6 Slack app, Slack makes this pretty easy and has good documentation for this [https://api.slack.com/apps](https://api.slack.com/apps)

2. You can name your app anything you want but "Number6" is a reasonable choice, [there's an icon file `No6Icon.jpg`](https://github.com/Number6App/number6app.github.io/blob/master/assets/images/No6Icon.jpg) in the project repo you can use to really run with the theme

3. After creating an app with a name in your workspace the only 'features and functionality' you'll need is to assign permissions

4. You'll need to assign it the following oauth Bot Token scopes:

- channels:history
- channels:read
- channels:join
- chat:write

5. click 'install your app to your workspace'

6. you won't need to distribute it, set up redirect URLs or any of the other things you can do with Slack apps

7. you will need to use the oauth token that Slack creates for your app though, you can find this in `OAuth and Permissions` in the `Features` side menu of your app's page in Slack

## Number6 Channel Id

Number6 needs a Slack channel in your workspace to post its results back to each day, currently you need to supply the id of that channel: 

- It's recommended to create a new one just for this purpose 
- The simplest way to find the channel id is to log into your workspace through a browser then go to the channel
- the URL will look something like `https://app.slack.com/client/T03QK0277/C03QK207F` the final path parameter is the channel id (C03QK207F in this case)

[back](./)

