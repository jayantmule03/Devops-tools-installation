
### **Steps to Install Ansible on Ubuntu**

1. **Update the package index**:
   ```bash
   sudo apt-get update
   ```

2. **Install required dependencies**:
   ```bash
   sudo apt-get install -y software-properties-common
   ```

3. **Add the Ansible PPA**:
   ```bash
   sudo add-apt-repository --yes --update ppa:ansible/ansible
   ```

4. **Update the package index again**:
   ```bash
   sudo apt-get update
   ```

5. **Install Ansible**:
   ```bash
   sudo apt-get install -y ansible
   ```

6. **Verify installation**:
   - Check the Ansible version:
     ```bash
     ansible --version
     ```

