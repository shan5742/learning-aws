# S3 Buckets

Amazon S3 is a super scalable cloud storage service. I decided to create the bucket using the ui, just a few simple steps gets this done. Just adding bucket name and making sure AES encryption is used as well as blocking all bucket access.

This is also very achievable via the AWS cli:

```
aws s3 mb s3://your-bucket-name
```

That is it, bucket created.

### Move local file into bucket

I always prefer using the cli when possible, moving a local file into the bucket is again a simple task when using the AWS cli. I created a file **AWS.pdf** and saved it to my desktop. To move it into my bucket I ran:

```
aws s3 mv Desktop/AWS.pdf s3://my-bucket-name/
```
