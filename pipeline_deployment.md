[back](./how_do_i_get_it.md)

# Pipeline Deployment

### You will need 

- a local copy of [the Number6 repo](https://github.com/Number6App/Number6), either clone it directly or fork it in GitHub to a repository in your account and clone that.
- 2 AWS accounts set up for CLI access
- the AWS CLI tools installed locally

### You will get

This will create a pipeline deploying to 2 accounts with a Number6 app running in each, a "test" and "production" version. 

- The pipeline is triggered each time a commit is pushed to a given branch in a given GitHub repository. 

- a successful build triggers a Number6 deployment to the test account

- The production deployment requires a manual approval step before running. 

- The S3 bucket containing the build artifacts is encrypted. 

- The pipeline, S3 bucket and encryption key all reside in the test account. 

- Each account requires its own Slack OAuth token stored in AWS Secrets Manager (these can be the same token but they'll still need storing in each account.)

- A GitHub OAuth access token needs to be stored in AWS Secrets Manager (in the test account) to be able to set up the webhook that triggers the pipeline on each commit

  - this has to be saved in AWS Secrets Manager with a name and key of `no6/test/github/2`

- You'll need to create 2 files in the project root named `No6AppTemplateConfig-test.json` and `No6AppTemplateConfig-prod.json`

  - these are JSON files that contain parameters for the test and prod environments that the pipeline will use at deploy time, they both look like this:

  - ```javascript
    {
      "Parameters": {
        "SlackChannel": "<YOUR SLACK CHANNELID>",
        "SlackTokenSecretName": "<YOUR SECRET NAME>",
        "BlacklistedChannels": "<YOUR BLACKLIST>",
        "EnvType": "test|prod"
      }
    }
    ```

  - see [Number6 Deployment Parameters](./number6_deployment_params.md) for the values to use when creating these files

### Create Pipeline

To create the pipeline run `./no6.sh` in the project root, this will ask for the following parameters:

- **test acct** - AWS's account id for the test account (a 12 digit number)
- **prod acct** - AWS's account id for the production account (a 12 digit number)
- **AWS profile** - this is the name of a profile in your `~/.aws/credentials` file which is the account that the pipeline stack will be created in (and should be the test acct specified previously)
  - you'll probably have one called "default" but you'll still need to specify `default` at the prompt if that's the one you want to use
- **AWS region** - the name of the region to create the stack in, e.g. `eu-west-1`
- **GitHub Owner** - the name of the GitHub account where the Number6 repo lives (e.g. `Number6App`)
- **GitHub Repo Name** - the name of the Git repository in the GitHub account (e.g. `Number6`)
- **GitHub branch name** - the name of the branch to build from whenever there is a commit to it (e.g. `master`)

It will create a couple of stacks for the encryption keys and the roles in the test account then it will ask for 2 more parameters before it creates the roles in the production account:

- **S3 Bucket from the CMK stack**
- **ARN of the CMK in KMS**

both of these can be found from CloudFormation in the AWS console in the test account by clicking on the "Number6-CMK" stack and clicking on "Resources". 

- The name of the S3 bucket can be copied directly as the physical id of the "ArtifactBucket" resource. 

- Click on the physical id of the KMSKey resource, this will take you to the details for this CMK in KMS and you can copy the ARN from the "General Configuration" panel there.

These need pasting in directly to the stack in the production stack because we can't export stack parameters across accounts.

Once both of those have been supplied the rest of the script should complete a few minutes later.

[back](./how_do_i_get_it.md)