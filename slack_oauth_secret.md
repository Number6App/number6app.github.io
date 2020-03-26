[< back](../readme.md)

- in the AWS console go to AWS Secrets Manager (in the AWS account and region) you're deploying Number6 to) and click `store a new secret`
- choose the `other types of secret` radio button
- the secret value is the OAuth token generated by Slack when you created your app (you can find this in `OAuth and Permissions` in the `Features` side menu of your app's page in Slack)
- the secret key can be anything you like but it will be a parameter to Number6 for it to use the secret so something short and descriptive is advisable, `no6/slack` is a good choice.
- use the default encryption key, select next and __make sure you use the secret key as the secret name__, click next and leave automatic rotation disabled
- Click next, review the details (make sure the key and the name are the same) and click 'store'

[< back](../readme.md)