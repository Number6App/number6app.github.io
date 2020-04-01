[back](./)

# What about privacy?

- Number6 only reads messages from your Slack's public channels that it is able to join using a Slack app that you create and only with permissions you grant to it
- You deploy the backend to AWS yourself in your own account, the code and resources are all available for you to examine
- No messages are stored in Number6, once they've been sent to Amazon Comprehend for analysis they're discarded
- Number6 can be configured with a list of channels to permanently exclude them from analysis
- A copy of [the summary analysis](./what_does_it_do.md) is saved to Number6's database in AWS. This is the same analysis that's posted to its Slack channel, persisting it allows for later analysis and comparison of trends over time

[back](./)

