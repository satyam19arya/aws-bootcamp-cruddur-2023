# Week 0 — Billing and Architecture

## Technical Tasks
```
👉 Discussing the format of the bootcamp
👉 Going over the business use-case of our project
👉 Looking at an architectural diagram of what we plan to build
👉 Showcase how to use Lucid Charts to build architectures
👉 Talk about C4 Models
👉 Running through the cloud services we will utilize
👉 Testing that we can access our AWS accounts
👉 Settings up AWS free-tier and understand how to track spend in AWS --> eg . AWS Budgets, AWS Cost Explorer, Billing Alarms
👉 Understanding how to look at monthly billing reports
👉 Launching AWS CloudShell and looking at AWS CLI
👉 Generating AWS credentials
```

## Business Scenario
```
Your company has asked to put together a technical presentation on the proposed architecture that will be implemented so it can be reviewed by the fractional CTO.
Your presentation must include a technical architectural diagram and breakdown of possible services used along with their justification.
The company also wants to generally know what spend we expect to encounter and how we will ensure we keep our spending low.
```

## Homework Challenges

✅ [[Installed AWS CLI Latest version]((https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)) on GitPod Desktop with [env variables](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html)]
   ```
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
   unzip awscliv2.zip
   sudo ./aws/install
   ```

   Updated my .gitpod.yml
   ```
   tasks:
    - name: aws-cli
      env:
         AWS_CLI_AUTO_PROMPT: on-partial
      init:
         cd /workspace
         curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
         unzip awscliv2.zip
         sudo ./aws/install
         cd $THEIA_WORKSPACE_ROOT

   vscode:
     extensions:
       - 42Crunch.vscode-openapi
   ```
   
   Set Env Vars
   ```
   export AWS_ACCESS_KEY_ID=""
   export AWS_SECRET_ACCESS_KEY=""
   export AWS_DEFAULT_REGION=""
  ```
  
  To check env vars
  ```
  env | grep AWS_
  ```
  
  We will tell gitpod to remember these credentials if we relaunch our credentials
  ```
  gp env AWS_ACCESS_KEY_ID=""
  gp env AWS_SECRET_ACCESS_KEY=""
  gp env AWS_DEFAULT_REGION=""
  ```
  Check that AWS cli is working or not:
  ```
  aws sts get-caller-identity
  ```
  Output
  ```
  {
    "UserId": "",
    "Account": "",
    "Arn": ""
  }
  ```

✅ [Destroy your root account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html#id_root-user_manage_delete-key), Set MFA & IAM role

✅ [Set a billing alarm](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html#turning_on_billing_metrics), [Set a AWS Budget](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-create.html), [Set Budget Notifications using CLI](https://docs.aws.amazon.com/cli/latest/reference/budgets/create-budget.html)


✅ Review all the questions of each pillars in the [Well Architected](https://aws.amazon.com/architecture/well-architected/) Tool 

✅ Configured Cloud Trail 

✅ Research the technical and [service limits](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) of specific services and how they could impact the technical path for technical flexibility

✅ Open a support ticket and request a service limit

✅ [Use EventBridge to hookup Health Dashboard](https://docs.aws.amazon.com/health/latest/ug/cloudwatch-events-health.html#creating-event-bridge-events-rule-for-aws-health) to SNS and send notification when there is a service health issue
