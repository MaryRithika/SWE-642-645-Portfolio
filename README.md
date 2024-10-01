# AWS Portfolio Website Hosting and EC2 Deployment

Part 1: Static Website Hosting on Amazon S3
Homepage URL (S3 Hosted):
http://rithikawebsite-ttt2024.s3-website-us-east-1.amazonaws.com


Part 2: Survey Form Hosting on Amazon EC2
Survey Form URL (EC2 Hosted):
http://ec2-18-204-3-68.compute-1.amazonaws.com/

Instructions to Access the Application
Visit the homepage by clicking the S3 URL provided above.
To access the survey form, click the link on the homepage that redirects to the survey form hosted on an EC2 instance.
Alternatively, you can directly visit the survey form by using the EC2 URL provided above.

Part 1: Static Website Hosting on Amazon S3

Step-by-Step Procedure: Hosting a Static Website on Amazon S3

1. Log in to AWS Console:
Open the AWS Management Console and sign in with your credentials.

3. Create an S3 Bucket:
Navigate to the S3 Service.
Click Create Bucket.
Choose a unique bucket name 
Select the appropriate region (e.g., us-east-2).
Uncheck the Block all public access option to allow public access to the website.
Click Create Bucket.

5. Upload Website Files:
Open your newly created bucket.
Navigate to the Objects tab and click Upload.
Upload your website files, including index.html (homepage) and other necessary assets (CSS, images, etc.).

7. Enable Static Website Hosting:
Go to the Properties tab of your S3 bucket.
Scroll down to the Static website hosting section.
Enable static website hosting.
Set index.html as the Index document.
Optionally, set a custom error page (e.g., error.html).
Note the S3 Endpoint URL (e.g., http://swe645hwonee.s3-website.us-east-2.amazonaws.com).


9. Set Permissions:
Go to the Permissions tab of your S3 bucket.
In Bucket Policy, add the following policy to make the bucket publicly accessible:
json
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::swe645hwonee/*"
    }
  ]
}
```
Save the bucket policy.

11. Test Your Website:
Open your browser and visit the S3 Endpoint URL to test your website:
http://swe645hwonee.s3-website.us-east-2.amazonaws.com.
Part 2: Survey Form Hosting on Amazon EC2

Step-by-Step Procedure: Hosting a Survey Form on Amazon EC2
1. Launch an EC2 Instance:
In the AWS Management Console, navigate to EC2 under the Compute section.
Click Launch Instance.
Choose Amazon Linux 2 AMI (or Ubuntu) as the operating system.
Select the t2.micro instance type (free tier eligible).
Configure the instance settings, ensuring the Security Group allows HTTP (port 80) and SSH (port 22) traffic.
2. Connect to the EC2 Instance:
Once the instance is running, connect to it via SSH. Open your terminal and run:
bash
Copy code
ssh -i /path/to/your-key.pem ec2-user@<public-ip>
Replace <public-ip> with the public IP address of your instance and provide the correct path to your .pem key file.
3. Install Apache Web Server:
After connecting to the instance, update the system and install Apache:
bash
```
sudo yum update -y
sudo yum install httpd -y
```
Start and enable the Apache service:

```
sudo systemctl start httpd
sudo systemctl enable httpd
```
4. Upload the Survey Form Files:
Create a directory for your survey form:
```
sudo mkdir /var/www/html/survey
```
Use SCP or another file transfer tool to upload your survey.html file to the EC2 instance:
```
scp -i /path/to/your-key.pem survey.html ec2-user@<public-ip>:/var/www/html/survey/
```
Move the uploaded files to the appropriate directory if needed:
bash
```
sudo mv survey.html /var/www/html/survey/
```

5. Configure EC2 Security Group:
Ensure that the Security Group of your EC2 instance allows inbound traffic on port 80 (HTTP) for public access.

7. Test Your Survey Form:
Open your browser and visit the EC2 public IP address to access the survey form:
vbnet

```
http://<public-ip>/survey.html
Example: http://3.21.75.162/survey.html.
```
Sign in to the AWS Management Console, navigate to the Amazon S3 dashboard, and locate the bucket containing your website files. Upload the updated HTML file or modify the existing HTML file to include a hyperlink pointing to the EC2 instance's public IP address or domain name.

After launching the instance, choose the instance from the dashboard and connect. A new window console will open.

This documentation outlines the steps to host a static website on AWS S3 and a survey form on AWS EC2. Make sure to replace any placeholders (<public-ip>, /path/to/your-key.pem) with the actual values specific to your setup.






