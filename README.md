# ECS-CICD

Simple CI/CD pipeline base on AWS ECS.

### Logic diagram:

```mermaid

graph LR

A[Github] -- features branch PR --> H(Jenkins QA testing job)

H -- 1. Jenkins build QA --> D((QA ENV))

H -- 2. trigger --> J(Auto testing) -- 1. if pass, drop QA --> D

J -- 2. build Staging --> C(Jenkins build Staging)

J -- 1. if testing not pass, block merge --> A1[return false to Github]

C --> E((1% PROD))

A -- master merge --> F(Jenkins build Prod) --> G((All PROD))

```

### Requirment

- AWS [Infrastructure](Infrastructure/)

- Github: integrate Github with Jenkins by Github App or webhook.

- Jenkins server: [Job code](CICD/qa_testing.groovy), Jenkinsfile can be saved in independent Repo, like [this](example/Jenkinsfile).

### TOGO

- Not finish yet

- Keep terraform state on remote backend

- Need grayscale releasing pipeline

- Need approval process

### Reference resources

[Log filter and alarm](https://github.com/terraform-aws-modules/terraform-aws-cloudwatch/tree/master/examples/complete-log-metric-filter-and-alarm)