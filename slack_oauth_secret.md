[< back](./index.md)
# Save Slack OAuth Secret To Secrets Manager

- in the AWS console go to AWS Secrets Manager and click `store a new secret`
- choose the `other types of secret` radio button
- select the `plaintext` tab
- the secret value is the oauth token generated by Slack [when you created your app](./what_do_i_need.md), delete anything in the box that's pregenerated by the AWS console (any JSON formatting etc) and paste the token in
- leave the encryption key as default, select next
- the secret name can be anything you like but it will be a parameter passed to Number6 when you deploy it so something short and descriptive is advisable, `no6/slack`is a good choice.
- Click next, review the details and click 'store'

[< back](./index.md)