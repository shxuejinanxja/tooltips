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

h2 aws and global infrastructure

### region and avaiability zone

one and many

### edge locations

CDN
CloudFront
regional edge caches

### global services

IAM
CloudFront
aws Route 53
aws S3: althrough S3 buckets need to be created in each region. But AWS S3 service is a global services.

### on-premises services

- Amazon Snow Family
- Amazon Storage Gateway
- Amazon Outposts

### aws support plan

- basic support plan
- developer support plan
- business support plan
- enterprise on-ramp
- enterprise

## aws accounts and AWS organizations

## why multi-account aws environment

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

### aws landing zone(deprecated)

baseline blueprint

### aws control tower

deploy landing zone

### managing multi-accounts - aws organizations

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

### how many aws accounts needed?

it's advisrable to create accounts that meet your functional requirement and fulfill your security controls, rather than simply creating accounts based on some corporate hierarchical nature
Start from OUs.

### core aws OUs

- infrastructure services account
  - shared acrss all accounts for common services
- security services

### additional OUs

- sandbox OUs
- workloads OUs
- suspended OUs

## IAM

### aws IAM services

you can **customize** the sign-in url for IAM users.

### MFA

virtual MFA device: app like duo, Microsoft authenticator

### IAM user and IAM groups

root user is the most privileged account and should not be used daily operation

- IAM user
  - person
  - used by applications and other services
  - login by username and password or acccess key ID and secret access key
- IAM groups
  - define IAM policies on group level.
- IAM policies

  - written as JSON documents
  - six types
    - Identity-based policies
      - Managed aws policies
      - Customer-managed policies
      - Inline policies
    - Resources-based policies
    - Permission boundaries
    - Orgranization Service Control Policies
    - ACLs
    - Session policies
  - policy detail
    - Effect: "Allow"
    - Action : can use widecard asterisks(\*)
    - Resource: can use \* or ARN to restrict to specific resource
      - "arn:aws:s3:::packet-marketing-docs"
      - arn example:
        in the previous example the region and account id is ommited with just ":".
        arn:partition:service:region:account-id:resource-id
        arn:partition:service:region:account-id:resource-type/resource-id
        arn:partition:service:region:account-id:resource-type:resource-id

- [IAM policy simulator](https://policysim.aws.amazon.com/https://policysim.aws.amazon.com/)
- assign temporary credentials with IAM roles.
  - advantage of use temporary credentials:
    - more secure
    - avoid distribute credentials around devices
    - avoid credentials management overhead
  - IAM roles can be used to grant access to fedrated users( external users)
  - IAM roles make user of STS. STS assign temporary credentials to the identity that assume the role. temporary credentials include:
  - access key ID
  - secret access key
  - security token
- review credential reports
  - aws allow you download csv file including a list of all your IAM user in your aws account and the status of their credentials.

## s3

### storage options on aws

#### block storage

fixed-size chunk

#### File storage

has limitation of number of folder and depth of path

- EFS
- FSx for Lustre
- FSx for Windows File Server

#### Object storage

- a type of unstructured data
- it's a flat file structure
- metadata can contain many information and used for data analytics

## introduction to aws s3

### buckets and objects

buckets need to have a unique global namespace as their contents can be made accessible over the public internet. It need to be unqiue accoss all aws ecosystem.
first come first serve basis.

## dictornary

- **on-premise** : On-premises is the software and technology that is located within the physical confines of an enterprise often in the company’s data center as opposed to running remotely on hosted servers or in the cloud.
- authentication : who or what can access the aws services in your account
- authorization : what these entities are permitted to do in your account
- metadata : information about the object—such as its name, and so on

| term   | meaning                            |
| ------ | ---------------------------------- |
|        |                                    |
| EFS    | Elastic File System                |
| OUs    | Organization Units                 |
| ACLs   | Access Control Lists               |
| ARN    | Amazon Resource Name               |
| AMIs   | Amazon Machine Images              |
| AuP    | Acceptable Use Policy              |
| AZ     | avaiability zone                   |
| CDN    | content delivery network           |
| DAS    | Direct-Attached Storage            |
| DNS    | Domain Name System                 |
| EBS    | Elastic Block Store                |
| EC2    | Elastic Compute Cloud              |
| ECS    | Elastic Container Service          |
| EKS    | Elastic Kubernetes Service         |
| ELB    | Elastic Load Balancer              |
| EMR    | Elastic MapReduce                  |
| ERP    | Enterprise Resource Planning       |
| UAT    | User Acceptance Testing            |
| LOB    | line of business                   |
| bucket | container                          |
| RDS    | Relational Database Service        |
| PHD    | Personal Health Dashboard          |
| IOPS   | input/output operations per second |
| Idp    | Identity Provider                  |
| IEM    | Infrastructure Event Management    |
| IAM    | Identity and Access Management     |
| SCPs   | Service Control Policies           |
| SSD    | solid-state driver                 |
| S3     | Simple storage Service             |
| STS    | security Token Service             |
| SANs   | storage area networks              |
| SMB    | Server MEssage Block               |
|        |                                    |
