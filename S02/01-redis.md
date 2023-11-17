### Redis Help(DevOps days)

- docker:

```bash
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
```bash
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

For example:
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
---
# S02
---
---

Redis SDK
https://redis.io/resources/clients/

Docs:

https://redis.readthedocs.io/en/stable/commands.html

```bash
docker run -d --name redis redis
docker start redis

# docker run -p 6379:6379 -d --name rdis redis

docker exec -it redis bash
redis-cli
```
---

Create a python envoiroment for test application:

```bash
sudo apt install python3-venv -y
python3 -m venv venv
cd /venv/bin
source activate
```

---

```python
pip install redis
```

```bash
docker start redis
docker exec -it redis bash

redis-cli
```

```python
from redis import Redis
redis = Redis()

redis.ping()
```

#### connect to redis(docker)
- #### show ip address:
```bash
docker inspect redis

# "IPAddress": "172.17.0.2"
```

#### connection test:

```python
from redis import Redis
from redis.exceptions import ConnectionError

redis = Redis(host="172.17.0.2")
try:
    redis.ping()
    print("Connected")
except ConnectionError:
    print("ConnectionError!")
```

- #### decode_responses:

```bash
redis-cli

SET test devops
```
```pythoh
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

- ##### print binary to sting:

```python
from redis import Redis
from redis.exceptions import ConnectionError

redis = Redis(host="172.17.0.2", decode_responses=False)
try:
    redis.ping()
#    print("Connected")
except ConnectionError:
    print("ConnectionError!")

x = redis.get("test")

print(x.decode('ascii'))
```
---

```python
from redis import Redis
from redis.exceptions import ConnectionError
from time import sleep

redis = Redis(host="172.17.0.2", decode_responses=True)
try:
    redis.ping()
except ConnectionError:
    print("ConnectionError!")
else:
    print("ok")
sleep(15)

try:
    redis.ping()
except ConnectionError:
    print("ConnectionError!")
else:
    print("ok")

x = redis.get("test")
print(x)
```

---


- #### ExponentialBackoff for retry connection:

```python
from redis import Redis
from redis.exceptions import ConnectionError
from time import sleep
from redis.backoff import ExponentialBackoff
from redis.retry import Retry

retry = Retry(ExponentialBackoff(), 3)
redis = Redis(host="172.17.0.2", decode_responses=True, retry=retry)

try:
    redis.ping()
except ConnectionError:
    print("ConnectionError!")
else:
    print("ok")
sleep(5)

try:
    redis.ping()
except ConnectionError:
    print("ConnectionError!")
else:
    print("ok")
sleep(5)
```

---
- #### (write to app.py1):

```python
from redis import Redis
from redis.exceptions import ConnectionError
from time import sleep
from redis.backoff import ExponentialBackoff
from redis.retry import Retry


redis = Redis(host="172.17.0.2", decode_responses=True)

try:
    redis.ping()
except ConnectionError:
    print("ConnectionError!")
else:
    print("ok")

redis.set("test", "devops")
```
### app2 get from app1.py
```
from redis import Redis
from redis.exceptions import ConnectionError
from time import sleep
from redis.backoff import ExponentialBackoff
from redis.retry import Retry


redis = Redis(host="172.17.0.2", decode_responses=True)

try:
    redis.ping()
except ConnectionError:
    print("ConnectionError!")
else:
    print("ok")

test = redis.get("test")
print(test)

```
```

### While until input vlaue:(run app1.py after app2.py)

First---run app2.py

from redis import Redis
from redis.exceptions import ConnectionError

redis = Redis(host="172.17.0.2", decode_responses=True)

try:
    redis.ping()
except ConnectionError:
    print("ConnectionError!")
else:
    print("ok")

while redis.get("test") is None:
    test = redis.get("test")

print(test)

Second--- run app1.py

from redis import Redis
from redis.exceptions import ConnectionError
from time import sleep
from redis.backoff import ExponentialBackoff
from redis.retry import Retry


redis = Redis(host="172.17.0.2", decode_responses=True)

try:
    redis.ping()
except ConnectionError:
    print("ConnectionError!")
else:
    print("ok")

redis.set("test", "devops")
```
---


#### Expire:

```bash
set test devops
expire test 60
```

#### TTL(Expire status):

```bash
ttl test
```

#### SETEX(Set key expire value at the same time simultaneously)
```bash
setex test 10 devops
```

#### Example:

```bash
from redis import Redis
from redis.exceptions import ConnectionError
from sys import exit

r = Redis(host="127.0.0.1", decode_responses=True)

try:
    r.ping()
    print("Connected")

except ConnectionError:
    print("Connection Error!")
    exit(1)

user = "araz"
password = "123456"

auth_count_key = ":".join(["auth", user, "auth_count"])
auth_blocked_key = ":".join(["auth", user, "auth_blocked"])

ask_password = input("Enter password: ")

if r.exists(auth_blocked_key) != 0:
    print("Authenticaion is current blocked for this user:")
    exit(1)

if password != ask_password:

    if r.exists(auth_count_key) == 0 :
        r.set(auth_count_key, 0)
    current_auth_count = r.get(auth_count_key)
    if int(current_auth_count) < 10:
        r.incr(auth_count_key)
    else:
        r.setex(auth_blocked_key, 60, "1")
        r.set(auth_count_key, 0)

    print("Invalid password.")
    exit(1)

print("Wellcome to program...")
```

#### INCRBY:

```bash
incrby test 20
```














