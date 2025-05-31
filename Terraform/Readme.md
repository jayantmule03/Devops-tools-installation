### **Steps to Install Terraform on Ubuntu**

1. **Update the package index**:
   ```bash
   sudo apt-get update
   ```

2. **Install required dependencies**:
   ```bash
   sudo apt-get install -y gnupg software-properties-common curl
   ```

3. **Add HashiCorp’s GPG key**:
   ```bash
   curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
   ```

4. **Add the HashiCorp repository**:
   ```bash
   echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
   ```

5. **Update the package index again**:
   ```bash
   sudo apt-get update
   ```

6. **Install Terraform**:
   ```bash
   sudo apt-get install -y terraform
   ```

7. **Verify installation**:
   - Check the Terraform version:
     ```bash
     terraform -version
     ```
   - You should see output like `Terraform v1.9.x` (or the latest version as of May 31, 2025).

### **Basic Setup and Test**
1. **Initialize a Terraform project**:
   - Create a directory for your Terraform configuration:
     ```bash
     mkdir ~/terraform-project && cd ~/terraform-project
     ```
   - Create a sample `main.tf` file:
     ```bash
     echo 'output "hello" { value = "Hello, Terraform!" }' > main.tf
     ```
   - Initialize Terraform:
     ```bash
     terraform init
     ```
   - Apply the configuration to test:
     ```bash
     terraform apply
     ```
   - You should see the output: `hello = "Hello, Terraform!"`.

2. **(Optional) Configure Terraform for a cloud provider**:
   - To use Terraform with AWS, GCP, Azure, etc., install the provider’s CLI (e.g., `aws-cli` for AWS) and configure credentials.
   - Example for AWS:
     ```bash
     sudo apt-get install -y awscli
     aws configure
     ```
     Enter your AWS Access Key, Secret Key, region, and output format.
   - Add provider details to `main.tf` (e.g., for AWS):
     ```hcl
     provider "aws" {
       region = "us-east-1"
     }
     ```
