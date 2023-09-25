# localstack
LocalStack is an open-source framework that lets developers create a local simulation of Amazon Web Services (AWS) on their own machines. It imitates various AWS services like S3, DynamoDB, Lambda, SQS, and more. This allows developers to develop and test AWS applications offline, saving costs and speeding up development cycles. It supports API compatibility, is easy to set up, can run in a Docker container, and offers customization options for simulating various AWS scenarios.

# Steps to setup on local machine
## Using python library
```pip install localstack[version] ```

## Running localstack on Docker
```docker run --rm -it -p 4566:4566 -p 4571:4571 localstack/localstack```

# Using AWS CLI
### Use the below command to install aws, if not installed already.
``` pip install awscli ```

### Setting up local region and credentials to run LocalStack
Configure AWS test environment variables and add the --endpoint-url=<localstack-url> flag to your aws CLI invocations. For example:
```
export AWS_ACCESS_KEY_ID="test"
export AWS_SECRET_ACCESS_KEY="test"
export AWS_DEFAULT_REGION="us-east-1"
```

```aws --endpoint-url=http://localhost:4566 s3api```

**Note**: Few of AWS regions will not work here. For testing purpose, you can choose either us-east-1 or us-west-1

### List down all S3 buckets
```awslocal s3api list-buckets --region us-east-1```

```awslocal s3api list-buckets --region us-east-1```
OR
```aws --endpoint-url=http://localhost:4566 s3api list-buckets --region us-east-1```

### Create a bucket
```aws --endpoint-url=http://localhost:4566 s3api create-bucket --bucket welcome --region us-east-1```

### List down all Lambda functions
```aws --endpoint-url=http://localhost:4566 lambda list-functions```

## Use Terraform with localstack
### Create aws localstack resources using terraform
```
terraform init -upgrade
terraform apply
```
### Verify created resources in AWS localstack
```
aws --endpoint-url=http://localhost:4566 lambda list-functions
aws --endpoint-url=http://localhost:4566 ec2 describe-instances
```

### Remove aws localstack resource using terraform
```terraform destroy```
