

#### [Link](https://github.com/netbox-community/netbox-docker)

```bash
git clone https://github.com/netbox-community/netbox-docker.git
```

```bash
cd netbox-docker
```

```bash

touch docker-compose.override.yml

version: '3.6.5'
services:
  netbox:
    ports:
    - 8000:8080

```
```bash

docker compose pull

docker compose up
```



# To create the first admin user run this command:
docker compose exec netbox /opt/netbox/netbox/manage.py createsuperuser



docker compose exec netbox /opt/netbox/netbox/manage.py createsuperuser
