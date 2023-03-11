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

## Homework Challenges
✅ Created a free AWS account, [Destroy your root account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html#id_root-user_manage_delete-key), Set MFA, IAM role, and generated credentials 

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

✅ [Set a billing alarm](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html#turning_on_billing_metrics), [Set a AWS Budget](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-create.html), [Set Budget Notifications using CLI](https://docs.aws.amazon.com/cli/latest/reference/budgets/create-budget.html)
<img width="697" alt="image" src="https://user-images.githubusercontent.com/77580311/219863827-32624873-3762-42ad-b582-893355b20bb4.png">


✅ Review all the questions of each pillars in the [Well Architected](https://aws.amazon.com/architecture/well-architected/) Tool 

✅ Recreated a architectural Diagram in Lucid 
    https://lucid.app/lucidchart/1387d175-9c11-43e7-90cf-5902992f11e4/edit?viewport_loc=-202%2C-410%2C1979%2C986%2C0_0&invitationId=inv_ceeca159-d3ba-417a-97a0-792f8bfa68ae
    
  <img width="749" alt="image" src="https://user-images.githubusercontent.com/77580311/219868178-0ed781ae-752a-4b56-817b-a61a68c7c9b5.png">


✅ Watched all spend and security considerations
