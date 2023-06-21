# High Resilient Web Site hosting using R53, Cloud Front, S3 and EC2

![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)
[diagram]

<summary><h2 style="display: inline-block;">Project Explanation:</h2></summary>
In this project I deployed a highly resilient static website using AWS Cloud Infrastructure. The website is hosted in 2 different locations the primary location being US-EAST-1a with EC2 and the standby location, in case the primary location,ca-central-1 with S3, which serves as a backup in case the primary location becomes unavailable. To ensure efficient and fast distribution, CloudFront is employed to deliver the website content globally. Below is a concise step-by-step overview of the project implementation.

<summary><h2 style="display: inline-block;">Step 1: R53 domain registration and certificate creation</h2></summary>
Step 1 of the project was to register a domain with R53. R53 was chosen over other DNS services due to its seamless integration with AWS services and its convenient auto-renewal feature. The chosen domain name was brenocaetano.com <br>


![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)
[registeredDomains pic]

<summary><h2 style="display: inline-block;">Step 2: EC2 creation</h2></summary>
In the second step of the project, an EC2 instance was created to serve as the primary hosting location for the website. The specific region and Availability Zone selected for the EC2 instance was us-east-1a.

![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)
[ec2 pic]

<summary><h2 style="display: inline-block;">Step 3: S3 creation and configuration</h2></summary>
In step 3 of the project, two buckets were created in separate locations without public access. The first bucket, intended to serve content for both the EC2 instance and the standby S3 bucket location, was created in the us-west-1 region. The second bucket, designed as a standby location in case of unavailability in the us-east-1a Availability Zone or the us-east-1 region, was established in the ca-central-1 region.

![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)
[buckets pic]
<br>

Once both buckets were created, a Multi-Region Access Point was set up to ensure synchronization between them. This access point allowed the replication of content from the us-west-1 bucket to the ca-central-1 bucket, keeping them consistent and up to date.

![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)
[buckets replication pic]


<summary><h2 style="display: inline-block;">Step 4: EC2 configuration</h2></summary>
Following the creation of the bucket containing the website content, the EC2 instance was configured to host the website using the CLI. Additionally, as the S3 bucket and its objects was not made public, an IAM role was created with specific permissions. The role granted privileges for listing the bucket and retrieving its objects This role was then attached to the EC2 instance, enabling it to access and serve the content from the S3 bucket.

![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)
[EC2 CLI sync]

![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)
[EC2 Permissions]

<summary><h2 style="display: inline-block;">Step 5: Cloud Front distribution creation and configuration</h2></summary>
Finally, a CloudFront distribution was created to globally serve the website content from both locations, leveraging the integration with Route 53 and utilizing the website certificate. The CloudFront distribution included both the EC2 instance and the S3 bucket as origins. The behavior of the distribution was configured to redirect HTTP requests to HTTPS, ensuring secure communication. Moreover, an origin group was set up to contain both the EC2 instance as the primary location and the S3 bucket as a failover option in case of any failover.

![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)
[CF distributions]

![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)
[CF distribution origin groups]

Lastly, the cloudfront distribution was utilized as the A Alias record within the website hosted zone.

![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)
[r53 cf as a record pic]

You can see the website by <a href="https://brenocaetano.com" target="_blank">clicking here!</a>




