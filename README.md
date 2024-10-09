# Stackops Installation
StackOps deployment file, templates and parameter files to install StackOps in a member account
and create IAM Roles for administrative access.

## Why?
Let's say you use AWS Organizations to manage multiple AWS Accounts and you want to establish
an isolated environment for a web application or an API.

Your plan is to use StackOps for IaC and have staged AWS Accounts for build, dev, test, and prod. 
Because the DevOps Engineers for this web application or API are separate from those who manage 
AWS Organizations, you want to restrict access by creating IAM Roles for administrative access in
the staged AWS Accounts only.

## Steps

1. Clone this repo and add the cloned repo to your [Enterprise StackOps](https://stackops.ngin.global/guide/multi)
   installation.
2. Deployment file `stackops-deployment.yaml`
   - obtain the OrganizationAccountAccessRole ARN from the master account for the build, dev, 
     test, and prod AWS Accounts
   - update the `AccountAccessRoleArns` section with the ARNs
3. Parameter file `params/stackops-params.yaml`
   - obtain the LicenseKey from the [StackOps Service app](https://service.stackops.ngin.global)
     and update the `LicenseKey` parameter value
   - update the `AuthorizedUserArns` parameter value with a csv of AWS Principals. If you are 
     using AWS Identity Center, use an AWS Account number that all the users are in,
     preferably NOT the master account number as these users already have access to everything.
4. Commit, push and execution using StackOps

## Update the StackOps CloudFormation Template
This is only required if the StackOps CloudFormation template is updated. If you've just
cloned this repo, you can skip this step.
To obtain the latest StackOps CloudFormation template, use the AWS cli 
command `aws s3 cp s3://ngin.stackops.ap-southeast-2/stackops.yaml ./templates`.
