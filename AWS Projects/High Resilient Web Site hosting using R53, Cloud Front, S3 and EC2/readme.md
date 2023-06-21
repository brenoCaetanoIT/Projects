# High Resilient Web Site hosting using R53, Cloud Front, S3 and EC2

![pictureCat](https://user-images.githubusercontent.com/136939198/247661690-ef1987b1-ee97-48eb-afbc-0f3892b7123c.jpg)

<h2 style="border-bottom: none;">Project Explanation:</h2>
In this project I deployed a highly resilient static website using AWS Cloud Infrastructure. The website is hosted in 2 different locations the primary location being US-EAST-1a with EC2 and the standby location, in case the primary location,ca-central-1 with S3, which serves as a backup in case the primary location becomes unavailable. To ensure efficient and fast distribution, CloudFront is employed to deliver the website content globally. Below is a concise step-by-step overview of the project implementation.
