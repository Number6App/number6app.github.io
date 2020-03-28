[< back](./index.md)

- create a Number6 Slack app with access to your workspace, Slack makes this pretty easy and has good documentation for this https://api.slack.com/apps 
- You can name your app anything you want but "Number6" is a reasonable choice, there's an icon file `No6Icon.jpg` in the project root you can use to really run with the theme
- After creating an app with a name in your workspace the only 'features and functionality' you'll need is to assign permissions
- You'll need to assign it the following oauth Bot Token scopes:
  - channels:history
  - channels:read
  - channels:join
  - chat:write
- click 'install your app to your workspace'
- you won't need to distribute it, set up redirect URLs or any of the other things you can do with Slack apps

[< back](./index.md)
