# wordpress-on-aws
This project demonstrates how to deploy a WordPress site on an AWS EC2 instance using an Ubuntu server. It includes steps for configuring Apache, MySQL, and PHP (LAMP stack) and setting up a secure, scalable environment for hosting WordPress on the cloud. The repository provides detailed documentation and scripts to automate the setup process.

o Stop Instance
```
import boto3
region = 'us-west-1'
instances = ['i-12345cb6de4f78g9h', 'i-08ce9b2d7eccf6d26']
ec2 = boto3.client('ec2', region_name=region)

def lambda_handler(event, context):
    ec2.stop_instances(InstanceIds=instances)
    print('stopped your instances: ' + str(instances))
```
