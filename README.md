# [AWS Certified Developer - Associate](https://aws.amazon.com/certification/certified-developer-associate/)

<center>
<img alt="Amazon Web Services" src="https://assets.pcmag.com/media/images/514204-amazon-web-services-logo.jpg?width=333&height=245"> <br>
For more information on AWS, visit <a href="https://aws.amazon.com/">aws.amazon.com</a>
</center>

> ## IAM(Identity Access Management)
	- User
	- Groups
	- Role
	- Policies

- ### **Basic or Mandatory IAM Settings**
    - Delete root access key
    - Activate MFA(Multi-Factor Authentacation) on root account
    - Create Individual IAM users
    - user access types
        - Programatic access(login using AWS CLI using access key and secret access key)
        - AWS Management console access
    - Use groups to assign permissions
    - Apply an IAM password policy

- **Root user has complete Admin access**
- **New user has no permissions when created**
- **You can assign up to 10 policies to a single group**
---
> ## EC2 (Elastic compute cloud) just virtual machines in cloud

	Elastic Compute Cloud - Backbone of AWS, provides re-sizable compute capacity in the cloud. Reduces the time required to obtain and boot new server instances to minutes allowing you to quickly scale capacity, both up and down, as your computing requirements change.
- Once an Instance has been launched with instance store storage, you can not attach additional instance store volumes after the instance is launched, only EBS volumes
- By default both Root volumes will be deleted on termination, however you can tell AWS to keep the root device volume on a new instance during launch
- Can not encrypt root volumes, but you can encrypt any additional volumes that are added and attached to an EC2 instance.
- ### **Roles**
	- You can only assign an EC2 role to an instance on create. You can not assign a role after the instance has been created and/or is running
	- You can change the permissions on a role post creation, but can NOT assign a new role to an existing instance
	- Role permissions can be changed, but not swapped
	- Roles are more secure then storing your access key and secret key on individual EC2 instances
	- Roles are easier to manager, You can assign a role, and change permissions on that role at any time which take effect immediately
	- Roles are universal, you can use them in any region

- ### **EC2 Pricing Options/Models**
    - **On Demand (un predectable workloads)**
		- allows to pay a fix rate by hour or by second with no commitment
		- Low cost and flexible without any commitment
		- Used for application with short term or spiky or unpredictible workloads
		- Application being tested or developed on aws for first time
    - **Reserved (steady state or predectable usage)**
		- provides capacity reservation and offers discount on yearly contract
		- used for application with steady state or predictable usage
		- user can make up-front payment to reduce the total cost
		- Standard Ris
		- Convertable Ris
		- Scheduled Ris
    - **Spot**
		- allows to bid on whatever price you want
		- used for applications that have flexible start and end times
		- used by chemical companies
		- **NOTE:** if a spot instance is terminated by Amazon EC2, you will not be charged for partial hour usage
		However, if you terminate the instance yourself, you will be charged for complete hour in which the instance ran.
    - **Dedicated hosts**
		- physical EC2 servers dedicated to you

- ### **EC2 Types**
	 - FIGHT DR MC PX

- ### **Instance sizing:**
	- T2 - Lowest Cost General Purpose - Web/Small DBs
	- M4 - General Purpose - App Servers
	- M3 - General Purpose - App servers
	- C4 - Compute Optimized - CPU Intensive Apps/DBs
	- C3 - Compute Optimized - CPU Intensive Apps/DBs
	- R3 - Memory Optimized - Memory Intensive Apps/DBs
	- G2 - Graphics / General Purpose - Video Encoding/Machine Learning/3D App Streaming
	- I2 - High Speed Storage - NoSQL DBs, Data Warehousing
	- D2 - Dense Storage - Fileservers/Data Warehousing/Hadoop
	- D - Density
	- I - IOPS
	- R - RAM
	- T - Cheap General Purpose
	- M - Main General Purpose
	- C - Compute
	- G - Graphics

- ### **Storage Types:**
	- **Instance Store (Ephemeral):**
		- Instances using instance store storage can not be stopped. If they are, data loss would result
		- If there is an issue with the underlying host and your instance needs to be moved, or is lost, Data is also lost
		- Instance store volumes cannot be detached and reattached to other instances; They exist only for the life of that instance
		- Best used for scratch storage, storage that can be lost at any time with no bad ramifications, such as a cache store
	- **EBS (Elastic Block Storage):- Virtual Disk in cloud that is attached to EC2 instance**
		- Elastic Block Storage is persistent storage that can be used to procure storage to EC2 instances.
		- You can NOT mount 1 EBS volume to multiple EC2 instances instead you must use EFS
		- Default action for EBS volumes is for the root EBS volume to be deleted when the instance is terminated
		- By default, ROOT volumes will be deleted on termination, however with EBS volumes only, you can tell AWS to keep the root device volume
		- EBS backed instances can be stopped, you will NOT lose any data
		- EBS volumes can be detached and reattached to other EC2 instances
		- Number of EBS volumes: 5000
			- **EBS Volume Types**		
				- **SSD**
					- General Purpose SSD (GP2)
						- Less than 10,000 IOPS
						- Total volume storage of General Purpose SSD (gp2) volumes: 20TiB
					- Provisioned IOPS SSD (101)- Very high performance
						- MORE THAT 10,000 IOPS
						- Provision of 20,000 IOPS per volume
						- Designed for I/O intensive application
						- Total volume storage of Provisioned IOPS SSD (io1) volumes: 20TiB					
				-  **MAGNETIC**
					- **Throughtput optimized HDD (ST1)**
						- Bid Data
						- Data warehouses
						- Cannot be a boot volume
						- Total volume storage of Throughput Optimized HDD (st1): 20TiB
					- **Cold HDD (SC1)**
						- LOW COST
						- File Servers		
						- cannot be boot volume
						- Total volume storage of Cold HDD (sc1): 20TiB
					- **Magnetic (standard)**
						- CAN BE A ROOT VOLUME OR BOOTABLE VOLUME LIKE c: DRIVE
						- lowest cost of all EBS volume types
						- infrequest access
						- Ideal for workloads where data is accessed infrequently and apps where the lowest cost storage is important.
						- Ideal for fileservers
						- Total volume storage of Magnetic volumes: 20TiB
- ### **Encryption:**
	- Root Volumes cannot be encrypted by default, you need a 3rd party utility
	- Other volumes added to an instance can be encrypted.

- ### **AMI's: (Amazon Machine Images)**
	- Template for the root volume for the instance (OS, Apps, etc)
	- AMI's are simply snapshots of a root volume and is stored in S3
	- AMI's are regional. You can only launch an AMI from the region in which it was stored
	- You can copy AMI's to other regions using the console, CLI or Amazon EC2 API
	- When you create an AMI, by default its marked private. You have to manually change the permissions to make the image public or share images with individual accounts
	- Hardware Virtual Machines (HVM) AMI's Available
	- Paravirtual (PV) AMI's Available
	- You can select an AMI based on:
		- Region
		- OS
		- Architecture (32 vs. 64 bit)
		- Launch Permissions
		- Storage for the root device (Instance Store Vs. EBS)
			- Types of virtual machines images (AMI)
				- HVM (hardware virtual machine): fully virtualised hardware and boot. Recommended for best performance.
				- PV (paravirtual): uses a special boot loader, can run on hardware that does not have direct support for virtualisation. Recommended for old generation instances.

- ### **Security Groups**
	- Acts like virtual firewalls for the associated EC2 instance
	- If you edit a security group, it takes effect immediately.
	- You can not set any deny rules in security groups, you can only set allow rules
	- There is an implicit deny any any at the end of the security group rules
	- You don't need outbound rules for any inbound request. Rules are stateful meaning that any request allowed in, is automatically allowed out
	- You can have any number of EC2 instances associated with a security group

- ### **Snapshots:**
	- You can take a snapshot of a volume, this will store that volumes snapshot on S3
	- Snapshots are point in time copies of volumes
	- The first snapshot will be a full snapshot of the volume and can take a little time to create
	- Snapshots are incremental, which means that only the blocks that have changes since your last snapshot are moved to S3
	- Snapshots of encrypted volumes are encrypted automatically
	- Volumes restored from encrypted snapshots are encrypted automatically
	- You can share snapshots but only if they are not encrypted
	- Snapshots can be shared with other AWS accounts or made public in the market place again as long as they are NOT encrypted
	- If you are making a snapshot of a root volume, you should stop the instance before taking the snapshot
	- Number of EBS snapshots : 10,000
---			
> ## Elastic Load Balancer (ELB)
Elastic Load Balancing offers two types of load balancers that both feature high availability, automatic scaling, and robust security. These include the Classic Load Balancer that routes traffic based on either **application or network level information**, and the Application Load Balancer that routes traffic based on advanced application level information that includes the **content of the request**.

- When configuring ELB health checks, bear in mind that you may want to create a file like healthcheck.html or point the ping path of the health check to the main index file in your application
- Enable Cross-Zone Load Balancing will distribute load across all back-end instances, even if they exist in different AZ's
- ELBs are NEVER given public IP Addresses, only a public DNS name
- ELBs can be In Service or Out of Service depending on health check results
- Charged by the hour and on a per GB basis of usage
- Must be configured with at least one listener
- A listener must be configured with a protocol and a port for front end (client to ELB connection), as well as a protocol and port for backed end (ELB to instances connection)
- ELBs support HTTP, HTTPS, TCP, and SSL (Secure TCP)
- ELBs support all ports (1-65535)
- ELBs do not support multiple SSL certificates
- HTTP Error Codes:
	- 200 - The request has succeeded
	- 3xx - Redirection
	- 4xx - Client Error (404 not found)
	- 5xx - Server Error
- **There can be 20 Load balancer per region**

- ### **Types of Load Balancer**
	- Application load balancer (http & https traffic Layer 7)
	- Network load balancer (TCP traffic where extreme performance is required : layer 4)
	- Classic load balancer (http/https or tcp)

- ### **Classic load balancer error**
    - 504 i.e the gateway is timed out
    - If you need IPV4 address of end user , look for X-FORWARDED-FOR-HEADER
---
> ## Route53
- Amazon's DNS server
- Allows to map domain name to
	- EC2
	- load balancer
	- s3
---
> ## AWS CLI
```bash
	 aws configure
	 aws s3 ls -- list buckets
	 aws s3 mb s3://bucketname --- make bucket
	 echo "hello some text" > hello.txt -- create a file
	 aws s3 cp hello.txt s3://bucketname --------upload to bucket
	 aws s3 ls s3://bucketname
```
---
> ## EC2 with S3 Role
	- Roles allow you to not use Access Key ID's and Secret Access Keys
	- Roles are preferred from a security prespective
	- Roles are controlled by policies- You can change a policy on a role and it will take immediate affect
	- you can attach and detach roles to running EC2 instances without having to stop or terminate these instances
---
> ## RDS (Relational Databases) - OLTP (online transactional processing)
- **Types**
	- SQL Servers
	- Oracle
	- MySql Servers
	- PostgreSQL
	- Amazon Aurora
	- MAriaDb		
    - RedShift - OLAP - online analytic processing (Data Warehouse - large data sets used only/primarily for reporting)

- ### **ElasticCache - in menory caching**
    - a web service that makes easy to deploy, operate and scale an in-memory cache in cloud
    - The service improves performance of application by allowing to retrive information from fast, managed and in-memory caches
    - **Open-cource caching engines**
        - Memcached
        - Redis
    - **Memcached**
        - Object caching is your primary goal
        - You want to keep things simple as possible
        - You want to scale in/out your cache horizontally
    - **Redis**
        - for davance data types, list, hashes and sets
        - data sorting and ranking (as liaderboards)
        - data persistence
        - Multi-AZ
        - Pub/Sub capabilities

#### Note: open security group of RDS instance 3306 to EC2 security group

- ### **RDS - Backups, Multi-AZ & Read Replicas**
	- ### **Backups**
		- **Types**
			- Automated
			- Snapshots
		- **Automated**
			- allow to recover database to any point time within a retention period
			- retention period can be between 1-35 days
			- will take a full daily snapshot
			- enabled by default
			- backup data is stored in s3
			- you get free storage space equal to size of your database
			- during backup you may experience latency
			- they are deleted after the original RDS instance is deleted
		- **Snapshots**
			- done manually - ie user initiated
			- they are stored even after original RDS is deleted
	- ### **Restoring Backups**
		- whenever you restore a backup automatic or manual snapshot, the restored version of database will be a new RDS instance
			with new DNS endpoint
	- ### **Encryption**
		- Encryption supported for all types of DB's
		- done using AWS Key Management Service(KMS)
		- When RDS is encrypted it encrypts
			- data in it
			- automated backups
			- snapshots
			- read replicas
		- Encrypting an existing DB is not supported
		- To encrypt you should create snapshot, create copy of that and encrypt the copy

	- ### **Multi-AZ**
		- this is for disaster recovery only
		- If you loose your primary DB, amazon will automatically detect that and will update the DNS to point to IP-Address of your Multi-AZ DB
		- Allows you to have exact copy of your production DB
		- Not used for improving performance
		- copies is maintained synchronously

	- ### **Read Replicas**
		- Allows to have read-only copies of production DB
		- mainly used for heavy read only operations
		- these are asynchronous
		- used for scaling
		- must have automatic backup turned on to deploy read replicas
		- can have upto 5 read replicas
		- you can have read replicas of read replicas (but watch for latency)
		- each read replicas will have its own DNS end point
		- you can have read replicas that have Multi-AZ
		- you can create read replicas of Multi-AZ
		- you can have read replicas in different region
---		
> ## S3 (Simple Storage Service)

- Used for file storage, objects
- **S3 URL structures are region/amazon.aws.com/bucketname (https://s3-eu-west-1.amazonaws.com/myawesomebucket)**
- **Bucket/Object url format: http://${BUCKET_NAME}.s3.amazonaws.com/${OBJECT_KEY}**
- **S3 can be used to host (static) websites :  bucket-name.s3-website-<AWS-region>.amazonaws.com**
- And bucket-name.s3-website.AWS-region.amazonaws.com. You can use Cloudfront as a CDN to make the website fast globally.

- Not for OS & database
- Individual Amazon S3 objects can range in size from a minimum of 0 bytes to a maximum of 5 terabytes. The largest object that can be uploaded in a single PUT is 5 gigabytes. For objects larger than 100 megabytes, customers should consider using the Multipart Upload capability.
- Unlimited storage
- Files are stored in buckets (Similar to Folder)
- S3 is a universal namespace, ie names must be unique globally
- When you upload a file into S3 you're going to receive an HTP 200 code.
- Read after write consistency for PUTS of new objects (As soon as you write an object, it is immediately available)
- Eventual consistency for overwrite PUTS and DELETES. (Updating or deleting an object could take time to propagate)
- S3 is object based
	- key - name of object
	- value - data
	- versionId
	- Metadata
	- Subresources
		- bucket policies
		- Access control list
		- Cross Origin Resource Sharing (CORS)
		- Transfre Acceleration
- Build for 99.99% availability
- 99.99999999999% durability (11 x 9s)
- Versioning is available but must be enabled. It is off by default
- Offers encryption, and allows you to secure the data using ACLs
- S3 charges for storage, requests, and data transfer
- Bucket names must be all lowercase, however in US-Standard if creating with the CLI tool, it will allow capital letters
- When you upload a file to S3, by default it is set private

- ## Versioning and Cross-Region Replication (CRR):
	- Versioning must be enabled in order to take advantage of Cross-Region Replication
	- Once Versioning is turned on, it can not be turned off, it can only be suspended
	- If you truly wanted versioning off, you would have to create a new bucket and move your objects
	- When versioning is enabled, you will see a slider tab at the top of the console that will enable you to hide/show all versions of files in the bucket
	- With versioning enabled, if you delete a file, S3 creates a delete marker for that file, which tells the console to not display the file any longer
	- In order to restore a deleted file you simply delete the delete marker file, and the file will then be displayed again in the bucket
	- To move back to a previous version of a file including a deleted file, simply delete the newest version of the file or the delete marker, and the previous version will be displayed
	- Versioning does store multiple copies of the same file. So in the example of taking a 1MB file, and uploading it. Currently your storage usage would be 1MB. Now if you update the file with small tweeks, so that content changes, but the size remains the same, and upload it. With the version tab on hide, you will see only the single updated file, however if you select show on the slider, you will see that both the original 1MB file exists as well as the updated 1MB file, so your total S3 usage is now 2MB not 1MB
	- Cross Region Replication (CRR) has to be enabled on both the source and destination buckets in the selected regions
	- You have the ability to select a separate storage class for any Cross Region Replication destination bucket
	- CRR does NOT replicate existing objects, only future objects meaning that only objects stored post turning the feature on will be replicated
	- Any object that already exists at the time of turning CRR on, will NOT be automatically replicated
	- Versioning integrates with life-cycle management and also supports MFA delete capability. This will use MFA to provide additional security against object deletion

- ## Life-cycle Management:
	- When clicking on Life-cycle, and adding a rule, a rule can be applied to either the entire bucket or a single 'folder' in a bucket
	- Rules can be set to move objects to either separate storage tiers or delete them all together
	- Can be applied to current version and previous versions
	- If multiple actions are selected for example transition from STD to IA storage 30 days after upload, and then Archive 60 days after upload is also selected, once an object is uploaded, 30 days later the object will be moved to IA storage. 30 days after that the object will be moved to glacier.
	- Calculates based on UPLOAD date not Action data
	- Transition from STD to IA storage class requires MINIMUM of 30 days. You can not select or set any data range less than 30 days
	- Archive to Glacier can be set at a minimum of 1 day If STD->IA is NOT set
	- If STD->IA IS set, then you will have to wait a minimum of 60 days to archive the object because the minimum for STD->IA is 30 days, and the transition to glacier then takes an additional 30 days
	- When you enable versioning, there will be 2 sections in life-cycle management tab. 1 for the current version of an object, and another for previous versions
	- Minimum file size for IA storage is 128K for an object
	- Can set policy to permanently delete an object after a given time frame
	- If versioning is enabled, then the object must be set to expire, before it can be permanently deleted
	- Can not move objects to Reduced Redundancy using life-cycle policies

- ## S3 Transfer Acceleration:
- Utilizes the CloudFront Edge Network to accelerate your uploads to S3
- Instead of uploading directly to your S3 bucket, you can use a distinct URL to upload directly to an edge location which will then transfer the file to S3
- Transfer Acceleration URLs will have the format of **bucketname.s3-accelerate.amazonaws.com**
- There is a test utility available that will test uploading direct to S3 vs through Transfer Acceleration, which will show the upload speed from different global locations
- Turning on and using Transfer Acceleration will incur an additional fee

- ## S3 - Storage Tiers/Classes
	- **S3**: regular
	- **S3-IA(Infrequent access)** - low cost , infrequest and rapid access
	- **S3-One Zone IA** - stored in only single availability zone
	- **Reduced Redundency** Storage - not recommended
	- **Glacier**- Used for archiving, very cheap, takes 4-5 hrs to retrive data
	- **Intelligent Tiering** - If you are storing lots of data in S3 and you have unpredictable access patterns then the S3 intelligent

- ## S3 Security
	- By default all newly created buckets are private
	- Setup access control using
		- Bucket Policies - Applied at bucket level
		- Access Control List - Applied at object level
	- you can configure S3 bucket to create access logs , which logs all the request made to bucket and these logs can be stored in other s3 bucket

- ## S3 ACL's & Policies
- ## S3 Encryption
	- **In transit** - encrypts the data over the network, when you're uploading files from your PC into your bucket and also when you're if you're downloading
		- SSl/TLS
	- **At Rest**
		- **Server Side Encryption**
			- **SSE-S3** - header: x-amz-server-side-encryption: AES256
				- S3 managed keys and this means that each object is encrypted with its own unique Key using strong multi-factor encryption
			- **SSE-KMS** -  header: x-amz-server-side-encryption: ams:kms
				- using AWS Key Management service
			- **SSE-C** (Server Side Encryption with customer provided keys)
		- **Client Side Encryption** - you encrypt files before uploading to s3 yourself

- ## Web Hosting:
	- Used for static hosting only; Server side code will not execute
	- Don't need to worry about scaling, ELBs or number of instances, S3 handles all of that for you
	- When you create an S3 bucket or enable hosting, you still need to make sure that either the files or the entire bucket are set to public accesibility
	- Bucket URLs are structured such as https://s3-eu-west-1.amazonaws.com/somebucketname
	- Hosted site URLs are structured as http://somebucketname.s3-website-eu-west-1.amazonaws.com
	- Hosting sites on S3 does not allow HTTPS support
	- Sites hosted on S3 can be served via HTTPS if distributed by cloudfront; Cloudfront would be configured to terminate a client HTTPS requst, and then talk to the bucket via standard HTTP
	- Can be configured to redirect to another URL
- ## CORS Configuration:
	- Cross Origin Resource Sharing (CORS)
	- Configured in the permisssions section of the properties tab in a bucket
	- CORS configuration is in XML format and will be pasted directly into the permissions
	- CORS is required if you are calling an asset that resides in another bucket from the bucket that your static site resides in using the hosted URL

#### And just remember if you want to enforce the use of encryption for your files stored in S-3 use a bucket policy to deny any request that does not include the "x-amz-server-side-encryption" server side encryption parameter within the request header.
---		
> ## CloudFront (Amazon Content delivery network)
- So CloudFront is used to deliver your entire web site including dynamic static streaming and
interactive content using a AWS global network of edge locations. So that means requests for
content are automatically routed to your nearest edge location and content gets delivered to you
with the best possible performance.

- CloudFront is used for S3 Transfre Acceleration - i.e to transfer files at faster rate over long distance

- **Termanologies**
    - **Edge Locations** - location where content will be cached, this is seprate from AWS Region
    - **Origin** - this is the origin of all files that the CDN will distribute, can be S3, EC2, Elastic Load Balancer, Route53
    - **Distribution** - collection of different Edge locations
        - **Web distribution** - websites http/https
        - **RTMP Distribution** - Media Streaming/ Flash multi-media content

- Edge locations are not just read-only, you can write to them
- Objects are cached for life of TTL(Time to LIve)
- Default TTl is 24 hrs
- You can clear object manually but you will be charged

- S3 Performance Optimization
	- **GET-Intensive Workloads** - use CloudFront that will cache the objects
	- **Mixed Request Type Workloads**
        - avoid sequential object names
	    - use perfectly ramdom keyName, which results in strong indexing and will force S3 to store objects in different partitions
---
> ## Elastic Beanstalk
- Readymade environment for running code
- Automatically handles capicity, load banacing, scaling and application health monitering
- Healps to quickly deploy and manage application on environments
---

> ## [Lambda](https://d1.awsstatic.com/whitepapers/serverless-architectures-with-aws-lambda.pdf)
- Can have multiple versions
- Latest version will have 	**$latest**	at the end of ARN
- Versions are immutable (cannot be changed)
- Can split traffic using aliases to different versions
	- Cannot split traffic with $latest, instead create an alias to latest
- **The Lambda runtime environment is based on an Amazon Linux AMI**
- **The
maximum size of a function code package is 50 MB compressed and 250MB
extracted at the time of this publication and 3MB console editor.**
- **Default Timeout is 300 seconds**
- **Lambda code is stored in S3**
- **You can allocate 128 MB of RAM up to 1.5 GB of RAM to your
Lambda function**
- If an
exception occurs when trying to invoke your function in these models, the
invocation will be attempted two more times (with back-off between the retries).
After the third attempt, the event is either discarded or placed onto a dead
letter queue, if you configured one for the function.
A dead letter queue is either an SNS topic or SQS queue that you have
designated as the destination for all failed invocation events
- Exception Handling
	- Throw Error
	- Use DLQ
- [AWS Lambda Limitations](https://docs.aws.amazon.com/lambda/latest/dg/limits.html)

***
> ## Step Functions
Step functions that basically allow you to visualize and test your serverless applications and they provide a graphic console to a range and visualize the components of your applications as a series of steps.

This makes it easy to build and run multistep applications so it functions automatically trigger and track each step and retries when your application executes in order and as expected step functions logs the state of each step.

So when things do go wrong you can go in and diagnose and debug problems quickly.

***
> ## DynamoDB
Fast and flexible NoSQL DB service for all apps that need consistent, single-digit millisecond latency at any scale. It is a fully managed database and supports both document and key-value data models. Its flexible data model and reliable performance make it a great fit for mobile, web, gaming, ad-tech, IoT, and many other applications.

- **Stored on SSD Storage**
- Spread across 3 geographically distinct data centers
- **Eventual Consistent Reads (Default)**
	- Consistency across all copies of data is usually reached within 1 second
	- Repeating a read after a short time should return updated data
	- Best Read Performance
- **Strongly Consistent Reads**
	- Returns a result that reflects all writes that received a successful response prior to the read
- Provisioned throughput capacity
- Write throughput 0.0065 per hour for every 10 units
- Read throughput 0.0065 per hour for every 50 units
- **First 25 GB of storage is free**
- **Storage costs of 25 cents per additional GB per Month**
- Can be expensive for writes, but really really cheap for reads
- **The combined key/value size must not exceed 400 KB for any given document**
- **Supports attribute nesting up to 35 levels**
- Conditional writes are idempotent, you can send the same conditional write request multiple times, but it will have no further effect on the item after the first time Dynamo performs the update
- Supports atomic counters, using the UpdateItem operation to increment or decrement the value of an existing attribute without interfering with other write requests
- Atomic counter updates are not idempotent, the counter will increment each time you call UpdateItem
- If you can have a small margin of error in your data, then use atomic counters
- If your application needs to read multiple items, you can use the BatchGetItem API endpoint;
- **A single request can retrieve up to 1MB of data with as many as 100 items**
- A single BatchGetItem request can retrieve items from multiple tables
- All write requests are applied in the order in which they are received


### **Pricing(calculate the amount of writes and reads per second)**
- Steps
	- Calculate Write's/Read's per second
	- Write/Read capicity unit can handle 1 write/read operation per second
	- Charge for Write is $0.0065 per 10 units
	- Charge for Read is $0.0065 per 50 units

- Example
	- Calculate read & write cost for 28GB of storage and 1,000,000 writes per day
		- Calculate writes per second
			- 1,000,000/24(hrs) = 41,666.67
			- 41,666.67/60(min) = 694.44
			- 694.44/60(sec) = 11.574 writes per second
		- Write/Read capicity unit can handle 1 write/read operation per second
			- This example will require 12 write capicity units
		- Charges for write per 10 units is $0.0065
			- $0.0065/10 = $0.00065 -> per unit
		- Charges for 12 units
			- $0.00065 * 12 = $0.0078
		- Charges for 12 units for 24 hrs
			- $0.0078 * 24 = $0.1872 per day for writes
		- Charge for read is $0.0065 per 50 units
			- $0.0065 / 50 = $0.00013 per unit
		- Charges for 12 units
			- $0.00013 * 12 (required read units) = $0.00156
		- Charges for 12 units for 24 hrs
			- $0.00156 * 24 (hours per day) = $0.03744 per day for reads
		- Using 28 GB storage with first 25 GB free = 3 GB storage required
			- 3 GB * $0.25 per GB (after initial 25) = $0.75

### **Indexes:**
	- Primary Key TYpes:
		- Single Attribute (Unique Id)
			- Partition Key (Hash Key composed of one attribute)
			- No 2 items in a table can have the same partition key value
		- Composit (Unique Id and Date Range)
			- Partition Key & Sort Key (Hash and Range) composed of two attributes
			- 2 Items can have the same partition key, but they MUST have a different sort key
			- All Items with the same partition key are stored together, in sorted order by the sort key value
- **Local Secondary Index (LSI):**
	- Has same partition key but different sort key
	- Can only be created when creating Table
	- Cannot remove or modify after creation
	- Can have 5 LSI per table
- **Global Secondary Index (GSI):**
	- Has DIFFERENT partition key and different sort key
	- Can be created at table creation or added LATER
	- Can have 5 GSI per table

### **Streams:**
- Used to capture any kind of modification of the DynamoDB tables
- If new item is added to the table, the stream captures an image of the entire item, including all of its attributes
- If an item is updated, the stream captures the before and after image of any attributes that were modified in the item
- If an item is deleted from the table, the stream captures an image of the entire item before it was deleted
- Streams are stored for 24 hours and then is lost
- Streams can trigger functions with Lambda that will perform actions based on the instantiation of a stream event

### **Query's:**
- Operation that finds items in a table using only the primary key attribute value
- Must provide a partition attribute name and distinct value to search for
- Optionally can provide a sort key attribute name and value and use comparison operator to refine the search results
- By default a query returns all of the data attributes for items with the specified primary key(s)
- The ProjectionExpression parameter can be used to only return some of the attributes from a query as opposed to the default all
- Results are always sorted by the sort key
- If the data type of the sort key is a number, the results are returned in numeric order
- If the data type of the sort key is a string, the results are returned in order of ASCII character code values
- Sort order is ascending, the ScanIndexForward parameter can be set to false to sort in descending order
- By default queries are eventually consistent but can be changed to strongly consistent
- More efficient then a scan operation
- For quicker response times, design your tables in a way that can use the query, GET, or BatchGetItem API


### **Scans:**
- Examines every item in the table
- By default, a scan returns all of the data attributes for every item
- Can use the ProjectionExpression parameter so that the scan only returns some of the attributes, instead of all
- Always scans the entire table, then filters out values to provide the desired result (added step of removing data from initial dataset)
- Should be avoided on a large table with a filter that removes many results
- As table grows, the scan operation slows
- Examines every item for the requested values, and can use up provisioned throughput for a large table in a single operation


### **Provisioned Throughput:**
- Unit of read provisioned throughput
	- All read operation are performed in chunks of 4kb
	- Eventual consistent reads (default) consist of 2 reads per second
	- Strongly consistent reads consist of 1 read per second
	- Take the (size of the read rounded to the nearest 4 KB chunk / 4 KB) * No. of items = read throughput
	- Divide by 2 if eventually consistent
- Unit of write provisioned throughput:
	- All writes are 1 KB
	- All writes consist of 1 write per second

- Calculate Read/Write Throughput
### Steps
- Calculate number of chunks required to read/write one item
- Multiply with total items to read/write
- All write consist of 1 write operation per second
- Eventual consistent reads (default) consist of 2 reads per second so divide by 2
- Strongly consistent reads consist of 1 read per second


### Calculate Read Throughput
- Example: 1
	-	Application requires to read 10 items of 1 KB per second using eventual consistency, whats the read throughput
	- Calculate the number of read units per item needed
	- 1 KB rounded to the nearest 4 KB increment = 4 (KB) or a single chunk
	- 4 KB / 4 KB = 1 read unit per item
	- 1 x 10 read items = 10
	- Using eventual consistency is 10 /2 = 5
	- 5 units of read throughput
- Example 2:
	- Application requires to read 10 items of 6 KB per second using eventual consistency, whats the read throughput
	- Calculate the number of read units per item needed
	- 6 KB rounded to the nearest 4 KB increment = 8 (KB) or 2 chunks of 4 KB
	- 8 KB / 4 KB = 2 read unit per item
	- 2 x 10 read items = 20
	- Using eventual consistency is 20 /2 = 10
	- 10 units of read throughput

### Calculate Write Throughput
- Example: 1
	- Application requires to write 5 items with each being 10KB in size per second
	- Each write unit consists of 1 KB of data, need to write 5 items per second with each item using 10 KB of data
	- 5 items * 10 KB = 50 write units
	- Write throughput is 50 units
- Example 2:
	- Application requires to write 12 items with each being 100KB in size per second
	- Each write unit consists of 1 KB of data, need to write 12 items per second with each item using 100 KB of data
	- 12 items * 100 KB = 1200 write units
	- Write throughput is 1200 units









---
>  Online Mock Test
[Whizlabs](https://www.whizlabs.com/aws-developer-associate/online-course/)


>  Refrences

- #### [User Guid](https://docs.aws.amazon.com/index.html)
- #### [Exam Guid](https://d1.awsstatic.com/training-and-certification/docs-dev-associate/AWS_Certified_Developer_Associate_Updated_June_2018_Exam_Guide_v1.3.pdf)
- #### [Certification Prep](https://aws.amazon.com/certification/certification-prep/)
---
