[back](./)

# What about privacy?

- Number6 only reads messages from public channels that it is able to join using a Slack app that you create and only with permissions you grant to it
- The reason for the rigmarole of creating your own Slack app and deploying Number6 yourself to your own AWS account is so that you don't have to trust an opaque third party Slack app that promises it's honestly not storing your Slack messages on its infrastructure
- Number6 can be configured with a list of channels to permanently exclude them from analysis
- No messages are stored in Number6, once they've been analysed they're discarded
- A copy of the summary analysis is saved to Number6's database in AWS. This is the same analysis that's posted to its Slack channel, persisting it allows for later analysis and comparison of trends over time.

[back](./)