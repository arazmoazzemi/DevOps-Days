## Install Bare Metal As A Service(MASS-3.4):

```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo snap install --channel=3.4 maas
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
```



```

virsh -c qemu+ssh://root@192.168.31.33/system list --all







maas login it http://192.168.31.34:5240/MAAS/api/2.0/ 
zJAwkVFnv286enznbE:22sJt9FyGdvXgMYQ6q:W7xCqdcuAPr4RQ2bu8J5Eq2vjsceFw9N



maas login it http://192.168.31.34:5240/MAAS/api/2.0/ zJAwkVFnv286enznbE:22sJt9FyGdvXgMYQ6q:W7xCqdcuAPr4RQ2bu8J5Eq2vjsceFw9N




maas it machines create \
    hostname=ubuntu \
    architecture=amd64 \
    mac_addresses=52:54:00:15:36:f2 \
    power_type=virsh \
    power_parameters_power_id=02d7f9cb-efae-4347-8b78-04d0f9e61fde3 \
    power_parameters_power_address=qemu+ssh://it@192.168.31.33/system \
    power_parameters_power_pass=xxxxxxxx
```










