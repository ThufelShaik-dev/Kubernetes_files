## Step - 1 : Create EKS Management Host in AWS

1. Launch new Ubuntu VM using AWS Ec2 ( t2.micro )
2. Connect to machine uisng gitbash and install kubectl using below commands:

---

```
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl

chmod +x ./kubectl

sudo mv ./kubectl /usr/local/bin

kubectl version --short --client
```

---

3. Install AWS CLI latest version using below commands

---

```
sudo apt install unzip
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version
```

---

4. Install eksctl using below commands

---

```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)\_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```

---

## Step - 2 : Create IAM role & attach to EKS Management Host

Since we know using HostVM (ubuntu AMI) we create cluster(using eksctl). so ubuntu need permission to create cluster.we provide permission using IAM role in AWS.

-> Create New Role using IAM service ( Select Usecase - ec2 )

## -> Add below permissions for the role

Administrator, IAM, VPC, EC2, cloudformation - full access
Enter Role Name (eks-role-ec2)

---

->Attach created role to EKS Management Host
(Select EC2 => Click on Security => Modify IAM Role => attach IAM role we have created)

## Step - 3 : Create EKS Cluster using eksctl

---

Syntax:
eksctl create cluster --name cluster-name
--region region-name
--node-type instance-type
--nodes-min 2
--nodes-max 2 \ --zones ,

---

EX: Mumbai region

```
eksctl create cluster --name thufel-cluster --region ap-south-1 --node-type t2.medium --zones ap-south-1a,ap-south-1b
```

---

## Note: Cluster creation will take 10 to 15 mins of time (we have to wait). After cluster created we can check nodes using below command.Run this command in HOST VM gitbash terminal

```
kubectl get nodes
```

## Note: We should be able to see EKS cluster nodes in gitbash terminal. we can also view worker nodes in EC2 instances running in aws console (shows ONE EKS-host-vm, TWO worker-nodes). thats all about EKS Setup in AWS.

## note : we can view our cluster in AWS:

    Go to aws console -> search for EKS -> shows thufel-cluster

## Step - 4 : After practicing, delete Cluster and other resources we have used in AWS Cloud to avoid billing.

```
eksctl delete cluster --name thufel-cluster --region ap-south-1
```

## note : Deleting the cluster will also take 10-15 mins.
