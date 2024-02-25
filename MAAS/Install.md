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

sudo apt install maas

sudo maas init

```












