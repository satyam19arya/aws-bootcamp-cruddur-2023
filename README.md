Application: Cruddur

![Cruddur Graphic](_docs/assets/cruddur-banner.jpg)
![Cruddur Screenshot](_docs/assets/cruddur-screenshot.png)

## Learning Outcomes
```
✅ To learn how to containerize a frontend and backend web application 
 👉 eg. Docker
✅ To learn how to work with multiple serverless containers 
 👉 eg. AWS Fargate, Amazon ECR
✅ To learn how to abstract API call with GraphQL 
 👉 eg. AWS AppSync
✅ To learn basic data modeling for NoSQL databases 
 👉 eg. Amazon DynamoDB
✅ To learn basic data modeling for SQL databases
 👉 eg. Amazon RDS
✅ To learn aside-caching to improve database performance
 👉 eg. Momento
✅ To learn how to set up a CI/CD pipeline 
 👉 eg. CodeBuild, CodeDeploy, CodePipeline
✅ To learn how to use Infrastructure as Code (IaC)
 👉 eg. CloudFormation
✅ To learn how to offload background jobs to serverless functions
✅ To learn how to setup hosted zones
 👉 Route53
```

## Journaling Homework

The `/journal` directory contains

- [X] [Week 0](journal/week0.md)
- [X] [Week 1](journal/week1.md)
- [X] [Week 2](journal/week2.md)
- [X] [Week 3](journal/week3.md)
- [ ] [Week 4](journal/week4.md)
- [ ] [Week 5](journal/week5.md)
- [ ] [Week 6](journal/week6.md)
- [ ] [Week 7](journal/week7.md)
- [ ] [Week 8](journal/week8.md)
- [ ] [Week 9](journal/week9.md)
- [ ] [Week 10](journal/week10.md)
- [ ] [Week 11](journal/week11.md)
- [ ] [Week 12](journal/week12.md)
- [ ] [Week 13](journal/week13.md)


## Project Scenario
```
A startup company has decided to build their own micro-blogging platform and has hired you to be its first cloud engineer.
The company paid a web-development firm to translate their wireframe designs into a mock web-application for the purpose of demoing to raise capital.
After a successful round of funding, you [the cloud engineer] have been tasked with taking the mock web-application and making it production ready at scale.
The startup company consulted a fractional CTO to help choose some of the technical requirements to place the company on a good technical roadmap:

✅ The frontend application should be written in Javascript using React (functional components).
✅ The backend application should be written in Python using Flask
✅ Since we plan to be API only
✅ Since we want to choose a popular framework API only framework
✅ Since we want a micro-framework because we are offloading as much to the cloud as possible to avoid be a monolithic application
✅ Since we don’t want an ORM because the CTO considers it an anti-pattern
✅ Since Python is the most popular language being learned for cloud right now
✅ That an API specification be defined detailing the exact endpoints required.

The web application:
✅ Shall be deployed to AWS.
✅ Takes advantage of modern-applications cloud services.
✅ Ensure to keep the cloud provider costs as low as possible
