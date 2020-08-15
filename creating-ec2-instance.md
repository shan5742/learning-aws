# Creating my first ec2 instance to talk to s3

My task was to create an ec2 instance on an ubuntu server with a key and security group.

### Creating a key and value pair

Navigate to ec2 dashboard and key pairs, create key value pair and give it a name

### Creating a security group

Navigate to main dashboard, security groups, create.

Fill out basic name and description info

Inbound rules need to be set to my ip so that it can only be accessed via me from my IP address.

### Creating IAM role

Go to IAM dashboard, create new role.

- AWS service, _EC2_, which allows EC2 instances to call AWS services on your behalf.
- Attach **AmazonS3FullAccess** policy to role, so we can enable communication between ec2 instance and s3 storage bucket.

### Setting up ec2 Instance

- Navigate tto EC2 dashboard and select launch instance.
- Select Ubuntu 18.04 server
- Select t2.micro instance type (free tier)
- Add security group created earlier and IAM role created earlier
- Upon launch select existing key that we created earlier

### Connecting to instance

to get correct permissions on certificate we need to run:

```
chmod <path-to-cert>
```

To ssh into instance we need to run:

```
ssh -i <path to key> ubuntu@<instance ip>
```
