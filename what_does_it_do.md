[back](./)

# What does it do, exactly?

Number6 runs once a day and uses [Amazon Comprehend](https://aws.amazon.com/comprehend/) to analyse all the messages in each public channel in your Slack workspace. Amazon Comprehend is a natural language processing service, Number6 uses it to report back on the sentiment, entities and key phrases in each channel. 

An example of each part is described in more detail below, Number6 combines them into one report for each public channel. Each report is posted as a message in Number6's own channel (that [you specify when you deploy it](./what_do_i_need.md)) not the channel it's reporting on:

### Sentiment Analysis

Each Slack message is given an overall sentiment as well as a score for each of the 4 sentiments: positive, negative, neutral and mixed. This is an example of how Number6 reports a channel's sentiment:

![Sentiment Analysis](/assets/images/sentiment.jpg)

There's 2 parts to this:

1. **Message Sentiments** - totals for the different sentiments for all the messages that day, in this case 23 messages
2. **Overall Sentiment Totals** - this is a summary of the individual sentiment scores expressed as a percentage and rounded up to 2dp. This can provide a more nuanced view of the totals e.g. a message with a positive score of 0.51 and negative score of 0.48 will get an overall rating of positive.

### Entity Analysis

This tries to identify and categorise entities in the messages, the number in brackets is how many times they occurred. Links are always classified as "Other":

![Entity Analysis](/assets/images/entities.jpg)

### Key Phrases Analysis

This tries to identify key phrases in the messages, this usually produces a large volume of phrases so only key phrases that occur more than once are reported, the number in brackets is how many times they occurred:

![Key Phrases Analysis](/assets/images/keyphrases.jpg)

[back](./)