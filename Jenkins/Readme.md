
### **Steps to Install Jenkins on Ubuntu**

1. **Update the package index**:
   ```bash
   sudo apt-get update
   ```

2. **Install Java (Jenkins requires Java)**:
   - Jenkins works with OpenJDK 11 or 17. Install OpenJDK 17:
     ```bash
     sudo apt-get install -y openjdk-17-jre
     ```
   - Verify Java installation:
     ```bash
     java -version
     ```

3. **Add the Jenkins repository key**:
   ```bash
   curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
   ```

4. **Add the Jenkins repository**:
   ```bash
   echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
   ```

5. **Update the package index again**:
   ```bash
   sudo apt-get update
   ```

6. **Install Jenkins**:
   ```bash
   sudo apt-get install -y jenkins
   ```

7. **Start and enable Jenkins**:
   - Start the Jenkins service:
     ```bash
     sudo systemctl start jenkins
     ```
   - Enable Jenkins to start on boot:
     ```bash
     sudo systemctl enable jenkins
     ```

8. **Verify Jenkins is running**:
   ```bash
   sudo systemctl status jenkins
   ```
   - Look for "active (running)" in the output. Press `Ctrl+C` to exit.

9. **Access Jenkins**:
   - Open a browser and go to `http://your_server_ip_or_localhost:8080`.
   - Get the initial admin password:
     ```bash
     sudo cat /var/lib/jenkins/secrets/initialAdminPassword
     ```
   - Copy the password, paste it into the Jenkins web interface, and follow the setup wizard to complete installation (install suggested plugins and create an admin user).


