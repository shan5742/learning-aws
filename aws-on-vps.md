# Setting up AWS cli on EC2 VPS instance

To ssh into instance we need to run:

```sh
ssh -i <path to key> ubuntu@<instance ip>
```

Check if aws is installed

```sh
aws --version
```

If not then install like so:

```sh
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip // unzip package not installed on base ubuntu system
unzip awscliv2.zip
sudo ./aws/install
```

Confirm this has worked by re-checking aws version

```sh
aws --version
```

## Interacting with S3

Ok now we have aws cli installed let's create file on VPS and move it to the bucket.

```sh
touch random_file // create test file
sudo apt-get install nano // nano not installed on base ubuntu
nano random_file // add content to est file
```

Once file opens in nano just add some text and then run `ls` to make sure file was created properly. If so then move to bucket like so:

```sh
aws s3 mv  random_file s3://<bucket-name>/
```
