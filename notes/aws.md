public vs private services

- referring to networking only
- public internet - accessed using public network
- aws private zone - can only be accessed within a virtual private cloud (vpc)
  - identities besides the root user has no authorization to access the resource until given
- aws public zone - where aws public services operate
  - runs between public internet and aws private zone
  - not on or part of the public internet
  - network that is connected to the public internet

aws global infrastructure
- aws regions
  - area of the world that contains a full deployment of aws cloud services
  - use regions to design systems that can withstand global disasters
  - e.g. north virginia, ohio, canada
  - benefits
    - geographic separation (something bad that occurs is isolated to the region)
    - geopolitical separation
      - affected by governance and political values of the region
      - data will not leave region without your permission
    - location control (can place infrastructure as close to your customers as possible)
  - availability zones (AZs)
    - isolated infrastructure within a region
    - helps build resilience
- aws edge locations
  - local distribution points (content is closer to customers)
  - high speed distribution and lower latency
  - fast, efficient data transfer
- example: netflix deploys services to multiple regions but content is stored in various edge locations to deliver content at faster speeds
- service resilience
  - globally resilient
    - service operates with single database
    - data replicated across multiple regions
    - region can fail but service will continue running
  - region resilient
    - service that operates in single region with one set of data per region
    - generally replicate data across multiple availability zones in that region
  - AZ resilient
    - service that operates in a single availability zone
    - prone to failure

virtual private cloud (VPC)
- virtual network inside AWS
- regional service (region resilient)
- types
  - **default vpc (1 per region)**
    - initially created by aws, can be removed and recreated
    - pre-configured, less flexible
      - provided with internet gateway (IGW), security group (SG), and NACL
    - default vpc CIDR is always 172.31.0.0/16 (always has the same subnet)
      - /20 subnet always created in each AZ in that region
      - subnets assigned public IPv4 addresses
    - best practice not to use this
  - custom vpc
    - 100% private by default
    - need to configure everything yourself

elastic compute cloud (ec2)
- infrastructure as a service (iaas) - unit of consumption is the instance
- private aws service
- must be launched inside a subnet
- AZ resilient
- instance lifecycle
  - running
  - stopped
  - terminated
- amazon machine image (ami)
  - can be created from ec2 instance or used to create ec2 instance
  - attached permissions (which accounts can access the AMI)
    - public - everyone allowed
    - owner - only owner can access
    - explicit - owner grants permissions to other aws accounts
  - root volume - drive that boots the volume
  - block device mapping - determine which volume is the boot and the data
- can connect to ec2 using rdp (windows) or ssh (linux)

simple storage service (s3)
- global storage platform
- public service (aws public zone)
- region resilient
- buckets
  - **bucket names**
    - names are globally unique (must be unique across all regions and aws accounts)
    - must be 3-63 characters, all lower-case, no underscore
    - must start with a lowercase letter or number
    - can't be IP formatted (e.g. 1.1.1.1)
  - **can have limited number of buckets per account (100 soft limit, 1000 hard limit)**
  - **unlimited objects in bucket (0 bytes - 5 tb each)**
  - **key = filename, value = data**
  - have flat structure (everything is stored at the root)
- should always consider using s3 as the default storage system of choice

cloudformation
- **`Description` field must follow `AWSTemplateFormatVersion` if you provide both**

shared responsibility model
- aws - responsible for security of the cloud
  - hardware
  - infrastructure
  - regions, AZs, edge locations
- customer - responsible for security in the cloud
  - networking traffic

HA vs. FT vs. DR
- high availability
  - system designed to be online as much as possible
  - maximizing system's online time
  - not about user experience
  - **minimize any outages**
- fault tolerance
  - continue operating through a failure (even while being fixed) without disruption to the user
  - level of redundancy of system and components
  - more complex to implement than high availability
  - **operate through faults**
- disaster recovery
  - have processes (and components/infrastructure/staff) in place and design what to do when disaster occurs
  - keep crucial and non-replaceable parts of system safe to rebuild after disaster
  - should have backups stored offsite
  - **used when high availability and fault tolerance don't work**

route 53
- allows us to register domains
- allows us to host zones with managed nameservers
- global service with single database
- **globally resilient**
- can be public or private behind VPC

DNS record types
- Nameserver (NS) - delegation to occur in DNS
- A and AAAA Records
  - maps host names to ip addresses
  - a - ipv4 address
  - aaaa - ipv6 address
- CNAME (canonical name) - host to host records
  - dns shortcuts
  - can only point to other names (can't point to specific ip address)
  - benefit when server ip address changes but cname points to A record -> only A record will need to be updated
- MX Records
  - Finds mail server (SMTP) for a domain
  - Contains priority and value
    - Priority - lower priority values means higher priority
    - Value - domain name
      - Fully qualified domain name contains dot(s) (.) that can point to same domain or outside domain
- TXT Records
  - Add arbitrary text to domain
  - Common usage is to prove domain ownership, fight spam

QUIZ
- what permissions options does an AMI have? [wrong]
  - public access, owner only, specific aws accounts [correct]
  - public access, owner only, specific iam users
  - public access, owner only, specific regions
  - public access, specific aws accounts, specific iam users
- ec2 is an example of which service model
  - pass
  - iaas [correct]
  - saas
  - dbaas
  - faas
- what is true of an aws public service
  - located in the public internet zone
  - located in the aws public zone [correct]
  - located in a vpc
  - publicly accessible by anyone
  - anyone can connect but permissions are required to access the service [correct]
- what is true of an aws private service [wrong]
  - located on the public internet
  - located in the aws public zone
  - located in a vpc [correct]
  - accessible from the vpc it is located in [correct]
  - accessible from any other vpc
  - accessible from other vpcs or on-premises networks as long as private networking is configured [correct]
- what is true of s3 [wrong]
  - s3 is an aws public service [correct]
  - s3 is a private service
  - s3 is a web scale block storage system
  - s3 is an object storage system [correct]
  - buckets can store a limit of 100tb of data
  - buckets can store an unlimited amount of data [correct]
- what is a cloudformation logical resource
  - a resource is a stack which hasn't been created yet
  - a resource defined in a cloudformation template [correct]
  - a resource created in an aws account by cloudformation
  - a name given to a resource created with best practice configuration
- what is a cloudformation physical resource
  - a resource defined in a cloudformation template i.e. ec2instance
  - a physical resource created by creating a cloudformation stack [correct]
  - a product in aws which is a physical piece of hardware i.e. a router
  - none of the above
- what is a simple and correct definition of high availability
  - a system which maximizes uptime
  - a system which is highly performing
  - a system which can operate through failure
  - a system which has regular backups and restore processes
- which of the following is a correct definition of a fault-tolerant system
  - a system which uses automation to return a service to operational status with little user disruption
  - a system which has a 99.999% uptime
  - a system which allows failure and can continue oeprating without disruption [correct]
  - a system which has regular and reliable system backups and restore processes
- how many dns root servers exist [wrong]
  - 12
  - 13 [correct]
  - 7
  - 100
- who manages the dns root servers [wrong]
  - iana
  - 12 large organizations [correct]
  - iana root server board
  - google
- who manages the dns root zone
  - iana [correct]
  - 12 large organizations
  - iana root server board
  - microsoft
  - nobody manages the root zone - its managed via the root hints file
- which dns record type converts a host into an ipv4 address
  - a [correct]
  - aaaa
  - txt
  - mx
  - cname
  - ns
- which dns record type is how the root zone delegates control of .org to the .org registry
  - a
  - aaaa
  - txt
  - cname
  - mx
  - ns [correct]
- which type of organization maintains the zones for a TLD (e.g. org) [wrong]
  - registrar
  - registry [correct]
  - iana
  - none of the above
- which type of organization has relationships with the .org TLD zone manager allowing domain registration [wrong]
  - registrar [correct]
  - registry
  - iana
  - none of the above
- how many subnets are in a default vpc
  - 2
  - 3
  - equal to the number of AZs in the region the vpc is located in [correct]
  - 10
- what is the default IP CIDR of the default vpc



QUESTIONS
- What's the difference between high availability, fault tolerance, and disaster recovery?


- TLS????????????????
