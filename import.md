A new EC2-Nano instance is created via the AWSCLI interface
 Either Terraform import or Terraforming are used to terraformize your instance
AMI and Instance Type are changed via the config files
Documentation has been created to the KnowledgeofThousandYears and a pull request has been sent with the new .md file in it, and rdg5 added as revieweer.

# How to import existing ec2 instance from aws.
====

### AWS CLI

- Make sure you have AWS CLI
  ```sh
  $ aws --version
  ```
  Output should be something like (there and further stdout)
  ```sh
  aws-cli/1.16.96 Python/2.7.10 Darwin/17.7.0 botocore/1.12.86
  ```
- Your credential have been configured
  ```sh
  cat ~/.aws/credentials
  ```
  stdout:
  ```sh
  [default]
  aws_access_key_id = AKKNKXF3KGBDQ5BFFVQ
  aws_secret_access_key = t72aLybwhs+PhJPSpk/c23pzKJ1DBO6HFrZFLki
  ```

### Terraform

- Make sure you've terraform
  ```sh
  terraform -v
  ```
  stdout:
  ```sh
  Terraform v0.11.11
  ```
## Import instance

### For import you need an Instance id and region where i runs.
 
 - Go to the [AWS Management Console](https://console.aws.amazon.com) -> Service -> EC2 (choose your region) -> [instances](https://eu-west-2.console.aws.amazon.com/ec2/v2/home?region=eu-west-2#Instances:)
 

  
