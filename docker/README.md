# Install and Use Docker and Docker Compose on Ubuntu 22.04

This guide will walk you through the installation and configuration of Docker on Ubuntu 22.04.

## Installing Docker

Docker is available in the default Ubuntu repositories. To install it, you need to add the official Docker repository to your system’s sources list. You can do this by typing:

1. Update the apt package index and install packages to allow apt to use a repository over HTTPS:

```bash
 sudo apt-get update
 sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

2. Add Docker’s official GPG key:

```bash
 sudo mkdir -p /etc/apt/keyrings
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

3. Use the following command to set up the repository:

```bash
 echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

4. Update the apt package index, and install the latest version of Docker Engine and containerd:

```bash
 sudo apt-get update
 sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin docker-compose
```

5. Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running:

```bash
  sudo systemctl status docker
```
