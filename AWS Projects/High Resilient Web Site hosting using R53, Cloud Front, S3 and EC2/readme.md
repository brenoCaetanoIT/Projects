# High Resilient Web Site hosting using R53, Cloud Front, S3 and EC2

![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)
[diagram]

<summary><h2 style="display: inline-block;">Project Explanation:</h2></summary>
In this project I deployed a highly resilient static website using AWS Cloud Infrastructure. The website is hosted in 2 different locations the primary location being US-EAST-1a with EC2 and the standby location, in case the primary location,ca-central-1 with S3, which serves as a backup in case the primary location becomes unavailable. To ensure efficient and fast distribution, CloudFront is employed to deliver the website content globally. Below is a concise step-by-step overview of the project implementation.

<summary><h2 style="display: inline-block;">Step 1: R53 domain registration</h2></summary>
Step 1 of the project was to register a domain with R53. R53 was chosen over other DNS services due to its seamless integration with AWS services and its convenient auto-renewal feature. The chosen domain name was brenocaetano.com

![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)
[registeredDomains pic]

<summary><h2 style="display: inline-block;">Step 2: EC2 creation</h2></summary>
In the second step of the project, an EC2 instance was created to serve as the primary hosting location for the website. The specific region and Availability Zone selected for the EC2 instance was us-east-1a.
![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)
[ec2 pic]
