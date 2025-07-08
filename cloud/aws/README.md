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
