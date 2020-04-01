[back](./)

# How does it work, exactly?

Number6 is a serverless app hosted on AWS, built and deployed using their [Serverless Application Model](https://aws.amazon.com/serverless/sam/) framework. It's based on lambda functions written in Java using a [hexagonal architecture](https://en.wikipedia.org/wiki/Hexagonal_architecture_(software)) ("ports and adaptors") and the [Dagger DI framework.](https://dagger.dev) Here's a picture of it in action:

![Architecture](/assets/images/arch.png)

These are the resources in the diagram:

| Name                        | Type     | Purpose                                                      |
| --------------------------- | -------- | ------------------------------------------------------------ |
| SlackComprehensions         | DynamoDb | Table holding a row for each channel and date that Number6 analyses the Slack workspace |
| SlackReaderFunction         | Lamda    | Calls the Slack API to retrieve all the messages for each public channel each day (or [for a specific date in testing](./how_do_i_test_it.md)), puts them onto the `SlackChannelMessagesTopic` |
| SlackChannelMessagesTopic   | SNS      | topic that notifies listeners of all the messages on a channel for a day |
| MessageSentimentFunction    | Lambda   | listens to `SlackChannelMessagesTopic`, sends all the Slack messages to Amazon Comprehend for sentiment analysis, writes a summary to the `SlackComprehensions` table |
| MessageEntityFunction       | Lambda   | listens to `SlackChannelMessagesTopic`, sends all the Slack messages to Amazon Comprehend for entity analysis, writes a summary to the `SlackComprehensions` table |
| MessageKeyPhrasesFunction   | Lambda   | listens to `SlackChannelMessagesTopic`, sends all the Slack messages to Amazon Comprehend for key phrases analysis, writes a summary to the `SlackComprehensions` table |
| ProcessComprehensionsStream | Lambda   | triggered by updates to the `SlackComprehensions` table, when the sentiment, entity and key phrases analysis for a channel have been completed it posts the details to Slack |

Not shown is AWS Secrets Manager which holds the [Slack access token needed](./what_do_i_need.md) to use the Slack API.

Number6 is created in a single CloudFormation stack containing all its resources with the possible exception of the Slack token in AWS Secrets Manager, depending on [how you choose to deploy it](./how_do_i_get_it.md).

The DynamoDB table is configured for on-demand capacity with no backup schedule. This is the cheapest configuration, if backups and/or higher capacity are important to you you'll need to update the table configuration manually or [deploy a non-SAR version](how_do_i_get_it.md).  

[back](./)