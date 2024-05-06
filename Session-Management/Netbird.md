Netbird

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \

  tee /etc/apt/sources.list.d/docker.list > /dev/null
apt-get update


apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin








------------------------------------
https://github.com/netbirdio/netbird

apt install jq


export NETBIRD_DOMAIN=netbird.mylab.loc; curl -fsSL https://github.com/netbirdio/netbird/releases/latest/download/getting-started-with-zitadel.sh | bash


-----------------------------------



https://app.netbird.io/install

docker run --rm -d \
 --cap-add=NET_ADMIN \
 -e NB_SETUP_KEY=SETUP_KEY \
 -v netbird-client:/etc/netbird \
 netbirdio/netbird:latest




https://docs.netbird.io/how-to/getting-started#running-net-bird-in-docker
```
