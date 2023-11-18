## Install Bare Metal As A Service(MASS-3.3):

```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo snap install --channel=3.3 maas
sudo systemctl disable --now systemd-timesyncd
```


```bash
sudo apt install -y postgresql

Note! you will face a problem. if you want to use '@' sign for create db password:

```bash

$MAAS_DBUSER = maasuser
$MAAS_DBPASS = 123456
$MAAS_DBNAME = maasdb
$HOSTNAME = localhost

```

```bash
sudo -i -u postgres psql -c "CREATE USER \"maasuser\" WITH ENCRYPTED PASSWORD '123456'"
sudo -i -u postgres createdb -O "maasuser" "maasdb"


sudo maas init region+rack --database-uri "postgres://maasuser:123456@localhost/maasdb"
```


Create PostgreSQL user:
```bash
sudo -i -u postgres psql -c "CREATE USER \"$MAAS_DBUSER\" WITH ENCRYPTED PASSWORD '$MAAS_DBPASS'"
```


Create the MAAS database:
```bash
sudo -i -u postgres createdb -O "$MAAS_DBUSER" "$MAAS_DBNAME"
sudo maas init region+rack --database-uri "postgres://$MAAS_DBUSER:$MAAS_DBPASS@$HOSTNAME/$MAAS_DBNAME"
```

```bash
sudo maas status
sudo maas createadmin

# sudo maas init region

#sudo maas configauth

#sudo maas createadmin

#sudo maas config-tls enable
```







