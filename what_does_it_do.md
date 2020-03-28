## What does it do, exactly?

Number6 runs once a day and uses [Amazon Comprehend](https://aws.amazon.com/comprehend/) to analyse all the messages in each public channel in your Slack workspace. Amazon Comprehend is a natural language processing service, Number6 uses it to report back on the sentiment, entities and key phrases in each channel.

### Sentiment Analysis

Each Slack message has an overall sentiment as well as a score for the 4 sentiments: positive, negative, neutral and mixed. This is an example of how Number6 reports a channel's sentiment:

![Sentiment Analysis](/assets/images/sentiment.jpg)

There's 2 parts to this:

1. **Message Sentiments** - totals for the overall sentiments for all the messages that day, in this case 23 messages
2. **Overall Sentiment Totals** - this is a summary of the individual sentiment scores expressed as a percentage and rounded up to 2dp. This can provide a more nuanced view of the totals e.g. a message with a positive score of 0.51 and negative score of 0.48 will get an overall rating of positive.

### Entity Analysis

![Entity Analysis](/assets/images/entities.jpg)

