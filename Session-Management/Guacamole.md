 # Apache Guacamole manual:
 
[Site](https://guacamole.apache.org/)
:
[Introduction](https://guacamole.apache.org/doc/gug/introduction.html#what-is-guacamole)

----

1️⃣ Installation with bitnami image for kvm host:

[Bitnami image download](https://bitnami.com/redirect/to/2348922/bitnami-guacamole-1.5.3-r0-debian-11-amd64.ova)









Bitnami enable ssh

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

wget https://github.com/Zer0CoolX/guacamole-customize-loginscreen-extension/raw/master/branding.jar 
/opt/bitnami/guacamole/extensions/


---------------open port----------disable firewall-----------------------
sudo which nft >/dev/null && echo nftables is enabled in this system || echo ufw is enabled in this system

# To stop nftables from doing anything, just drop all the rules:
nft flush ruleset

# To prevent nftables from starting at boot:
systemctl mask nftables.service

# To uninstall it and purge any traces of nftables in your system:
aptitude purge nftables


Docker Installation:

https://guacamole.apache.org/doc/gug/guacamole-docker.html



Proxying Guacamole
https://guacamole.apache.org/doc/gug/configuring-guacamole.html















