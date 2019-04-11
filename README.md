# [AWS Certified Developer - Associate](https://aws.amazon.com/certification/certified-developer-associate/)

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
---
> ## EC2 (Elastic compute cloud) just virtual machines in cloud

- ### **EC2 Options**
    - #### On Demand (un predectable workloads)
		- allows to pay a fix rate by hour or by second with no commitment
		- Low cost and flexible without any commitment
		- Used for application with short term or spiky or unpredictible workloads
		- Application being tested or developed on aws for first time
    - #### Reserved (steady state or predectable usage)
		- provides capacity reservation and offers discount on yearly contract
		- used for application with steady state or predictable usage
		- user can make up-front payment to reduce the total cost
		- Standard Ris
		- Convertable Ris
		- Scheduled Ris
    - #### Spot
		- allows to bid on whatever price you want
		- used for applications that have flexible start and end times
		- used by chemical companies
		- NOTE: if a spot instance is terminated by Amazon EC2, you will not be charged for partial hour usage
		However, if you terminate the instance yourself, you will be charged for complete hour in which the instance ran.
    - #### Dedicated hosts
		- physical EC2 servers dedicated to you
		
- ### **EC2 Types**
	 - FIGHT DR MC PX
---
> ## EBS (Virtual Disk in cloud that is attached to EC2 instance) Elastic Block Storage
- ### **EBS Volume Types**		
    - #### **SSD**
		- General Purpose SSD (GP2)
			- Less than 10,000 IOPS
		- Provisioned IOPS SSD (101)- Very high performance
			- MORE THAT 10,000 IOPS
			- Provision of 20,000 IOPS per volume
			- Designed for I/O intensive application
		
	- #### **MAGNETIC**
		- **Throughtput optimized HDD (ST1)**
			- Bid Data
			- Data warehouses
			- Cannot be a boot volume
		- **Cold HDD (SC1)**
			- LOW COST
			- File Servers		
			- cannot be boot volume
		- **Magnetic (standard)**
			- CAN BE A ROOT VOLUME OR BOOTABLE VOLUME LIKE c: DRIVE
			- lowest cost of all EBS volume types
			- infrequest access
---			
> ## Elastic Load Balancer (ELB)
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
```
- Used for file storage, objects, 
- Not for OS & database
- Individual Amazon S3 objects can range in size from a minimum of 0 bytes to a maximum of 5 terabytes. The largest object that can be uploaded in a single PUT is 5 gigabytes. For objects larger than 100 megabytes, customers should consider using the Multipart Upload capability.
- Unlimited storage
- Files are stored in buckets (Similar to Folder)
- S3 is a universal namespace, ie names must be unique globally
- When you upload a file into S3 you're going to receive an HTP 200 code.
- When you add the new object into history you can read it immediately you can read
- But then if you wanted to make a modification or delete that file it can just take a little bit of time to propagate.
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
- Versioning
- Encryption
```
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


> ## Step Functions
Step functions that basically allow you to visualize and test your serverless applications and they provide a graphic console to a range and visualize the components of your applications as a series of steps.

This makes it easy to build and run multistep applications so it functions automatically trigger and track each step and retries when your application executes in order and as expected step functions logs the state of each step.

So when things do go wrong you can go in and diagnose and debug problems quickly.










---
>  Online Mock Test
[Whizlabs](https://www.whizlabs.com/aws-developer-associate/online-course/)


>  Refrences

- ### [User Guid](https://docs.aws.amazon.com/index.html)
- ### [Exam Guid](https://d1.awsstatic.com/training-and-certification/docs-dev-associate/AWS_Certified_Developer_Associate_Updated_June_2018_Exam_Guide_v1.3.pdf)
- ### [Certification Prep](https://aws.amazon.com/certification/certification-prep/)
---
