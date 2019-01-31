# How to import existing ec2 instance from aws.

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
 ![instance](https://github.com/kopako/terraform/blob/master/img/instance.jpg)
 
- Now we need to generate a template project
 ```sh
 mkdir terraform-dir && cd terraform-dir
 ```
 
- Create main.tf
```sh
{
        echo 'resource "aws_instance" "example" {'
        echo '  # ...instance configuration...'
        echo '}'
} >> main.tf
 ```
 
terraform-dir
  └ main.tf

main.tf

```js
resource "aws_instance" "example" {
  # ...instance configuration...
}
```
  
  - Initialize terraform project
  ```sh
  terraform init
  ```
  stdout:
  ```
    Initializing provider plugins...
  - Checking for available provider plugins on https://releases.hashicorp.com...
  - Downloading plugin for provider "aws" (1.57.0)...

  The following providers do not have any version constraints in configuration,
  so the latest version was installed.

  To prevent automatic upgrades to new major versions that may contain breaking
  changes, it is recommended to add version = "..." constraints to the
  corresponding provider blocks in configuration, with the constraint strings
  suggested below.

  * provider.aws: version = "~> 1.57"

  Terraform has been successfully initialized!

  You may now begin working with Terraform. Try running "terraform plan" to see
  any changes that are required for your infrastructure. All Terraform commands
  should now work.

  If you ever set or change modules or backend configuration for Terraform,
  rerun this command to reinitialize your working directory. If you forget, other
  commands will detect it and remind you to do so if necessary.
  ```
  - terraform import
  ```sh
  terraform import aws_instance.example i-0c3a0e151e3224520
  ```
stdout:
```
provider.aws.region
The region where AWS operations will take place. Examples
are us-east-1, us-west-2, etc.

Default: us-east-1
Enter a value:
```

-Entering region:
```sh
eu-west-1
```
stdout:
```
aws_instance.example: Importing from ID "i-0c3a0e151e3224520"...
aws_instance.example: Import complete!
  Imported aws_instance (ID: i-0c3a0e151e3224520)
aws_instance.example: Refreshing state... (ID: i-0c3a0e151e3224520)

Import successful!

The resources that were imported are shown above. These resources are now in
your Terraform state and will henceforth be managed by Terraform.
```

Now we have terraform.tfstate created with current configuration of imported instance.
We can read it by running:
```sh
terraform show
```

There if we should edit main.tf according to terraform.tfstate, if we will change some configuration and run terraform plan - it will show us what changes will happen if we will apply edited main.tf configuration.
  
  
