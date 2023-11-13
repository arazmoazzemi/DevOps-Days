### Redis Help

- docker
```cmd
docker run -d --name redis redis
docker exec -it redis bash
```

- connect to database:
```bash
redis-cli
```
#### partitioning is the way for increase database speed and performance

---

- check Redis connectivity
```bash
PING 
```
---

- data store for key value:
SET
```bash
set test devops
get test

set x 10
get x
```

---

Increament:
INCR
```bash
incr x
```
---

- Decrement:
DECR
```bash
decr x
```

---

- find:
EXISTS
```bash
exists test
```

---

- delete:
del 
```cmd
del test
```

---

- override:
```bash
set test devops
get test

set test redis
get test
```

---

- Moniter(watch):
#### we need two terminal for run his this commands:
```bash
get test devops
get test
```

---


- KEYS:
Show all keys:
```bash
keys *

set name1 john 
set name2 araz
set name3 rosa

keys name*
```

---

FLUSH
Note! In redis exists 16 databese [0-15] and Default databese is 0 (Sharding redis databse in one instance)

Example:
```bash
select 1
keys *
#(empty array)

select 0 keys *

flushdb
Delete running database

Flushdb 01-Exampe:

select 15
set h 10
keys *

flushdb 

keys *
select 0
keys *

Databese 0 is exist, Just database 15 is deleted
```

```bash
flushall
Delete all of databases

select 2
set x 10
set y 20
keys *

flush all

select 0
keys *

#Also

select 15
keys *

All pf databases are deleted
(empty array)

```
---
# S02
---

Redis SDK
https://redis.io/resources/clients/

Docs:

https://redis.readthedocs.io/en/stable/commands.html


docker run -d --name redis redis
docker start redis

# docker run -p 6379:6379 -it redis/redis-stack:latest

docker exec -it redis bash
redis-cli

```cmd
python -m venv venv
cd venv\Scripts
activate.bat
```


pip install redis


docker start redis
docker exec -it redis bash

redis-cli

```python
from redis import Redis
redis = Redis()

redis.ping()
```

Connect to redis(docker)
show ip address:
```cmd
docker inspect redis

#   "IPAddress": "172.17.0.2"
```

```
# get redis ip from docker
docker inspect redis

---test connection:

rom redis import Redis
from redis.exceptions import ClusterError

redis = Redis(host="172.17.0.2")
try:
    redis.ping()
    print("Connected")
except ConnectionError:
    print("ConnectionError!")


----------decode_responses---------------

redis-cli

SET test devops

redis = Redis(host="172.17.0.2", decode_responses=True)
try:
    redis.ping()
#    print("Connected")
except ConnectionError:
    print("ConnectionError!")

x = redis.get("test")

print(x)

```
---

OR

---
rom redis import Redis
from redis.exceptions import ClusterError

redis = Redis(host="172.17.0.2", decode_responses=False)
try:
    redis.ping()
#    print("Connected")
except ConnectionError:
    print("ConnectionError!")

x = redis.get("test")

print(x.decode('ascii'))






























