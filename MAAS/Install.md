## Install Bare Metal As A Service(MASS-3.3):

```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo snap install --channel=3.3 maas
sudo systemctl disable --now systemd-timesyncd
```

### Install postgresql
```bash
sudo apt install -y postgresql
```

#### Note! you will face a problem. if you want to use '@' sign for create db password:

```bash
MAAS_DBUSER=maasuser
MAAS_DBPASS=123456
MAAS_DBNAME=maasdb
HOSTNAME=localhost

```

Create PostgreSQL user and Create the MAAS database::

```bash
sudo -i -u postgres psql -c "CREATE USER \"maasuser\" WITH ENCRYPTED PASSWORD '123456'"
sudo -i -u postgres createdb -O "maasuser" "maasdb"
```

### MASS init
```
sudo maas init region+rack --database-uri "postgres://maasuser:123456@localhost/maasdb"
```


```bash
sudo maas status
sudo maas createadmin

# sudo maas init region

#sudo maas configauth

#sudo maas createadmin

#sudo maas config-tls enable
```

---

### Install with APT:

```
sudo apt-get update && sudo apt-get upgrade -y

sudo apt-add-repository ppa:maas/3.4

sudo apt install maas -y

sudo maas init

```

---

### KVM

### Power parameters for KVM in MaaS CLI 

```
https://maas.cloud.cbh.kth.se/MAAS/docs/cli/power-management-reference.html
https://ubuntu-on-big-iron.blogspot.com/2019/08/maas-kvm-on-s390x-part1.html
```



```
virsh -c qemu+ssh://root@192.168.31.33/system list --all

maas login <maas_user> http://192.168.31.34:5240/MAAS/api/2.0/ <api_key>
maas login it http://192.168.31.34:5240/MAAS/api/2.0/ V6R34MrmuTY2aTffAj:N9CuHV4X6PbNZkP8NQ:La3ZzMu27dcG2bmxUdUtgbnK5D5YZYfU


maas it machines create \
    hostname=ubuntu \
    architecture=amd64 \
    mac_addresses=52:54:00:15:36:f2 \
    power_type=virsh \
    power_parameters_power_id=02d7f9cb-efae-4347-8b78-04d0f9e61fde3 \
    power_parameters_power_address=qemu+ssh://it@192.168.31.33/system \
    power_parameters_power_pass=******
```


Proxmox power type example:
```
Power type
Proxmox

Proxmox host name or IP
192.168.200.10

Proxmox username, including realm
root@pam

Proxmox password, required if a token name and secret aren't given
*******

Proxmox API token name
—

Proxmox API token secret
—

# VM name on proxmox
Node ID
node02

Verify SSL connections with system CA certificates
No

```

----
# Test section for install maas 3.3 stable instead of 3.4 and bug fix it for virsh host:

```

sudo chsh -s /bin/bash maas  
sudo su - maas  
ssh-keygen -f ~/.ssh/id_rsa -N ''  
logout  
sudo cat ~maas/.ssh/id_rsa.pub | tee -a ~/.ssh/authorized_keys
With the keys in place, let’s test our connection to the local hypervisor:

sudo -H -u maas \
    bash -c 'virsh -c qemu+ssh://ubuntu@192.168.30.1/system list --all'




# If you installed MAAS via snap, then create the needed SSH keys this way:

Set up libvirt SSH (3.3,3.4 snap)

sudo mkdir -p /var/snap/maas/current/root/.ssh
cd /var/snap/maas/current/root/.ssh
sudo ssh-keygen -f id_rsa



nano /etc/libvirt/libvirtd.conf


unix_sock_group = "libvirt"
unix_sock_rw_perms = "0770"
auth_unix_rw = "none"


sudo nano /etc/libvirt/qemu.conf
user = "oneadmin"
group = "kvm"

sudo systemctl restart libvirtd




sudo -H -u maas \
bash -c 'virsh -c qemu+ssh://it@192.168.200.15/system list --all'




sudo maas it machines create \
    hostname=ubuntu \
    architecture=amd64 \
    mac_addresses=52:54:00:b1:b6:bd \
    power_type=virsh \
    power_parameters_power_id=2ff77996-e092-4bff-a2ac-15890d0167db \
    power_parameters_power_address=qemu+ssh://it@192.168.200.15/system 
    

https://discourse.maas.io/t/maas-virsh-power-type-power-error/7913/2
sudo snap refresh --channel=3.3/stable/hotfix-bug-2053033 maas

```
----
```
Set an ip address for bridge network

https://maas.io/docs/managing-vm-hosts


Set up libvirt SSH (3.3,3.4 snap)
If you installed MAAS via snap, then create the needed SSH keys this way:



sudo mkdir -p /var/snap/maas/current/root/.ssh
cd /var/snap/maas/current/root/.ssh
sudo ssh-keygen -f id_rsa

sudo nano /etc/libvirt/qemu.conf
user = "it"
group = "kvm"
```


----

# OK -------------------->>> YOU just bug fix
```
[[Set up libvirt SSH (3.3,3.4 snap)

sudo mkdir -p /var/snap/maas/current/root/.ssh
cd /var/snap/maas/current/root/.ssh
sudo ssh-keygen -f id_rsa
sudo cat /var/snap/maas/current/root/.ssh/id_rsa.pub | tee -a ~/.ssh/authorized_keys



maas login it http://192.168.200.15:5240/MAAS/api/2.0/ cwuEJsZAbxbvMxwMxH:fYfL37gcrtEnNRNPMM:NtNWzr55ND5Ay2DdDUrM8LCvf9kW72HK



ssh-copyid it@192.168.200.15
virsh -c qemu+ssh://it@192.168.200.15/system list --all'






sudo maas it machines create \
    hostname=ubuntu \
    architecture=amd64 \
    mac_addresses=52:54:00:c5:d4:86 \
    power_type=virsh \
    power_parameters_power_id=91d1cc78-7bd5-4f83-b84c-db8cec522080 \
    power_parameters_power_address=qemu+ssh://it@192.168.200.15/system ](https://discourse.maas.io/t/maas-virsh-power-type-power-error/7913/2
sudo snap refresh --channel=3.3/stable/hotfix-bug-2053033 maas


API key:
cwuEJsZAbxbvMxwMxH:fYfL37gcrtEnNRNPMM:NtNWzr55ND5Ay2DdDUrM8LCvf9kW72HK

maas login it http://192.168.200.15:5240/MAAS/api/2.0/ cwuEJsZAbxbvMxwMxH:fYfL37gcrtEnNRNPMM:NtNWzr55ND5Ay2DdDUrM8LCvf9kW72HK


sudo mkdir -p /var/snap/maas/current/root/.ssh
cd /var/snap/maas/current/root/.ssh
sudo ssh-keygen -f id_rsa
sudo cat /var/snap/maas/current/root/.ssh/id_rsa.pub | tee -a ~/.ssh/authorized_keys



maas it machines create \
    hostname=ubuntu \
    architecture=amd64 \
    mac_addresses=52:54:00:be:09:15 \
    power_type=virsh \
    power_parameters_power_id=54dc45aa-1a1a-409a-947d-c587e3496f99 \
    power_parameters_power_address=qemu+ssh://it@192.168.200.15/system )](https://discourse.maas.io/t/maas-virsh-power-type-power-error/7913/2
sudo snap refresh --channel=3.3/stable/hotfix-bug-2053033 maas


API key:
cwuEJsZAbxbvMxwMxH:fYfL37gcrtEnNRNPMM:NtNWzr55ND5Ay2DdDUrM8LCvf9kW72HK

maas login it http://192.168.200.15:5240/MAAS/api/2.0/ cwuEJsZAbxbvMxwMxH:fYfL37gcrtEnNRNPMM:NtNWzr55ND5Ay2DdDUrM8LCvf9kW72HK


sudo mkdir -p /var/snap/maas/current/root/.ssh
cd /var/snap/maas/current/root/.ssh
sudo ssh-keygen -f id_rsa
sudo cat /var/snap/maas/current/root/.ssh/id_rsa.pub | tee -a ~/.ssh/authorized_keys



maas it machines create \
    hostname=ubuntu \
    architecture=amd64 \
    mac_addresses=52:54:00:be:09:15 \
    power_type=virsh \
    power_parameters_power_id=54dc45aa-1a1a-409a-947d-c587e3496f99 \
    power_parameters_power_address=qemu+ssh://it@192.168.200.15/system )
```


# Network defination example:
```
network:
  version: 2
  ethernets:
    ens32:
      addresses:
      - 192.168.200.15/24
      nameservers:
        addresses:
        - 8.8.8.8
        search: []
      routes:
      - to: default
        via: 192.168.200.2
    ens33:
      optional:
        true
      dhcp4: false
      dhcp6: false

  bridges:
    virbr0:
      interfaces:
        - ens33
      addresses:
      - 192.168.100.1/24  # Adjust the IP address and subnet as needed

```

### Network define
```bash
brct addbr virbr0

cd /etc/libvirt/qemu/networks
touch virbr0.xml


nano /etc/libvirt/qemu/networks/vmbr0.xml

<network>
  <name>virbr0</name>
  <forward mode="bridge"/>
  <bridge name="virbr0" />
</network>

virsh net-define --validate --file virbr0.xml
virsh net-start --network virbr0
virsh net-autostart --network virbr0

```
