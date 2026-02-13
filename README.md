# example-todo-platform-infra

AWS CloudFormation infrastructure for the Todo platform. This stack provisions a wildcard TLS certificate for `*.jaik.me` with additional Subject Alternative Names for `*.todoapi.jaik.me` and `*.todo.jaik.me`, validated via DNS against a Route53 Hosted Zone.

## Resources

The CloudFormation template (`infra.yaml`) creates:

- **TodoClientCertificate** — A wildcard SSL/TLS certificate for `*.jaik.me` with SANs for `*.todoapi.jaik.me` and `*.todo.jaik.me`, validated via DNS.

### Cross-Stack Exports

| Export Name              | Description                              |
|--------------------------|------------------------------------------|
| `Projects-CertificateArn`   | ARN of the `*.jaik.me` wildcard certificate (includes SANs for `*.todoapi.jaik.me` and `*.todo.jaik.me`) |
| `Todo-HostedZoneId`         | Route53 Hosted Zone ID for the domain       |

## Files

| File                   | Purpose                                              |
|------------------------|------------------------------------------------------|
| `infra.yaml`           | CloudFormation template defining AWS resources        |
| `deployment-file.yaml` | Deployment configuration (template path + parameters) |

## Parameters

| Parameter          | Type   | Description                                                      |
|--------------------|--------|------------------------------------------------------------------|
| `TodoHostedZoneId` | String | The ID of the Hosted Zone created by AWS when the domain was purchased |

## Prerequisites

- An AWS account with permissions to manage CloudFormation, ACM, and Route53
- A Route53 Hosted Zone for the target domain

## Deployment

This stack is deployed using [AWS CloudFormation Git Sync](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/git-sync.html). The `deployment-file.yaml` contains the template path and parameter values used by the sync process.
