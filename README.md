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

## Install eksctl:
choco install eksctl
## (Requires Chocolatey package manager.)

## Verify:
eksctl version

## 4️⃣ Create a Kubernetes Cluster in AWS
## Example (2 nodes, t3.micro):
eksctl create cluster --name my-cluster --region ap-south-1 --nodes 2 --node-type t3.micro
## This will:
## Create the EKS cluster
## Configure kubectl automatically

## 5️⃣ Test the Cluster
kubectl get nodes
kubectl get pods --all-namespaces
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

resource "aws_s3_bucket" "test_bucket" {
  bucket = "my-terraform-test-bucket-12345"
  acl    = "private"
}


## Then run:
terraform init
terraform plan
terraform apply
### Type yes to create the bucket.
