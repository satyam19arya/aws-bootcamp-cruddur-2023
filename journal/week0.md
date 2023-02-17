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
![CLI Installed on GP Desktop](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-AWS%20CLI%20Installed%20on%20GP%20Desktop.png)
![Env Variables](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-Env%20variables.png)
![Created Account ID Env Variable](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-Created%20AccountID%20Env%20Variable.png)
![GP Persistent Env Variables](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-GPEnvVariablesPersisting.png)
![Get Account Contact Information on GP](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-GP-Account-GetContactInformation.png)

✅ [Installed AWS CLI Command Prompter](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-parameters-prompting.html)
![Get Caller Identity](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-GetCallerIdentity.png)
![Get Account Contact Information](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-Account-GetContactInformation.png)

✅ [Destroy your root account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html#id_root-user_manage_delete-key), [Set MFA](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html), [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html)
![MFA, IAM user](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-%20IAM%20Logged%20in.png)
![IAM user logging in](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-%20IAM%20Login.png)

✅ [Set a billing alarm](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html#turning_on_billing_metrics), [Set a AWS Budget](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-create.html), [Set Budget Notifications using CLI](https://docs.aws.amazon.com/cli/latest/reference/budgets/create-budget.html)
![Billing Alert](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-Billing%20Alerts.png)
![Budget](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-Budget.png)

✅ [Applied Org-level Day0 SCP's](https://github.com/hashishrajan/aws-scp-best-practice-policies)
![SCP Created](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-SCP.png)

✅ Review all the questions of each pillars in the [Well Architected](https://aws.amazon.com/architecture/well-architected/) Tool (No specialized lens)

✅ Configured Cloud Trail ![Configure AWS Cloud Trail](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/6938a0f830393ac3cadfcc3baab3e2657fecd273/_docs/Week0-CloudTrailEnabled.png)

✅ Research the technical and [service limits](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) of specific services and how they could impact the technical path for technical flexibility

✅ Open a support ticket and request a service limit
![Ticket](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-SupportCase.png)

✅ [Use EventBridge to hookup Health Dashboard](https://docs.aws.amazon.com/health/latest/ug/cloudwatch-events-health.html#creating-event-bridge-events-rule-for-aws-health) to SNS and send notification when there is a service health issue
![EventBridge SNS Notification rule](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-EventBridge%20Alerts.png)
![SNS Notification Confirmation](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0-EventBridge%20SNS%20Alert%20Confirmation.png)

✅ Create an architectural diagram (to the best of your ability) the CI/CD logical pipeline in Lucid Charts
 ([HighLevel CI/CD Architecture Flow](https://lucid.app/lucidchart/8dd4bb31-a6b9-480b-986f-65f8256dc229/edit?invitationId=inv_743505e2-23ee-42d6-84dc-aabcde24a6d3))
![HighLevel CI/CD Architecture Dgm](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/bbdd9533c80553702b5305f7fff7db499751a2ad/_docs/Week0%20-%20CI_CD%20Architecture%20Diagram.png)
![Architecture Dgm](https://github.com/DionneNoellaBarretto/aws-bootcamp-cruddur-2023/blob/main/_docs/Week0%20-%20CI_CD%20Architecture%20Diagram%20(Andrew's%20walkthrough).png)
