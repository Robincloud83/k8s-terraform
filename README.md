# k8s-terraform
## To install Kubernetes CLI (kubectl) on your Windows PC and work with a cluster in AWS, here’s the step-by-step guide:
## 1️⃣ Install kubectl (Kubernetes CLI)
## Download kubectl for Windows
## Open PowerShell and run:
curl.exe -LO "https://dl.k8s.io/release/v1.30.0/bin/windows/amd64/kubectl.exe"
## (You can replace v1.30.0 with the latest stable version.)
kubectl version --client

## 3️⃣ Install eksctl (for AWS EKS Clusters)
## eksctl is the easiest way to create and manage EKS clusters.
curl -sSL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_Windows_amd64.zip" -o eksctl.zip
### then extract it eksctl.zip
## also move it to "C:\Windows\System32\"
eksctl version
## (Requires Chocolatey package manager.)

## Verify:
eksctl version

## 4️⃣ Create a Kubernetes Cluster in AWS
## Example (2 nodes, t3.micro):
eksctl create cluster --name my-cluster --region ap-south-1 --nodes 2 --node-type t3.micro

## also
## 1️⃣ Create an EKS Cluster

eksctl create cluster `
  --name my-eks-cluster `
  --region eu-north-1 `
  --nodegroup-name my-nodes `
  --node-type t3.medium `
  --nodes 2 `
  --nodes-min 2 `
  --nodes-max 4 `
  --managed
### Explanation:
# --name → Cluster name
# --region → AWS region (eu-north-1 for you)
# --nodegroup-name → Worker node group name
# --node-type → EC2 instance type for nodes
# --nodes → Default node count
# --managed → AWS-managed node group

##  Test the Cluster
kubectl get nodes


kubectl get pods --all-namespaces  

### 2️⃣ Delete an EKS Cluster

eksctl delete cluster --name my-eks-cluster --region eu-north-1
## This will:
## Delete the EKS control plane
## Delete the managed node group
## Release related AWS resources


## If you want, I can give you a single PowerShell script that installs kubectl, aws-cli, eksctl, and creates the AWS cluster in one go. That would save you a lot of manual work.


### let’s get Terraform set up on your Windows PC so you can use it to manage AWS resources (including Kubernetes/EKS).

## 1️⃣ Download Terraform
## Go to: Terraform Downloads
## https://releases.hashicorp.com/terraform/1.12.2/terraform_1.12.2_windows_amd64.zip
## Download the Windows AMD64 ZIP file.
## Extract it — you’ll get a single file called terraform.exe.

### 4️⃣ Verify Installation
### Open a new PowerShell or CMD and run:
terraform -version

## 6️⃣ First Terraform Project (AWS Example)
## Here’s a minimal example to test Terraform:

vim main.tf

provider "aws" {
  region = "ap-south-1"
}

resource "aws_s3_bucket" "my_bucket" {
  bucket = "my-terraform-bucket-${formatdate("YYYYMMDDhhmmss", timestamp())}"

  tags = {
    Name = "Terraform Test Bucket"
  }
}


## Then run:
terraform init
terraform plan
terraform apply
### Type yes to create the bucket.

https://registry.terraform.io/browse/modules

### Terrafoam install in linux
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl

curl -fsSL https://apt.releases.hashicorp.com/gpg | \
  sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
  sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt-get update
sudo apt-get install terraform -y

