# aws-infra
Infrastructure as a code for AWS resources using cloudformation

### Pre-requisites:
* Setup [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html) 
* Configure credential in local environment for authentication using AWS CLI as shown below: 
```
aws configure
```
Sample output:
```
AWS Access Key ID [*********************]: <access key>
AWS Secret Access Key [********************]: <secret key>
Default region name [ap-south-1]: <region name>
Default output format [None]:
```

### VPC setup
Run below command from root folder(aws-infra) to create vpc stack:
```
aws cloudformation create-stack --stack-name ran --template-body file://vpc.yaml
```
Sample output:
```
{
    "StackId": "arn:aws:cloudformation:ap-south-1:<account-id>:stack/ran/0c7f7090-a0c6-11ec-be0d-028f52b83b4e"
} 
```

### Jenkins setup
Run below command from jenkins folder to provision Jenkins server:
```
aws cloudformation create-stack --stack-name jenkins --template-body file://jenkins.yaml --capabilities CAPABILITY_IAM
```

For deleting, run below command:
```
aws cloudformation delete-stack --stack-name jenkins
```

### EKS k8s setup
Create cluster:
```
eksctl create cluster -f k8s-cluster.yaml 
```

Delete cluster
```
eksctl delete cluster -f k8s-cluster.yaml
```

Verify nodes - kubectl command should work with "~/.kube/config", try below command to get node details:
```
kubectl get nodes
```
