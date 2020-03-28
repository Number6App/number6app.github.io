## What does it do, exactly?

Number6 runs once a day and uses [Amazon Comprehend](https://aws.amazon.com/comprehend/) to analyse all the messages in each public channel in your Slack workspace. Amazon Comprehend is a natural language processing service, Number6 uses it to report back on the sentiment, entities and key phrases in each channel.

### Sentiment Analysis

Each Slack message has an overall sentiment as well as a score for the 4 sentiments: positive, negative, neutral and mixed. This is an example of how Number6 reports a channel's sentiment:

![Sentiment Analysis]('assets/images/sentiment.jpg')

