# Kubernetes Basics with AWS Cloud9


## 1. Create an AWS Cloud9 Environment

   [AWS Cloud9](https://github.com/t2yijaeho/Docker-with-AWS-Cloud9)


## 2. Create an Amazon EKS cluster


1. Get an AWS CloudFormation stack template body

    ```console
    wget https://github.com/t2yijaeho/K8s-with-Cloud9/raw/matia/Template/K8sCluster.yaml
    ```

2. Get a AMI ID for Kubernetes worker node EC2

    

    ```console
    aws cloudformation create-stack \
      --stack-name Cloud9IDE \
      --template-body file://./EC2-Cloud9.yaml
    ```    

2. Create an AWS CloudFormation stack

    ```console
    aws cloudformation create-stack \
      --stack-name Cloud9IDE \
      --template-body file://./EC2-Cloud9.yaml
    ```

3. Verify the instance security group creation completed by the CloudFormation stack's events in AWS management console

    <img src="https://github.com/t2yijaeho/Docker-with-AWS-Cloud9/blob/matia/images/SecurityGroup%20Complete.png?raw=true">
    

4. Add inboud rule to AWS Cloud9 EC2 Security Group

    ***It may need some time to get proper Security Group ID (such as sg-01a234b567cd890ef)***

    Find AWS Cloud9 EC2 Security Group ID
    ```bash
    CLOUD9_SECURITY_GROUP_ID=$(aws ec2 describe-security-groups \
      --filters Name=group-name,Values=*Docker-Basics* \
      --query "SecurityGroups[*].[GroupId]" \
      --output text)
    echo $CLOUD9_SECURITY_GROUP_ID
    ```
    
5. Add Local Machine IP address to Security Group inboud rule
    
   Get your local machine public IP address in the browser
   [Your public IP address](http://checkip.amazonaws.com/)
    
   ***Change `<My IP>` to your local machine IP address (ParameterValue must be in CIDR notation)***
    
    ```console
    aws ec2 authorize-security-group-ingress \
      --group-id $CLOUD9_SECURITY_GROUP_ID \
      --protocol all \
      --cidr "<My IP>/32"
    ```

6. Monitor the progress by the CloudFormation stack's events in AWS management console

    <img src="https://github.com/t2yijaeho/Docker-with-AWS-Cloud9/blob/matia/images/CloudFormation%20Stack%20Creation%20Events.png?raw=true">
    
