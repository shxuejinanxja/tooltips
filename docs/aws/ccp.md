# Study notes of AWS Certified Cloud Practitioner

## What is cloud computing

### six advantage of cloud computing

- trade capital expense for variable expense
- massive economics of scale
- stop guessing capacity
- increae speed and agility
- stop spending money running and maintaining data centers
- go global in minutes

### cloud computing models

- IaaS Infrastructure as a Service
  - greatest fleibility
  - configure the underlying network, storage and compute services
  - example AWS EC2, EBS, Azure VM
- PaaS Platform as a Service
  - remove the burden of configure and managing underlying Infrastructure
  - example: AWS Elastic Beanstalk; Azure Functions; Google App Engine
- SaaS Software as a Service
  - applications are hosted and managed by the provider
  - example: Salesforce; ;Microsoft Office 365;

### three cloud deployment models

- public cloud
- private cloud
- hybrid cloud

### aws and global infrastructure

#### region and avaiability zone

one and many

#### edge locations

CDN
CloudFront
regional edge caches

#### global services

IAM
CloudFront
aws Route 53
aws S3: althrough S3 buckets need to be created in each region. But AWS S3 service is a global services.

#### on-premises services

- Amazon Snow Family
- Amazon Storage Gateway
- Amazon Outposts

#### aws support plan

- basic support plan
- developer support plan
- business support plan
- enterprise on-ramp
- enterprise

### aws accounts and AWS organizations

#### why multi-account aws environment

- isolation
  - experiment
  - development
  - UAT
  - production
- limited visibility
- isolation of security and identity management
  - cross-account access
  - principle of least privilege
- isolation of recovery or audit accounts

#### aws landing zone(deprecated)

baseline blueprint

#### aws control tower

deploy landing zone

#### managing multi-accounts - aws organizations

offered free but the resources are chargeable

- management account -- previously called master account
- member account

Organization Units (OUs)

- where some accounts share similar types of workloads or functions

Service Control Policies(SCPs)

- apply to OUs or directly to account

AWS organizationscan be deployed using one of two options

- All features -- including consolidated billing feature
- consolidated billing feature

benefits of consolidated billing feature

- single bill
- easy tracking
- volume discounts
- free service

#### how many aws accounts needed?

it's advisrable to create accounts that meet your functional requirement and fulfill your security controls, rather than simply creating accounts based on some corporate hierarchical nature
Start from OUs.

#### core aws OUs

- infrastructure services account
  - shared acrss all accounts for common services
- security services

#### additional OUs

- sandbox OUs
- workloads OUs
- suspended OUs

## dictornary

| on-premise | On-premises is the software and technology that is located within the physical confines of an enterprise often in the company’s data center as opposed to running remotely on hosted servers or in the cloud. |

| term   | meaning                         |
| ------ | ------------------------------- |
| OUs    | Organization Units              |
| AMIs   | Amazon Machine Images           |
| AuP    | Acceptable Use Policy           |
| AZ     | avaiability zone                |
| UAT    | User Acceptance Testing         |
| LOB    | line of business                |
| ELB    | Elastic Load Balancer           |
| CDN    | content delivery network        |
| bucket | container                       |
| RDS    | Relational Database Service     |
| DNS    | Domain Name System              |
| EC2    | Elastic Compute Cloud           |
| ECS    | Elastic Container Service       |
| EKS    | Elastic Kubernetes Service      |
| EMR    | Elastic MapReduce               |
| PHD    | Personal Health Dashboard       |
| IEM    | Infrastructure Event Management |
| IAM    | Identity and Access Management  |
| SCPs   | Service Control Policies        |
| SSD    | solid-state driver              |
| S3     | Simple storage Service          |
|        |                                 |
|        |                                 |
|        |                                 |
