# **Terraform AWS EC2 Setup - README**

## **General Setup Instructions**

This project sets up an **Ubuntu EC2 instance** using **Terraform** with the following configurations:
- Installs **Nginx** and **Nmap** via `cloud-init`
- Configures **SSH access** with a specified key pair
- Deploys the infrastructure in AWS

### **Prerequisites**
Ensure you have the following installed on your local machine:
- [Terraform](https://developer.hashicorp.com/terraform/downloads)
- AWS CLI (`awscli`)
- SSH client (for connecting to the instance)

### **Project Setup Steps**
1. **Clone the starter repository**:
   ```bash
   git clone https://gitlab.com/cit_4640/4640-w4-lab-start-w25.git
   cd 4640-w4-lab-start-w25
   ```
2. **Ensure AWS CLI is configured**:
   ```bash
   aws configure
   ```
   Provide your AWS **Access Key ID**, **Secret Access Key**, **Region**, and leave the output format as `json`.

3. **Ensure Terraform is installed and accessible**:
   ```bash
   terraform -v
   ```

4. **Generate a new SSH key pair for access** (if needed):
   ```bash
   ssh-keygen -t rsa -b 4096 -f web-key
   ```
   - This creates `web-key` (private key) and `web-key.pub` (public key).
   - **Important**: The **public key** must be placed in `cloud-config.yaml` under `ssh-authorized-keys`.

5. **Initialize Terraform**:
   ```bash
   terraform init
   ```
   - This downloads required **Terraform provider plugins**.

6. **Format the Terraform files (optional but recommended)**:
   ```bash
   terraform fmt
   ```
   - Ensures consistent Terraform syntax.

7. **Validate Terraform configuration**:
   ```bash
   terraform validate
   ```
   - Ensures that the configuration is correct.

8. **Plan the deployment**:
   ```bash
   terraform plan
   ```
   - Displays what Terraform will create before applying changes.

9. **Apply Terraform configuration to provision resources**:
   ```bash
   terraform apply -auto-approve
   ```
   - This creates the **VPC, security group, EC2 instance, and cloud-init configuration**.

10. **Retrieve the EC2 Public IP**:
   ```bash
   terraform output
   ```
   - Note down the public IP address of the created instance.

11. **SSH into the new instance**:
   ```bash
   ssh -i web-key web@<EC2_PUBLIC_IP>
   ```
   - Replace `<EC2_PUBLIC_IP>` with the actual instance public IP.

12. **Verify that Nginx and Nmap were installed via cloud-init**:
   ```bash
   nginx -v
   nmap --version
   ```
   - Both commands should return their installed versions.

13. **Access the Nginx Web Server**:
   - Open a browser and visit:
     ```
     http://<EC2_PUBLIC_IP>
     ```
   - You should see the **default Nginx welcome page**.

### **Destroying the Infrastructure**
When you're done, clean up the AWS resources by running:
```bash
terraform destroy -auto-approve
```
This will **delete all provisioned resources** to avoid unnecessary costs.

---
### **Summary**
This guide covered setting up an **AWS EC2 instance using Terraform**, including:
- **Creating an SSH key pair**
- **Configuring Terraform and cloud-init**
- **Provisioning an instance with Nginx and Nmap**
- **Connecting via SSH and testing Nginx**
- **Destroying resources when finished**

🚀 **Terraform has successfully deployed an AWS EC2 instance with automated setup!** 🎉

**contributors: Nastaran Zirak, Sina Abbasnia**
