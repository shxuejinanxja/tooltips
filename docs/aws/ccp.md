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
flat filesystem.

### managing objects in a bucket

prefix delimiter
key and value

### access permissions

- bucket policies
- ACLs
  - Server access logging
- IAM policies
- it can be attached directly to the resources. can't attach a IAM policy to an IAMuser in another aws account.

### s3 storage class

you can host different objects under different storage classes with in the same bucket.you do not need to create speerate buckets for each storage class.

#### frequent access

Amazon S3 Standard

#### infrequent access

minimum object size of 128k.

- Amazon S3 Standard-IA
- Amazon S3 One Zone-IA

#### archive storage

- Amazon Glacier
  - initiate a restore request and wait for some time to download data.
- Amazon Glacier Deep Archive
  - lowest cost

#### unpredictable access patterns

- intelligent-tiering

### S3 on Outposts

### versioning

three states:

- unversioned(default)
- versioning-enabled
- versioning-suspended
  you can't change from versioning-enabled back to unversioned. but you can change to versioning-suspended from it.
  ater versioning, the overwrite and delete is not actually happened. just a tag was add to it.
  versioning is not free. see the "how ma i changed from using versioning" [s3 faq](https://aws.amazon.com/s3/faqs/#Billing)
  here is another [article](https://cloudiamo.com/2020/06/20/figuring-out-the-cost-of-versioning-on-amazon-s3/)

### life cycle

can set up rule about after XX days, the objects are tranfor to cheaper storage option.

### s3 bucket policy

[sid](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_sid.html)

### use aws s3 to host a static site

it's quiet easy to host a static site with s3

- uncheck the block public access when create s3 bucket
- set bucket policy that allow s3:getobject for all resources in the bucket
- the access point is the index.html's Object URL
  But please notice that there is a fee about data transfor in aws s3
  [aws s3 priciing](https://aws.amazon.com/s3/pricing/)

## aws networking services - VPCs, Route 53, and CloudFront

### IPv4 and IPv6

Since IPv4 is limited and each device in the internet need unique ip adress, so IANA allocate a range o IP address for private use only. [IANA site](https://www.iana.org/assignments/iana-ipv4-special-registry/iana-ipv4-special-registry.xhtml)
It's IPv4 notation. the number after the forwart slash is the subnet mask number.[about slash notation](https://www.watchguard.com/help/docs/help-center/en-US/Content/en-US/Fireware/overview/networksecurity/slash_about_c.html#:~:text=IPv4%20Slash%20notation%20is%20a%20compact%20way%20to,forward%20slash%20%28%2F%29%2C%20and%20the%20subnet%20mask%20number.)

- 10.0.0.0/8 : 10.0.0.0~10.255.255.255
- 172.16.0.0/12 :172.16.0.0~172.31.255.255
- 192.168.0.0/16 :192.168.0.0~192.168.0.255

  172.16.
  1010 1100 0001 0000
  172.31.
  1010 1100 0001 1111

### local device need inter access. NAT for the rescue

### network size and classes

| class | far left | range   | network portion | host portion |
| ----- | -------- | ------- | --------------- | ------------ |
| A     | 0        | 0~127   | 8               | 24           |
| B     | 10       | 128~191 | 16              | 16           |
| C     | 110      | 192~223 | 24              | 8            |

### subnet masks

AND operation by subnet mask so ip in same subnet will be same.

### subnetting

Subnetting is the process by which you can create sub-networks within a larger network.
involve borrowing additional bits from the host portion of an ip address. these borrowed bits are used to create smaller subnetworks. Not borrow network from left.
192.168.0.0 , subnet mark 255.255.255.224
....1110 0000
can create 8 subnet

- 000 192.168.0.0/27
- 001 192.168.32.0/27
- 010 192.168.64.0/27
- 011 192.168.96.0/27
- 100 192.168.128.0/27
- 101 192.168.160.0/27
- 110 192.168.192.0/27
- 111 192.168.224.0/27

### CIDR

192.168.1.0/24 --> avavible ip address is 256. Usable ip address is 256-2=254

### VPCs

default VPC for inbound internet

### internet access

By default, you custom VPCs need to be configured with internet access if you want the EC2 instances ithe VPC to send traffic to the internet.
If you deploy servers that require direct inbound access from the internet, then you need to depoly them in the subnets that have a direct route to the internet.
To configure a VPC with internet access, you need to deploy an internet gateway.

- gateway
- route table
- EC2 instances in a public must have a public IP address
  in term of cost, it's important to remember that elastic IP addresses are free only while they are associated with an EC2 instance that is in the running state. If it's stopped(or shutdown) you will incur charges for that elastic IP address in an hourly basis.

### VPC security

- security groups
  - firewall that is designed to allow you to configure what type of traffic you permit, inbound and outbound, to your EC2 instances.
  - act at the instance level and not the subnet level
  - each VPC comes with a default security group that allow all traffic inbound but only where the source of that traffic is the security group itself.(aka ec2s associated with same security group can talk with each other)
  - security groups do not allow any traffic to inbound from other sources(other than itself) until you create necessary rules. (specific protocol,port and source of the traffic)
  - implicit allow. even you may not have configureed any inbound rules, response traffic to any outbound request will be premitted inbound by security group. Similar ways works for outbound. This feature is what makes security groups **stateful**
  - other key features:
    - can configure _allow_ but not _deny_
    - specify separate rules for inbound and outbound traffic.
    - can filter traffics based on the protocols and port numbers. Can also specify sources and destinations that can be other **security groups** which thus offering a layered security approach.
- NACLs
  - another firewall service that are designed to protect entire subnets.

### NAT

Enable EC2 instances with private IPv4 address access to internet without directly exposing them on the internet

egress-only internet gateway(for IPv6?)

### VPC peering

It's a private network connection between two VPCs. it means that the traffic betweens VPCs over a peering connection does not traverse the public internet.
The service allows you to connect multiple VPCs so that instances in one VPC can access resources in another VPC.
You can create VPC peering connections between VPCs in one aws account or between aws accounts. it can also be configured between vpcs in the same region or across different regions.

### VPC transit gateway

problem with VPC peering is that every VPC must establish a one-to-one connection with its peer. You also need to configure your route table in eash of the peered VPCs to direct appropriate traffic across the peering connection.

hub-and-spoke architectural model

instead of talking to other VPC peering , all VPC talk to Transit Gateway.

### VPNs

you can also connect your VPC to your corporate network. This type of connection is known as VPN.
A VPN is a secure encrypted site-to-site tunnel established between two endpoints over the public internet.

### direct connect

dedicated private connection that bypasses the internet .

### DNS and aws Route53

DNS: a service which can help translate human-readable names into an IP address.
The process of translating domain names to IP address is called **name resolution**
Amazon Route53 offers following functions:

- Domain registration
  - Hosted zones
    A hosted zone is a container that is used to store and manage your resource records and allows you to define how traffic is routed for your domain and any sub-domains.
    - Public hosted zone
      This is a container that allows you to define how you want to route traffic for your domain name across the public internet.
    - Private hosted zone
      This is a container that allows you to define how you want to route traffic for your domain name across private networks.
  - DNS hostnames
    - private DNS hostnames
    - public DNS hostnames
- DNS routing
  - Routing policies
    - Simple routing policy
    - Failover routing policy
      To offer high avaiability. Health check.
    - Geolocation routing policy
      your users' location is determined from the source of the DNS queries for your web service.
    - Latency routing policy
      offer the lowest latency
    - Weighted routing policy
      route different ratios of your total traffic to different resources associated with a single domain
- Health checks
  - that monitor an endpoint
  - that monitor other health checks
  - that monitor CloudWatch alarms

Traffic Flow and Traffic Policies

- Geoproximity routing policy : avavible only when you use Route53 Traffic Flow.
  _bias_ value
- Route53 Resolver

### CloudFront

- Implementing a robust CDN with Amazon CloudFront.
  To configure Amazon CloudFront, you create a distribution endpoint that defines the types of content you want to serve and the source of that content.
- price class
  the most expensive price class is where your content is accessible via all edge locations globally. It's the default price class when you create your distribution , but ultimately offers the best performance.

### Amazon API Gateway

It helps you design application solutions that favor the microservices architecture in place of monolith design.
With it , the front does not need to call different backend API to get the work done.
With an API gateway, you essentially create an abstraction layer. Expose all the APIs that need to be made avaiable to external clients to call backend service.
The request will then be route to the various backend microservices.

## aws EC2

hypervisor: is a piece of software that allows you to create virtual resources such as virtual servers.

## dictornary

- **on-premise** : On-premises is the software and technology that is located within the physical confines of an enterprise often in the company’s data center as opposed to running remotely on hosted servers or in the cloud.
- authentication : who or what can access the aws services in your account
- authorization : what these entities are permitted to do in your account
- metadata : information about the object—such as its name, and so on

| term           | meaning                                           |
| -------------- | ------------------------------------------------- |
|                |                                                   |
| ACLs           | Access Control Lists                              |
| ARN            | Amazon Resource Name                              |
| AMIs           | Amazon Machine Images                             |
| AuP            | Acceptable Use Policy                             |
| AZ             | avaiability zone                                  |
| bucket         | container                                         |
| CIDR           | Classless Interdomain Routing                     |
| CloudFront     | a CDN                                             |
| CDN            | content delivery network                          |
| DAS            | Direct-Attached Storage                           |
| DDoS           | Distributed Denial of Service                     |
| DR             | Disaster Recovery                                 |
| DNS            | Domain Name System                                |
| DMZ            | demilitarized zone (called public subnets on AWS) |
| EBS            | Elastic Block Store                               |
| EFS            | Elastic File System                               |
| EC2            | Elastic Compute Cloud                             |
| ECS            | Elastic Container Service                         |
| EKS            | Elastic Kubernetes Service                        |
| ELB            | Elastic Load Balancer                             |
| EMR            | Elastic MapReduce                                 |
| ERP            | Enterprise Resource Planning                      |
| EUC            | End User Computing                                |
| HTTPS          | HyperText Transfer Protocol Secure                |
| IETF           | Internet Engineering Task Force                   |
| IANA           | Internet Assigned Numbers Authority               |
| IOPS           | input/output operations per second                |
| Idp            | Identity Provider                                 |
| IEM            | Infrastructure Event Management                   |
| IAM            | Identity and Access Management                    |
| IPSec          | Internet Protocol security                        |
| JSON           | JavaScript Object Notation                        |
| LOB            | line of business                                  |
| NAT            | Network Address Translation                       |
| NACLs          | Network Access Control Lists                      |
| NIC            | Network Interface Card                            |
| OUs            | Organization Units                                |
| PHD            | Personal Health Dashboard                         |
| RDS            | Relational Database Service                       |
| Route 53       | Amazon's DNS                                      |
| S3             | Simple storage Service                            |
| S3 Standard-IA | Amazon S3 Standard-Infrequent Access              |
| S3 One Zone-IA | Amazon S3 One Zone-Infrequent Access              |
| S3TA           | Amazon S3 Transfor Acceleration                   |
| SSL            | Secure Sockets Layer                              |
| STS            | security Token Service                            |
| SANs           | storage area networks                             |
| SMB            | Server MEssage Block                              |
| SCPs           | Service Control Policies                          |
| SSD            | solid-state driver                                |
| TLD            | Top-Level Domain                                  |
| TTL            | time-to-live                                      |
| URL            | Uniform Resource Locator                          |
| UAT            | User Acceptance Testing                           |
| VPC            | Virtual Private Cloud                             |
| VPNs           | Virtual Private Networks                          |
| VPG            | Virtual Private Gateway                           |
| VHD            | Virtual Hard Disk                                 |
|                |                                                   |
|                |                                                   |
|                |                                                   |
|                |                                                   |
