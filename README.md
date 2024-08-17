# Docker Installation on Ubuntu

## Step 1: Install Vim (Optional)

Update your package list and install Vim:

```bash
sudo apt update
sudo apt install vim -y
```

## Step 2: Create the `install.sh` Script

Create a file named `install.sh` and insert the following code:

```bash
#!/bin/bash

# Update package database and upgrade existing packages
sudo apt update && sudo apt upgrade -y

# Install required packages
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common

# Add Docker’s official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Add Docker APT repository
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker
sudo apt update && sudo apt install -y docker-ce

# Add current user to Docker group and set Docker socket permissions
sudo usermod -aG docker ${USER} && sudo chmod 666 /var/run/docker.sock

# Verify Docker installation
docker --version
```

## Step 3: Make the Script Executable

Make your script executable:

```bash
chmod +x install.sh
```

## Step 4: Run the Script

Execute the script to install Docker:

```bash
./install.sh
```

## Step 5: Open a New Terminal

To use Docker without root permissions, open a new terminal or continue using the current one with root permissions.
