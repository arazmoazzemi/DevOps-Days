 # Apache Guacamole manual-1.5.3:
 ----
- ___[Site](https://guacamole.apache.org/)___
- ___[Introduction](https://guacamole.apache.org/doc/gug/introduction.html#what-is-guacamole)___

----

- 1️⃣ **Installation with bitnami image for kvm host:**

- ___[Bitnami image download](https://bitnami.com/redirect/to/2348922/bitnami-guacamole-1.5.3-r0-debian-11-amd64.ova)___

Upload downloaded image on your kvm host, decompress downloaded file, and you will convert vmware vmdk file to qemu image, for example:
```
wget https://bitnami.com/redirect/to/2348922/bitnami-guacamole-1.5.3-r0-debian-11-amd64.ova
tar -xvf /bitnami-guacamole-1.5.3-r0-debian-11-amd64.ova
qemu-img convert -O qcow2 bitnami-guacamole-1.5.3-r0-debian-11-amd64.vmdk guacamole-1.5.3.qcow2

```


convert images:

----

- Bitnami enable ssh, for this image:
```bash
ssh-keygen -t rsa -b 2048

Debian
sudo rm -f /etc/ssh/sshd_not_to_be_run
sudo systemctl enable ssh
sudo systemctl start ssh

Ubuntu
sudo mv /etc/init/ssh.conf.back /etc/init/ssh.conf
sudo start ssh


Deactive ssh server

Debian
sudo systemctl stop ssh
sudo systemctl disable ssh


Ubuntu
sudo stop ssh
sudo mv /etc/init/ssh.conf /etc/init/ssh.conf.back

sudo systemctl restart ssh
```

```bash
wget https://github.com/Zer0CoolX/guacamole-customize-loginscreen-extension/raw/master/branding.jar 
/opt/bitnami/guacamole/extensions/
```

----

Bitnami permenet ip address:
```bash
sudo touch /etc/systemd/network/25-wired.network
sudo nano /etc/systemd/network/25-wired.network

[Match]
Name={INTERFACE-NAME} 

[Network]
Address={HOST-IP-ADDRESS}
Gateway={GATEWAY-IP-ADDRESS}

```


open portdisable firewall and openport
sudo which nft >/dev/null && echo nftables is enabled in this system || echo ufw is enabled in this system

- To stop nftables from doing anything, just drop all the rules:
```bash
nft flush ruleset
```

- To prevent nftables from starting at boot:
```bash
systemctl mask nftables.service
```

- To uninstall it and purge any traces of nftables in your system:
```bash
aptitude purge nftables
```

----

### [Docker Installation](https://guacamole.apache.org/doc/gug/guacamole-docker.html)


----

### [Proxying Guacamole](https://guacamole.apache.org/doc/gug/configuring-guacamole.html)


Two setp Varification













