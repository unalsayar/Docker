# Install Docker Engine on Ubuntu

## Uninstall old versions

Older versions of Docker went by the names of docker, docker.io, or docker-engine. Uninstall any such older versions before attempting to install a new version:

sudo apt-get remove docker docker-engine docker.io containerd runc


## Install using the repository

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.


### Set up the repository

1. Update the apt package index and install packages to allow apt to use a repository over HTTPS:

 sudo apt-get update
 
 sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release



2. Add Docker’s official GPG key:

 sudo mkdir -p /etc/apt/keyrings
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg



3. Use the following command to set up the repository:

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null



## Install Docker Engine

1. Update the apt package index:

sudo apt-get update



2. Install Docker Engine, containerd, and Docker Compose.

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin



3. Verify that the Docker Engine installation is successful by running the "hello-world" image:

sudo docker run hello-world



This command downloads a test image and runs it in a container. When the container runs, it prints a confirmation message and exits.

You have now successfully installed and started Docker Engine. The docker user group exists but contains no users, which is why you’re required to use sudo to run Docker commands.



## Docker Engine post-installation steps

These optional post-installation procedures shows you how to configure your Linux host machine to work better with Docker.


### Manage Docker as a non-root user

If you don’t want to preface the docker command with sudo, create a Unix group called docker and add users to it. When the Docker daemon starts, it creates a Unix socket accessible by members of the docker group. On some Linux distributions, the system automatically creates this group when installing Docker Engine using a package manager. In that case, there is no need for you to manually create the group.


1. Create the docker group.

sudo groupadd docker


2. Add your user to the docker group.

sudo usermod -aG docker $USER


3. Log out and log back in so that your group membership is re-evaluated.
    You can also run the following command to activate the changes to groups:

newgrp docker


4. Verify that you can run docker commands without sudo.

docker run hello-world


## Configure Docker to start on boot with systemd

Many modern Linux distributions use systemd to manage which services start when the system boots. On Debian and Ubuntu, the Docker service starts on boot by default. To automatically start Docker and containerd on boot for other Linux distributions using systemd, run the following commands:

sudo systemctl enable docker.service
sudo systemctl enable containerd.service


WARNING: To stop this behavior, use disable instead.

sudo systemctl disable docker.service
sudo systemctl disable containerd.service


===================================================

https://docs.docker.com/engine/install/ubuntu/
