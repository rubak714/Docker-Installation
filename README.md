# Docker-Installation

#### Docker Installation Guide for Ubuntu Virtual Machine

## Simplified Docker Installation

This is an easier and faster method for beginners to install Docker using Ubuntu's default package manager.

---

## Step-by-Step: Easy Docker Installation

### Step 1: Update System

```bash
sudo apt update
sudo apt upgrade -y
```

### Step 2: Install Docker (Community Version)

```bash
sudo apt install docker.io -y
```

This installs:

* Docker Engine (docker service)
* Docker CLI (command-line interface)

### Step 3: Enable and Start Docker Service

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

* `enable`: Ensures Docker starts at boot
* `start`: Launches the Docker service now

### Step 4: Check Docker Version

```bash
docker --version
```

### Step 5: Test Docker

```bash
sudo docker run hello-world
```

This downloads a test container and prints a success message if Docker is working.

### (Optional) Step 6: Use Docker Without sudo

```bash
sudo usermod -aG docker $USER
newgrp docker
```

Now you can just type `docker` instead of `sudo docker`.

---

## Summary

| Task           | Command                         |
| -------------- | ------------------------------- |
| Install Docker | `sudo apt install docker.io -y` |
| Start Docker   | `sudo systemctl start docker`   |
| Enable on Boot | `sudo systemctl enable docker`  |
| Test Install   | `docker run hello-world`        |

This method is simple and quick for Ubuntu users who don’t need the latest Docker version. For advanced features, use the full installation method with Docker’s official repo.


# Full-Docker Installation

### Step 1: Update your system

```bash
sudo apt update
sudo apt upgrade -y
```
apt update: Refreshes the list of available packages and versions.
apt upgrade -y: Installs the latest versions of installed packages.

### Step 2: Install required packages

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```
These packages allow your system to securely fetch Docker from an HTTPS source:

apt-transport-https: Enables APT to use HTTPS.
ca-certificates: Ensures secure server communications.
curl: For downloading Docker’s GPG key.
software-properties-common: Adds tools to manage software sources.

### Step 3: Add Docker’s GPG key

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
Downloads Docker’s public GPG key (curl -fsSL).
Converts it into a trusted format for APT (gpg --dearmor).

### Step 4: Add the Docker repository

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Adds Docker’s stable software source for your specific Ubuntu version (e.g., jammy, focal).
Uses the GPG key added earlier for secure verification.

### Step 5: Install Docker Engine

```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
```
docker-ce: Community Edition of Docker Engine.
docker-ce-cli: Command-line interface.
containerd.io: Runtime backend Docker relies on.

### Step 6: Check Docker installation

```bash
docker --version
```

You should see output like: `Docker version 20.10.x, build xxxx`

### Step 7: Run Docker without sudo (Optional but Recommended)

```bash
sudo usermod -aG docker $USER
newgrp docker
```
Adds user to the docker group so you don’t need sudo every time.
newgrp docker: applies group membership changes instantly.

Then try:

```bash
docker run hello-world
```

If you see a welcome message from Docker, everything is working!

---

You're now ready to install Jenkins using Docker or run any containerized application.
