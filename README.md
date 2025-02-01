
# Terraform AWS Lab - Week 4

This repository contains the Terraform configuration for provisioning an AWS EC2 instance with a cloud-init configuration. The lab involves using Terraform to create a VPC, subnet, security group, internet gateway, and an EC2 instance with a user-defined key pair.

---

## **📌 General Setup Instructions**
### **1️⃣ Prerequisites**
Before starting, ensure you have the following installed on your Linux environment:
- **Terraform** (Install instructions below)
- **AWS CLI** (Optional, but useful for debugging)
- **Git** (For version control)
- An **AWS account** with access to EC2

### **2️⃣ Install Terraform**
On **Ubuntu/Debian**, run:
```bash
sudo apt update && sudo apt install -y gnupg software-properties-common
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
```
Verify the installation:
```bash
terraform -version
```

---

## **📌 SSH Key Pair Creation**
Before applying Terraform, create an SSH key pair to allow secure access to the instance.

```bash
ssh-keygen -t rsa -b 2048 -f ~/.ssh/terraform-key
```
This will generate:
- **Private key**: `~/.ssh/terraform-key`
- **Public key**: `~/.ssh/terraform-key.pub`

Manually **import the public key** into AWS:
```yaml
1. **Go to AWS Console → EC2 → Key Pairs**.
2. Click **"Create Key Pair"**.
3. Choose **"Import Key Pair"**.
4. **Paste the contents of `~/.ssh/terraform-key.pub`**.
5. Click **Create Key Pair**.
```

---

## **📌 Terraform Setup & Execution**
### **1️⃣ Clone the Repository**
```bash
git clone <repository-url>
cd <repository-folder>
```

### **2️⃣ Initialize Terraform**
Run the following to **initialize Terraform**:
```bash
terraform init
```

### **3️⃣ Format and Validate Terraform Configuration**
```bash
terraform fmt
terraform validate
```

### **4️⃣ Plan Terraform Deployment**
```bash
terraform plan -out plan.tfplan
```

### **5️⃣ Apply the Terraform Plan**
```bash
terraform apply plan.tfplan
```
Confirm by typing **`yes`** when prompted.

### **6️⃣ Get the Public IP of the Instance**
```bash
terraform output
```

---

## **📌 Connect to the AWS EC2 Instance**
Once the instance is created, use SSH to connect:

```bash
ssh -i ~/.ssh/terraform-key ubuntu@<PUBLIC_IP>
```
If `ubuntu` doesn’t work, try:
```bash
ssh -i ~/.ssh/terraform-key ec2-user@<PUBLIC_IP>
```

---

## **📌 Destroy the Infrastructure**
To delete all resources:
```bash
terraform destroy
```
Confirm by typing **`yes`**.

---

## **📌 Repository Structure**
```yaml
.
├── README.md             # This file
├── main.tf               # Terraform configuration
├── cloud-config.yaml     # Cloud-init configuration for EC2 setup
├── .gitignore            # Ignore unnecessary files
```

