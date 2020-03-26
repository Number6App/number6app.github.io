## Number6 Deployment Parameters


- SlackChannel - this is Slack's id for the channel that Number6 will post its results to. 
  - The simplest way to find this is to log into your workspace through a browser, create a new channel (recommended rather than posting to an existing one) then go to the channel
  - the URL will look something like `https://app.slack.com/client/T03QK2077/C03QK207F` the final path parameter is the channel id (C03QK207F in this case)
- BlacklistedChannels - this is a single CSV string of channel names (**not ids** e.g. `meta,announcements,trumptweets`) that shouldn't be analysed by Number6
  - This is useful if you have channels with just bot traffic or something similar where it doesn't make sense to perform any semantic analysis. 
  - You'll probably want to include Number6's output channel in this.
- SlackTokenSecretName - the is the name used to store the Slack OAuth token in AWS Secrets Manager that you created earlier
- EnvType - this must be either `prod` or `test` the difference is that creating a `prod` stack will run Number6 at 1am every day analysing the previous day's messages. If you create a `test` stack then Number6 will only ever run when manually triggered and analyse the messages from whatever date you give it
