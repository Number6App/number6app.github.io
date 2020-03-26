Run `./no6-app.sh` in the project root, it will ask you to supply 3 arguments:

- aws profile - this is the name of a profile in your `~/.aws/credentials` file which is the account that the Number6 stack will be created in
  - you'll probably have one called "default" but you'll still need to specify `default` at the prompt if that's the one you want to use
- aws region - the name of the region to create the stack in, e.g. `eu-west-1`
- the name of an S3 bucket in the account and region that you're using, CloudFormation will use this to upload and deploy the lambda code

It should take a couple of minutes to run, Number6 is a Java app built with Maven so you'll see lots of output from that going up the screen as it compiles, tests and packages everything, when it finishes you'll see something like

```bash
   Successfully packaged artifacts and wrote output template to file template-export.yml.
   Execute the following command to deploy the packaged template
   aws cloudformation deploy --template-file /local/path/to/number6/deploy/template-export.yml --stack-name <YOUR STACK NAME>
```

See [this page for the deployment parameters](./number6_deployment_params.md) you'll need to provide next.

You can deploy the template from the command line by running the command given above with the following extra options added to it:

```bash
--capabilities CAPABILITY_IAM --profile <YOUR PROFILE> --region <YOUR REGION> --parameter-overrides SlackChannel=<YOUR SLACK CHANNEL ID> BlacklistedChannels=<YOUR BLACKLIST CSV> SlackTokenSecretName=<YOUR SECRET NAME> EnvType=<YOUR ENV TYPE>
```

and obviously you should replace the angled brackets and their contents with your own values.

 Alternatively you could deploy the template through the AWS console: 

- from the CloudFormation page (making sure you're logged into the right AWS account and in the correct region) select "create stack"
- leave "prepare template" as "Template is ready", choose "upload a template file" as the Template Source and choose the `./deploy/template-export.yml` file, click "next"
- supply the stack name and parameters in the boxes it provides
- accept all the other options including the IAM capability check boxes and it will create the stack.