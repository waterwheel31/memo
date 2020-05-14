# AWS


## General 
- 'ARN": Amazon Resource Names
- to see own AWS identiry: `aws sts get-caller-identity` 
- To show crednetials: 
    - `aws configure` 
    - `aws configure list`

## EC2 (VM)
- To see instances: `aws ec2 describe-instances --query "Reservations[*].Instances[*].{Instance:InstanceId,Instance:InstanceType, AZ:Placement.AvailabilityZone,Name:Tags[?Key=='Name']|[0].Value}" --output table` 

## S3 (Storage)
- To see S3 buckets: `aws s3 ls`

## ECR (Container Registry)

- to see the repositories: `aws ecr describe-repositories --output table`
- to login 
    - `aws ecr get-login --no-include-email --region us-east-1` 
    - `sudo (return from the above line)`
    - then you can execute commands, like:
        - `docker pull` 

    