# Prerequisites
## Install docker engine:
# Update existing list of packages
```sudo apt update```

# install a prerequisite packages 
```sudo apt install apt-transport-https ca-certificates curl software-properties-common```

# add the GPG key for the official Docker repository
```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -```

# Add the Docker repository to APT sources
```sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"```

# Make sure you are about to install from the Docker repo instead of the default Ubuntu repo
```apt-cache policy docker-ce```

# Install Docker
```sudo apt install docker-ce```

# Check that it’s running:
```sudo systemctl status docker```

## Executing the Docker Command Without Sudo
# add your username to the docker group
```sudo usermod -aG docker ${USER}```

# log out of the server and back
```su - ${USER}```

# add user to group:
```sudo usermod -aG docker ${USER}```


## How To Install and Use Docker Compose on Ubuntu 22.04
# Download:
```mkdir -p ~/.docker/cli-plugins/
   curl -SL https://github.com/docker/compose/releases/download/v2.3.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
```

# Set permissions
```chmod +x ~/.docker/cli-plugins/docker-compose```

# Check version
```docker compose version```



# ansible-docker-playground
A simple 3 containers ansible playground
![project image](https://i.imgur.com/jwf0hv9.png)

This repository contains a minimal set of files in order to quickly setup an environment for learning and experimenting with Ansible. 
You can use the `docker-compose.yml` file to tweak the infrastructure to your needs.

Start the containers by running the following snippet in your terminal :

```bash
git clone https://github.com/ido83/ansible-docker-playground
cd ansible-docker-playground
docker compose build # Build the containers
docker compose up -d # Start the containers
```
The containers ansible, web and db are now running the background

⚠ In a second terminal, run this second snippet to access the ansible-enabled container (named as "ansible" within the network) 

```bash docker exec -it ansible-docker-playground_ansible_1 /bin/bash```

Then you can try to ssh into the others containers (such as web or db) with the following snippets

```bash ssh web```

You can add/modify playbooks inside the shared-folder of this repository, it's a volume that's mounted at /shared-folder in the ansible container. This folder should be your workplace, place your inventory, templates etc in it and run your playbooks from it.
```bash
   cd /shared-folder
   ansible-playbook playbook.yml -i inventory.ini
```

---

If you do any change to the Dockerfiles, don't forget to build the containers again
```bash docker compose build```
