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
2. This template is then uploaded during the stack creation process via the AWS console.
## Stack Creation & Resource Provisioning
4. Stack is created with provisioned resources.
5. Lovely pictures are uploaded into the S3 bucket.
6. Instance is up and running click connect to open up 'connect to instance' options, select 'Session Manager' and click connect to SSM into EC2.
## Setting up & Configuring EC2
8. cd into home directory (cd ~) and create directory named 'mys3backup' (mkdir mys3backup).
9. Configure EC2 with your access and secret access keys, default region and output format by executing the command 'aws configure'
10. To copy contents of the S3 bucket into mys3backup directory, execute the command 'aws s3 sync s3://bucketname /home/ssm-user/mys3backup'(replacing 'bucketname' with your s3 bucket name created).
11. Install pip package manager and boto3 by executing 'sudo yum install pip' and 'pip install boto3' respectively since python script to be run require boto3.
12. Write python Script that copies S3 content to mys3backup directory on execution. 
13. Execute 'crontab -e' and set up a cronjob to execute the python script at 5:45am every day '45 05 * * * /usr/bin/python /home/ssm-user/mys3backup/cil_amazonlinux_copyscript.py'
## Architecture
