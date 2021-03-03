[back](./how_do_i_get_it.md)

# Deploy a stand-alone copy of Number6

### You will need 

- a local copy of [the Number6 repository](https://github.com/Number6App/Number6), either clone it directly or fork it in GitHub to a repository in your account and clone that.
- an AWS account set up for CLI access
- the AWS CLI tools installed locally
- your [Slack OAuth token stored in AWS Secrets Manager](./slack_oauth_secret.md)

### Run `./no6-app.sh` in the project root, 

it will ask you to supply 3 arguments:

- **aws profile** - this is the name of a profile in your `~/.aws/credentials` file which is the account that the Number6 stack will be created in
  - you'll probably have one called "default" but you'll still need to specify `default` at the prompt if that's the one you want to use
- **aws region** - the name of the region to create the stack in, e.g. `eu-west-1`
- **the name of an S3 bucket** - CloudFormation will use this bucket to upload and deploy the lambda code so obviously you'll need read and write privileges for that bucket for the profile you specify  

It should take a couple of minutes to run, Number6 is a Kotlin app built with Maven so you'll see lots of output from that going up the screen as it compiles, tests and packages everything, when it finishes you'll see something like

```bash
   Successfully packaged artifacts and wrote output template to file template-export.yml.
   Execute the following command to deploy the packaged template
   aws cloudformation deploy --template-file /local/path/to/number6/deploy/template-export.yml --stack-name <YOUR STACK NAME>
```

### Deploy Template

See [this page for the deployment parameters](./number6_deployment_params.md) you'll need to provide next.

#### CLI

You can deploy the template from the command line by running the command given above with the following extra options added to it:

```bash
--capabilities CAPABILITY_IAM --profile <YOUR PROFILE> --region <YOUR REGION> --parameter-overrides SlackChannel=<YOUR SLACK CHANNEL ID> BlacklistedChannels=<YOUR BLACKLIST CSV> SlackTokenSecretName=<YOUR SECRET NAME> EnvType=<YOUR ENV TYPE>
```

and obviously you should replace the angled brackets and their contents with your own values. The `--profile` and `--region` options will probably be the same that you supplied the first time round; they don't have to be but if you change them make sure you still have access to the bucket you specified in the first step.

#### Console

Alternatively you could deploy the template through the AWS console: 

- from the CloudFormation service homepage (making sure you're logged into the right AWS account and in the correct region) select "create stack"
- leave "prepare template" as "Template is ready", choose "upload a template file" as the Template Source and choose the `./deploy/template-export.yml` file, click "next"
- supply [the stack name and parameters](./number6_deployment_params.md) in the boxes it provides
- accept all the other options including the IAM capability check boxes and it will create the stack.

[back](./how_do_i_get_it.md)