# AWS Interview Questions

_Amazon Web Services (AWS) is a comprehensive and widely adopted cloud platform
provided by Amazon. It offers a variety of cloud services such as computing
power, storage options, and networking capabilities, enabling businesses and
developers to deploy, manage, and scale applications without the need for
physical hardware_

2.  ## **What are the key services provided by AWS?**

    _AWS offers numerous services categorized into different domains. Some of
    the key_

    **services include:**

    - **Compute:** _Amazon EC2, AWS Lambda_
    - **Storage:** _Amazon S3, Amazon EBS_
    - **Databases:** _Amazon RDS, Amazon DynamoDB_
    - **Networking:** _Amazon VPC, Amazon Route 53_
    - **Analytics:** _Amazon EMR, Amazon Redshift_

3.  ## **What is an EC2 instance?**

    _**Amazon EC2 (Elastic Compute Cloud)** is a web service that provides
    secure, resizable compute capacity in the cloud. An EC2 instance is a
    virtual server in Amazon’s Elastic Compute Cloud (EC2) for running
    applications on the AWS infrastructure_

4.  ## **How do you launch an EC2 instance?**

    1. Open the Amazon EC2 console.
    2. Click “Launch Instance.”
    3. Choose an Amazon Machine Image (AMI).
    4. Select an instance type based on your requirements.
    5. Configure instance details, such as the number of instances and network
       settings.
    6. Add storage by specifying the size and type of the volume.
    7. Configure security groups to control inbound and outbound traffic.
    8. Review and launch the instance.
    9. Create or select an existing key pair for SSH access.

5.  ## **What is S3 in AWS?**

    _**Amazon S3 (Simple Storage Service)** is a scalable object storage service
    that allows users to store and retrieve any amount of data at any time from
    anywhere on the web. It is designed for 99.999999999% (11 nines)
    durability._

6.  ## **Explain the difference between S3 and EBS**

    - **S3 (Simple Storage Service):** _Object storage service, used for storing
      and retrieving any amount of data. It is highly durable and accessible
      over the internet._
    - **EBS (Elastic Block Store):** _Block storage service, used as storage
      volumes for EC2 instances. It provides persistent storage that can be
      attached to EC2 instances._

7.  ## **What is an AMI?**

    _An **Amazon Machine Image (AMI)** is a pre-configured template for an EC2
    instance that contains the information required to launch an instance. This
    includes the operating system, application server, and applications._

8.  ## **What is the difference between stopping and terminating an EC2 instance?**

    - **Stopping an EC2 instance:** _The instance is shut down, and you will not
      be billed for hourly usage, but the instance’s EBS volume remains and you
      can restart the instance later._
    - **Terminating an EC2 instance:** _The instance is permanently deleted, and
      all associated storage (EBS volumes) is also deleted unless specified
      otherwise._

9.  ## **What is a VPC?**

    _A **Virtual Private Cloud (VPC)** allows you to provision a logically
    isolated section of the AWS cloud where you can launch AWS resources in a
    virtual network defined by you. You have complete control over your virtual
    networking environment._

10. ## **What are the benefits of using AWS?**

    - **Scalability:** _Easily scale resources up or down as needed._
    - **Cost-effective:** _Pay only for the resources you use._
    - **Security:** _Offers robust security features and compliance
      certifications._
    - **Flexibility:** _Wide range of services and tools to build and manage
      applications._
    - **Global Reach:** _Availability zones in multiple regions worldwide._

11. ## **What is the difference between public and private subnets?**

    - **Public Subnet:** _A subnet that is associated with a route table that
      has a route to an internet gateway. Resources in a public subnet can
      communicate with the internet._
    - **Private Subnet:** _A subnet that does not have a route to an internet
      gateway. Resources in a private subnet cannot communicate directly with
      the internet_

12. ## **What is IAM?**

    _**AWS Identity and Access Management (IAM)** is a service that helps you
    securely control access to AWS services and resources. It allows you to
    create and manage AWS users and groups, and to set permissions to allow or
    deny their access to AWS resources._

13. ## **How do you secure data in S3?**

    - **Enable server-side encryption:** _Encrypt data at rest._
    - **Use IAM policies:** _Control access to your S3 resources._
    - **Enable S3 bucket policies:** _Define rules to grant or deny access to
      buckets._
    - **Enable versioning:** _Preserve, retrieve, and restore every version of
      every object in an S3 bucket._
    - **Enable MFA delete:** _Add another layer of security for object
      deletion._

14. ## **What is the purpose of AWS CloudFormation?**

    _**AWS CloudFormation** provides a way to model and set up your AWS
    resources using a template file. It allows you to define the infrastructure
    as code, which helps automate the deployment and management of AWS
    resources._

15. ## **What is AWS Lambda?**

    _**AWS Lambda** is a serverless compute service that allows you to run code
    without provisioning or managing servers. You can run your code in response
    to events, such as changes to data in an S3 bucket or an update to a
    DynamoDB table._

16. ## **What is Auto Scaling?**

    _**Auto Scaling** is an AWS service that automatically adjusts the number of
    EC2 instances in response to changing application demand. This ensures that
    you have the right number of instances running to handle the current load on
    your application._

    **Example:** _You can configure an Auto Scaling group to automatically add
    more EC2 instances when the CPU utilization exceeds a specified threshold,
    and remove instances when the utilization drops below the threshold._

17. ## **How does Elastic Load Balancing work?**

    _Elastic Load Balancing (ELB) automatically distributes incoming application
    traffic across multiple targets, such as EC2 instances, containers, and IP
    addresses. It helps ensure that no single instance is overwhelmed, improving
    fault tolerance and availability._

    **Example:** _A web application can use an ELB to distribute incoming HTTP
    requests across a group of EC2 instances in multiple Availability Zones._

18. ## **Explain the different types of load balancers in AWS.**

    _AWS offers **three types** of load balancers:_

    - **Application Load Balancer (ALB):** _Operates at the application layer
      (HTTP/HTTPS), ideal for web applications_
    - **Network Load Balancer (NLB):** _Operates at the transport layer
      (TCP/UDP), suited for high-performance and low-latency applications._
    - **Classic Load Balancer (CLB):** _Operates at both the application and
      transport layers, used for applications built within the EC2-Classic
      network._

19. ## **What is Amazon RDS?**

    _**Amazon Relational Database Service (RDS)** is a managed database service
    that simplifies the setup, operation, and scaling of relational databases in
    the cloud. It supports multiple database engines, including MySQL,
    PostgreSQL, MariaDB, Oracle, and Microsoft SQL Server_

20. ## **What are Security Groups and Network ACLs?**

    - **Security Groups:** _Virtual firewalls for your EC2 instances that
      control inbound and outbound traffic. They operate at the instance level._
    - **Network ACLs (Access Control Lists):** _Stateless traffic filters that
      control inbound and outbound traffic for subnets within your VPC. They
      operate at the subnet level._

    **Example:** _**A security group** can be configured to allow SSH access
    (port 22) only from a specific IP address, while **a Network ACL** can allow
    HTTP and HTTPS traffic (ports 80 and 443) for a specific subnet_

21. ## **How do you monitor AWS resources?**

    _You can monitor AWS resources using:_

    - **Amazon CloudWatch:** _Collects and tracks metrics, monitors log files,
      and sets alarms._
    - **AWS CloudTrail:** _Provides governance, compliance, and operational and
      risk auditing by recording AWS API calls._

22. ## **What is Amazon CloudWatch?**

    _**Amazon CloudWatch** is a monitoring and observability service that
    provides data and actionable insights to monitor applications, understand
    and respond to system-wide performance changes, and optimize resource
    utilization._

    **Example:** _You can use CloudWatch to create alarms that trigger
    notifications when the CPU utilization of an EC2 instance exceeds a defined
    threshold_

23. ## **What is AWS Route 53?**

    _**AWS Route 53** is a scalable **Domain Name System (DNS)** web service
    designed to route end-user requests to internet applications by translating
    domain names into IP addresses._

    **Example:** _You can use Route 53 to route traffic to different endpoints,
    such as Amazon S3 buckets, EC2 instances, and ELBs, based on DNS queries._

24. ## **Explain the concept of elasticity in AWS.**

    _**Elasticity** refers to the ability of AWS resources to automatically
    scale up or down based on demand. This ensures that the infrastructure can
    handle varying levels of load without over-provisioning or
    under-provisioning resources._

    **Example:** _Using Auto Scaling and ELB together provides elasticity by
    dynamically adjusting the number of EC2 instances handling incoming traffic
    based on real-time demand._

25. ## **What is the difference between RDS and DynamoDB?**

    - **Amazon RDS:** _A managed relational database service supporting
      structured query language (SQL) databases. _
    - **Amazon DynamoDB:** _A managed NoSQL database service designed for fast
      and predictable performance with seamless scalability._

    **Example:** _Use RDS for applications requiring complex queries and
    transactions (e.g., e-commerce platforms), and DynamoDB for applications
    needing low-latency access to large datasets (e.g., real-time analytics)._

26. ## **What is the purpose of AWS Elastic Beanstalk?**

    _**AWS Elastic Beanstalk** is an easy-to-use service for deploying and
    scaling web applications and services. It automatically handles the
    deployment, capacity provisioning, load balancing, auto-scaling, and
    monitoring of applications._

    **Example:** _Developers can deploy a web application by uploading the
    application code, and Elastic Beanstalk handles the rest, including
    launching the necessary infrastructure._

27. ## **How do you use AWS CloudTrail?**

    _**AWS CloudTrail** records AWS API calls and delivers log files to an
    Amazon S3 bucket. It provides visibility into user activity by recording
    actions taken on your account_

    **Example:** _You can use CloudTrail to track changes to your AWS resources,
    such as modifications to security group rules or the creation of new IAM
    users._

28. ## **What is AWS Snowball?**

    _**AWS Snowball** is a data transport solution that uses secure physical
    devices to transfer large amounts of data into and out of AWS. It helps with
    data migration, disaster recovery, and content distribution._

    **Example:** _A company can use Snowball to move petabytes of data from
    their on-premises data center to AWS without using the internet,
    significantly reducing transfer times._

29. ## **What is Amazon ElastiCache?**

    _**Amazon ElastiCache** is a managed in-memory data store and cache service
    that supports Redis and Memcached. It helps improve the performance of
    applications by allowing you to retrieve data from high-throughput and
    low-latency in-memory caches._

    **Example:** _A web application can use ElastiCache to store session data,
    reducing the load on the backend database and improving response times._

30. ## **How do you implement multi-region deployments in AWS?**

    _**Multi-region deployments** involve deploying your application across
    multiple AWS regions to achieve higher availability, fault tolerance, and
    disaster recovery. This can be done using services like Route 53 for DNS
    routing, RDS for cross-region read replicas, and S3 for cross-region
    replication._

    **Example:** _An e-commerce application can be deployed in multiple regions
    using Route 53 for global traffic management, RDS for database replication,
    and S3 for storing and replicating product images._

31. ## **What is AWS Direct Connect?**

    _**AWS Direct Connect** is a cloud service that establishes a dedicated
    network connection from your premises to AWS. Using AWS Direct Connect, you
    can create a private, high-bandwidth network link between your data center,
    office, or colocation environment and AWS. This direct connection can reduce
    network costs, increase bandwidth throughput, and provide a more consistent
    network experience than internet-based connections._

    **Example:** _A company can use AWS Direct Connect to transfer large
    datasets between its on-premises environment and AWS S3, reducing transfer
    times and improving reliability._

32. ## **Explain the use of AWS Lambda with AWS API Gateway.**

    _**AWS Lambda** is a serverless compute service that allows you to run code
    without provisioning or managing servers. **AWS API Gateway** is a fully
    managed service that makes it easy to create, publish, maintain, monitor,
    and secure APIs. When used together, API Gateway can act as a front door for
    your Lambda functions, enabling you to create RESTful APIs that trigger
    Lambda functions upon receiving HTTP requests._

    **Example:** _You can create a Lambda function to process data and then use
    API Gateway to expose an endpoint that triggers this Lambda function
    whenever a specific API request is made._

33. ## **What is the difference between AWS OpsWorks and AWS Elastic Beanstalk?**

    - **AWS OpsWorks:** _is a configuration management service that provides
      managed instances of Chef and Puppet, which are automation platforms that
      allow you to automate server configuration, deployment, and management
      across your Amazon EC2 instances or on-premises compute environments._

    - **AWS Elastic Beanstalk:** _is an easy-to-use service for deploying and
      scaling web applications and services. It automatically handles the
      deployment, from capacity provisioning, load balancing, and auto-scaling
      to application health monitoring._

    **Example:** _Use OpsWorks when you need a higher level of control over
    configuration management using Chef or Puppet. Use Elastic Beanstalk for
    quick deployment and management of web applications without worrying about
    the underlying infrastructure._

34. ## **How do you optimize costs in AWS?**

    _To optimize costs in AWS, you can:_

    - **Use Reserved Instances:** _Purchase reserved capacity for predictable
      workloads._
    - **Auto-scaling:** _Automatically scale your resources based on demand to
      avoid over-provisioning._
    - **Right-sizing:** _Regularly analyze your resource utilization and adjust
      instance sizes accordingly._
    - **Use Spot Instances:** _Take advantage of unused EC2 capacity at a
      reduced cost._
    - **Monitor and manage:** _Use AWS Cost Explorer and AWS Budgets to track
      and manage your spending._

35. ## **What is AWS Global Accelerator?**

    _**AWS Global Accelerator** is a service that improves the availability and
    performance of your applications with global users. It provides static IP
    addresses that act as a fixed entry point to your application endpoints,
    such as EC2 instances, Elastic Load Balancers, or S3 buckets, improving the
    performance and reliability of your applications by routing traffic to the
    nearest AWS region._

    **Example:** _Use Global Accelerator to route traffic from users in
    different geographic locations to the nearest available endpoint, reducing
    latency and improving user experience._

36. ## **Explain the concept of serverless architecture in AWS.**

    _**Serverless architecture** allows you to build and run applications
    without managing infrastructure. AWS provides serverless services like AWS
    Lambda, Amazon API Gateway, Amazon DynamoDB, and Amazon S3. In a serverless
    architecture, your application is divided into individual functions that are
    triggered by events and executed in a managed environment, allowing you to
    focus on code and business logic rather than infrastructure management._

    **Example:** _A serverless web application can use API Gateway to handle
    HTTP requests, Lambda functions to process the requests, and DynamoDB to
    store application data._

37. ## **How do you handle disaster recovery in AWS?**

    _**Disaster recovery** in AWS involves strategies to ensure data protection
    and recovery in the event of a disaster._

    **Techniques include:**

    - **Backups:** _Regularly back up data using AWS services like S3, RDS, and
      EBS snapshots._
    - **Multi-region deployments:** _Deploy applications across multiple AWS
      regions to ensure high availability._
    - **Automated failover:** _Use Route 53 and ELB to automatically route
      traffic to healthy endpoints._
    - **Replication:** _Use services like RDS Read Replicas and DynamoDB global
      tables for cross-region replication._

38. ## **What is Amazon Kinesis?**

    _**Amazon Kinesis** is a platform on AWS to collect, process, and analyze
    real-time, streaming data._

    **It consists of four services:**

    - **Kinesis Data Streams:** _For building custom real-time applications._
    - **Kinesis Data Firehose:** _For loading streaming data into AWS data
      stores._
    - **Kinesis Data Analytics:** _For analyzing streaming data using SQL._
    - **Kinesis Video Streams:** _For securely streaming video from connected
      devices to AWS for analytics, machine learning, and other processing._

39. ## **Explain the concept of Infrastructure as Code (IaC) in AWS.**

    _**Infrastructure as Code (IaC)** is the practice of managing and
    provisioning computing infrastructure through machine-readable configuration
    files rather than physical hardware configuration or interactive
    configuration tools. In AWS, this is typically achieved using AWS
    CloudFormation or AWS CDK (Cloud Development Kit)._

    **Example:** _Use CloudFormation templates to define and provision AWS
    resources like EC2 instances, VPCs, and RDS databases in a consistent and
    repeatable manner. _

40. ## **How do you secure AWS environments?**

    **To secure AWS environments, you can:**

    - **Use IAM roles and policies:** _Implement the principle of least
      privilege._
    - **Enable MFA:** _Use multi-factor authentication for secure access._
    - **Encrypt data:** _Encrypt data at rest and in transit using AWS KMS and
      SSL/TLS._
    - **Monitor and log activities:** _Use CloudTrail and CloudWatch for logging
      and monitoring._
    - **Implement network security:** _Use security groups, Network ACLs, and
      VPCs to control traffic._

41. ## **What is AWS Transit Gateway?**

    _**AWS Transit Gateway** is a service that enables you to connect your
    Amazon VPCs and on-premises networks through a central hub. It simplifies
    network architecture by acting as a hub-and-spoke model, reducing the
    complexity and cost of managing multiple point-to-point connections._

    **Example:** _A large organization can use Transit Gateway to connect
    multiple VPCs and on-premises networks across different regions,
    streamlining network management._

42. ## **How do you use AWS Systems Manager?**

    _**AWS Systems Manager** provides a unified interface to view and control
    your AWS resources. It helps automate operational tasks across AWS
    resources, such as patch management, inventory management, and configuration
    compliance_

    **Example:** _Use Systems Manager to run commands on your EC2 instances,
    automate patching, and maintain a central inventory of your AWS resources._

43. ## **What are AWS Step Functions?**

    _**AWS Step Functions** is a serverless orchestration service that lets you
    coordinate multiple AWS services into serverless workflows. It allows you to
    design and run workflows that stitch together services such as Lambda, ECS,
    and SNS._

    **Example:** _Use Step Functions to automate an order processing workflow
    that involves steps like validating the order, processing payment, and
    updating inventory._

44. ## **Explain the use of AWS Config.**

    _**AWS Config** is a service that enables you to assess, audit, and evaluate
    the configurations of your AWS resources. It continuously monitors and
    records your AWS resource configurations and allows you to automate the
    evaluation of recorded configurations against desired configurations._

    **Example:** _Use AWS Config to track changes to security group rules and
    ensure they comply with your organization’s security policies._

45. ## **How do you manage compliance in AWS?**

    _**Managing compliance** in AWS involves using a combination of AWS services
    and best practices to meet regulatory requirements._

    **Key strategies include:**

    - **AWS Artifact:** _Access AWS compliance reports and agreements._
    - **AWS Config:** _Continuously monitor and record configuration changes._
    - **AWS CloudTrail:** _Record AWS API calls for auditing._
    - **IAM policies:** _Implement least privilege access control._
    - **Encryption:** _Use AWS KMS for data encryption._
