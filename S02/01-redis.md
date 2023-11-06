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












































