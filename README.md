# Kubernetes Basics with AWS Cloud9


## 1. Create an AWS Cloud9 Environment

   [AWS Cloud9](https://github.com/t2yijaeho/Docker-with-AWS-Cloud9)


## 2. Choose a proper way to build Kubernetes environment


### 1. Install local Kubernetes with minikube on AWS Cloud9 environment


### 2. Create Amazon EKS cluster and node group with eksctl


### 3. [Create Amazon EKS cluster and node group in new VPC with AWS CloudFormation](https://github.com/t2yijaeho/Amazon-EKS-with-CloudFormation/)

1. Get 
2. Set

## 3. Configure Kubernetes

### 1. Install kubectl (Kubernetes command line utility)

1. Refer to [AWS Guide to install kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html)
    
    ***Set `kubectl version`, `release date` according to Kubernetes version***
    
    ```console
    KUBECTL_VERSION=<kubectl version>
    RELEASE_DATE=<release date>
    echo $KUBECTL_VERSION
    echo $RELEASE_DATE
    ```
    ```console
    mspuser:~/environment $ KUBECTL_VERSION=1.22.6
    mspuser:~/environment $ RELEASE_DATE=2022-03-09
    mspuser:~/environment $ echo $KUBECTL_VERSION
    1.22.6
    mspuser:~/environment $ echo $RELEASE_DATE
    2022-03-09
    mspuser:~/environment $ 
    ```
    
2. Download the Amazon EKS vended kubectl binary
    
    ```console
    curl -o kubectl https://s3.us-west-2.amazonaws.com/amazon-eks/$KUBECTL_VERSION/$RELEASE_DATE/bin/linux/amd64/kubectl
    ```

3. Apply execute permissions to the binary
    ```console
    chmod +x ./kubectl
    ```
    
4. Copy the binary to a folder in PATH
    ```console
    mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin
    ```
    
5. Verify kubectl version
    ```console
    kubectl version --short --client
    ```

    ```console
    mspuser:~/environment $ kubectl version --short --client
    Client Version: v1.22.6-eks-7d68063
    mspuser:~/environment $ 
    ```
