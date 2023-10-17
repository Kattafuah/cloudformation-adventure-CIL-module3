# Why this Repo?
This Repo has been created to document steps taken to provide solutions to a challenge given in Module 3 of the CIL Academy Cloud Engineering Programme (Cohort 6)

# General Objective
Understanding and utilizing IaC via AWS cloudformation to provision and manage resources with templates.

# The Challenge
•	To create a CloudFormation (CFN) Stack that provisions a t2.micro EC2 instance (Amazon Linux 2 AMI) and an S3 bucket.

•	The EC2 instance should be given a role such that it can be accessed via SSM without any key-pairs.

## After creating the CFN stack:

•	Upload some lovely pictures into the S3 bucket.

•	SSM into the EC2 instance and copy the contents of the S3 bucket into a DIRECTORY within your home directory called "mys3backup" (e.g. /home/blessing/mys3backup).

•	Write a Python Script that copies the S3 content to that directory on execution.

•	Set up a cron job so that the Python Script does the above at least once every day at a time of your choosing - morning, noon, or night.

•	As a plus - write up a small design description to show what you have achieved. If you add a picture, you save a thousand words.

# Executing the Challenge
## Template preparation
1. As a prerequisite for the stack creation, a template is prepared in yaml to provision the resources required i.e. Amazon Linux 2 AMI (with role for SSM access) and an S3 bucket.
![Screenshot 2023-10-14 035112](https://github.com/Kattafuah/cloudfront-adventure-CIL-module3/assets/16202873/e3595386-8b23-40e3-b12d-eddeb933bb9b)

2. This template is then uploaded during the stack creation process via the AWS console.
![create stack - upload template](https://github.com/Kattafuah/cloudfront-adventure-CIL-module3/assets/16202873/6ff61ee9-16f7-480b-8f48-a5d7846a5c1b)

## Stack Creation & Resource Provisioning
3. Stack is created with provisioned resources.
![stack created](https://github.com/Kattafuah/cloudfront-adventure-CIL-module3/assets/16202873/16b6327c-254e-4bbb-95ae-283533417f35)

4. Lovely pictures are uploaded into the S3 bucket.
![uploaded pics into s3](https://github.com/Kattafuah/cloudfront-adventure-CIL-module3/assets/16202873/8cf47017-a82e-412d-85a8-855dc2fd54ba)

5. Check your EC2 running instances on your console. Instance should be up and running. Click connect to open up 'connect to instance' options. 
![instance is up and running](https://github.com/Kattafuah/cloudfront-adventure-CIL-module3/assets/16202873/20f69954-19fd-4a1c-bfcc-075b338610c2)

6. Select 'Session Manager' and click connect to SSM into EC2.
![SSM into EC2](https://github.com/Kattafuah/cloudfront-adventure-CIL-module3/assets/16202873/bc3a52c6-3b02-4ed3-bffe-8cde63a81ae7)

## Setting up & Configuring EC2
7. cd into home directory (cd ~) and create directory named 'mys3backup' (mkdir mys3backup).
8. Configure the EC2 instance with your access and secret access keys, default region and output format by executing the command 'aws configure'
9. To copy contents of the S3 bucket into mys3backup directory, execute the command 'aws s3 sync s3://bucketname /home/ssm-user/mys3backup'(replacing 'bucketname' with your s3 bucket name created).
![config VM   copy s3 content to s3backup](https://github.com/Kattafuah/cloudfront-adventure-CIL-module3/assets/16202873/399b06e8-4708-4152-8a9e-e60c250b001f)

10. Install pip package manager and boto3 by executing 'sudo yum install pip' and 'pip install boto3' respectively since python script to be run require boto3.
![install pip](https://github.com/Kattafuah/cloudfront-adventure-CIL-module3/assets/16202873/83b508c4-dffd-4852-965c-918f08fdeceb)

![install boto3](https://github.com/Kattafuah/cloudfront-adventure-CIL-module3/assets/16202873/2b27825d-232c-46ea-97e5-4a473dbaa9e6)

11. Write python Script that copies S3 content to mys3backup directory on execution.
![Pythonsript](https://github.com/Kattafuah/cloudfront-adventure-CIL-module3/assets/16202873/3d83832b-1bb3-4b56-bc70-a1788e81b9e9)

16. Execute 'crontab -e' and set up a cronjob to execute the python script at 5:45am every day '45 05 * * * /usr/bin/python /home/ssm-user/mys3backup/cil_amazonlinux_copyscript.py'
![cronjob](https://github.com/Kattafuah/cloudfront-adventure-CIL-module3/assets/16202873/cece5645-89e7-4a9a-af84-282592000df0)

## Architecture
![architecture](https://github.com/Kattafuah/cloudfront-adventure-CIL-module3/assets/16202873/49310577-2def-4685-a345-8567925f3c2e)

