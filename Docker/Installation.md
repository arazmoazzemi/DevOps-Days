# Docker Installation

Install Docker Engine on Ubuntu
- Add Docker's official GPG key:

```bash
sudo apt-get update
sudo mkdir -p /etc/apt/keyrings
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor --yes -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
- Add the repository to Apt sources:
```bash
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
```

Install docker engine
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Uninstall Docker Engine

sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras


-----------------------------------------

sudo groupadd docker

sudo usermod -aG docker $USER


# logout and back in or reboot your virtual machine



-----------------------------------------

nano ~/my_password.txt

cat ~/my_password.txt | docker login --username arazcode --password-stdin

OR

docker login -u arazcode -p danial123




-----------------------------------------

# Get images
docker pull nginx

# Run container
deattach and run in background
docker run -d nginx

# show docker images
docker ps
docker ps -a

# stop container

docker stop {CONTAINER ID} or {NAMES}
docker stop ac6c83fcfd73
docker stop zealous_bardeen

# Start container

docker start {CONTAINER ID} or {NAMES}
docker start ac6c83fcfd73
docker start zealous_bardeen








-----------------------------------------




sudo docker run hello-world

docker ps -a
docker images



sudo service docker start
sudo docker run hello-world





-------------------------------

