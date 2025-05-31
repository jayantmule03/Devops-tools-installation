##  Install Docker on Ubuntu

To install Docker Engine  on Ubuntu, follow these step-by-step instructions. This method works for  newer versions. The process involves setting up Docker's official repository, installing Docker, and verifying your installation.

**1. Update Your System**

Make sure your package list and installed packages are up to date:

```bash
sudo apt update && sudo apt upgrade -y
```


**2. Uninstall Old Versions (Optional)**

Remove any older Docker versions if present:

```bash
sudo apt remove docker docker-engine docker.io containerd runc
```


**3. Install Prerequisite Packages**

Install dependencies required for Docker's installation:

```bash
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```


**4. Add Docker’s Official GPG Key**

Import Docker’s GPG key to verify package authenticity:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```


**5. Add Docker’s Official Repository**

Add Docker’s repository to your APT sources:

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```


**6. Install Docker Engine**

Update your package list and install Docker:

```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
```


**7. Start and Enable Docker**

Ensure Docker starts now and on boot:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```


**8. (Optional) Run Docker Without Sudo**

Add your user to the Docker group to run Docker commands without `sudo`:

```bash
sudo usermod -aG docker $USER
```
Log out and log back in for this to take effect[6][4].

**9. Verify Docker Installation**

Check that Docker is installed and running:

```bash
docker --version
```


You can also run a test container:

```bash
docker run hello-world
```


---

