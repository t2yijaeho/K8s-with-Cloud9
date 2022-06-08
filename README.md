# Kubernetes Basics with AWS Cloud9


## 1. Create an AWS Cloud9 Environment

   [AWS Cloud9](https://github.com/t2yijaeho/Docker-with-AWS-Cloud9)


## 2. Create an Amazon EKS cluster


1. Get an AWS CloudFormation stack template body

    ```console
    wget https://github.com/t2yijaeho/K8s-with-Cloud9/raw/matia/Template/K8sCluster.yaml
    ```

2. Get a AMI ID for Kubernetes worker node EC2

   [Kubernetes version](https://docs.aws.amazon.com/eks/latest/userguide/platform-versions.html)

   [EKS Optimized AMI](https://docs.aws.amazon.com/eks/latest/userguide/eks-optimized-ami.html)
   
   ***Change `<K8s Version>` to your desired kubernetes version***
   
    ```console
    K8S_VERSION=<K8s Version>
    echo $K8S_VERSION
    ```

    ```console
    AMI_ID = $(aws ssm get-parameter \
      --name /aws/service/eks/optimized-ami/$K8S_VERSION/amazon-linux-2/recommended/image_id \
      --query "Parameter.Value" --output text)
    echo $AMI_ID
    ```    

2. Create an AWS CloudFormation stack

    ```console
    aws cloudformation create-stack \
      --stack-name K8sBasics \
      --template-body file://./K8sCluster.yaml \
      --parameters ParameterKey=WorkerImageID,ParameterValue=$IMAGE_ID \
      ParameterKey=K8sVersion,ParameterValue=$K8S_VERSION
    ```

3. Monitor the progress by the CloudFormation stack's events in AWS management console

    <img src="https://github.com/t2yijaeho/Docker-with-AWS-Cloud9/blob/matia/images/CloudFormation%20Stack%20Creation%20Events.png?raw=true">
    

## 3. Configure Kubernetes control plane

