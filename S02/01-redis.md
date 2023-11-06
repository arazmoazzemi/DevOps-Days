redis


docker run -d --name redis redis

docker exec -it redis bash

connect to database:
redis-cli

### partitioning for increase database speed and performance

---

check Redis connectivity
PING ----> PONG

---

data store for key value:
SET

set test devops
get test

set x 10
get x

----

Increament:
INCR

incr 10


DECR

decr 10
---

find:
EXISTS

exists test


---

delete:
del 

del test


---

override:

set test devops
get test

set test redis
get test

---

Moniter(watch):
# we need two terminal for this this commands:

get test devops
get test


---


KEYS:
Show all keys:

keys *

set name1 john 
set name2 araz
set name3 rosa

keys name*

---
FLUSH
Note! In redis exists 16 databese [0-15] and Default databese is 0

Example:

select 1
keys *
# (empty array)

select 0 keys *


flushdb
Delete running database

flushall
Delete all of databases


---


































