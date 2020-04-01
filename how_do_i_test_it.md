[back](./)

# How do I test it?

You can manually trigger Number6 by testing the entry lambda function from the AWS console. You can find this by going to the Lambda service in the AWS console and searching for one with `SlackReaderFunction` in the name. The start of the function's name will vary depending on [how you deployed Number6](./how_do_i_get_it.md) but the middle part will always be `SlackReaderFunction`.

Once you've clicked through to the function's home page there will be a 'Test' button at the top and an empty dropdown list called 'Select a test event'. Clicking on that should give you the option 'Configure test events'. Clicking on that will bring up a screen to create a new test event with a text box for you to enter a JSON payload that will be sent to the function.

You can create an empty event by changing the contents of the text box to 

```json
{
  
}
```

Sending this event to the function will cause it to analyse all the messages from yesterday. Alternatively you can analyse all the messages from a particular date by specifying a `comprehensionDate` field with a string value in the format `YYYY-MM-DD`, e.g.:

```json
{
  "comprehensionDate": "2020-02-29"
}
```

Whatever you choose, give the event a name and save it to go back to the function's home page. From here you should be able to select your event from the drop down and click 'Test' to run the function with it. It will take a few seconds to run and a few seconds after that you should see the output appearing in [the Slack channel you designated for it](./what_do_i_need.md).

[back](./)