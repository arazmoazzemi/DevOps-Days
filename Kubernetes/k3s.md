[ks3 link](https://k3s.io/)

```bash
curl -sfL https://get.k3s.io | sh - 
# Check for Ready node, takes ~30 seconds 
sudo k3s kubectl get node
```
```bash
kubectl completion bash > /etc/bash_completion.d/kubectl
logout
```
```bash
cat /etc/rancher/k3s/k3s.yaml

export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
kubectl get nodes 
```

### Get name space
```bash
kubectl get ns
```

### Create PODs with yaml

- Resource POD

- Object manifest

### Example:
```bash
kubectl api-resources
kubectl explain pods
kubectl explain pods.metadata
```
```bash
touch pod.yaml
nano pod.yaml


apiVersion: v1
kind: Pod
metadata:
  name: test
  namespace: default
  labels:
    app.kubernetes.io/name: test
    app.kubernetes.io/env: production
    app.kubernetes.io/project: test
spec:
  containers:
    - name: nginx
      image: nginx:alpine
```

```bash
kubectl apply -f pod.yaml

kubectl get pod
kubectl get pod -o wide

kubectl get nodes -o wide
```
```bash
curl 10.42.0.9
```

```
kubectl delete pod test
kubectl get pod
```

**ReplicaSet Definition:**

- **Set of identical Pods**: A ReplicaSet manages multiple instances (replicas) of a Pod template.

- **Desired state**: ReplicaSet maintains a specified number of replicas, ensuring they match the desired state defined by the user.

- **Self-healing**: If a Pod fails or terminates unexpectedly, ReplicaSet replaces it automatically to maintain the desired number of replicas.

- **Scalability**: ReplicaSet allows scaling the number of replicas up or down dynamically to accommodate changes in workload demand.

```bash
kubectl api-resources | grep replicaset
kubectl explain replicaset
```
```bash

touch rs.yaml
nano rs.yaml

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: test
  namespace: default
  labels:
    app.kubernetes.io/name: test
    app.kubernetes.io/env: development
    app.kubernetes.io/project: test
spec:
  replicas: 5
  selector:
    matchLabels:
      app.kubernetes.io/name: test
  template:
    metadata:
      labels:
        app.kubernetes.io/name: test
    spec:
      containers:
        - name: nginx
          image: nginx:alpine
```
```bash
kubectl apply -f rs.yaml
kubectl get rs

kubectl get pods
kubectl get pods -o wide
```

### Test a replicaset cluster
```bash
ssh to node and watch kubernets services
watch -n0.1 kubectl get pods -o wide
```
### For test:
```bash
kubectl delete pod test-dgr44
kubectl delete pods --all
```

### Scaling:
```bash
kubectl scale replicaset test --replicas 10
kubectl get pods -o wide
```

```bash
nano rs.yaml

kind: ReplicaSet
metadata:
  name: test
  namespace: default
  labels:
    app.kubernetes.io/name: test
    app.kubernetes.io/env: development
    app.kubernetes.io/project: test
spec:
  replicas: 5
  selector:
    matchLabels:
      app.kubernetes.io/name: test
  template:
    metadata:
      labels:
        app.kubernetes.io/name: test
    spec:
      containers:
        - name: nginx
          image: nginx:1.17
```
```bash
kubectl apply -f rs.yaml
kubectl get pods -o wide
```

### Check nginx version into kubernetes container

```bash
kubectl exec test-qnw4n -- nginx -v
```

### Example of upgrade nginx-1.17 to nginx-1.18:
### Deployment


```bash

nano rs.yaml

kind: ReplicaSet
metadata:
  name: test
  namespace: default
  labels:
    app.kubernetes.io/name: test
    app.kubernetes.io/env: development
    app.kubernetes.io/project: test
spec:
  replicas: 5
  selector:
    matchLabels:
      app.kubernetes.io/name: test
  template:
    metadata:
      labels:
        app.kubernetes.io/name: test
    spec:
      containers:
        - name: nginx
          image: nginx:1.18

```bash
kubectl apply -f rs.yaml
kubectl describe rs test

```

### Deployment resource for rollbask and upgrade:
### Example of upgrade nginx-1.17 to nginx-1.18:
```bash

touch deploy.yaml
nano deploy.yaml 

apiVersion: apps/v1
kind: Deployment
metadata:
  name: test
  namespace: default
  labels:
    app.kubernetes.io/name: test
    app.kubernetes.io/env: production    
spec:
  replicas: 10
  selector:
    matchLabels:
      app.kubernetes.io/name: test
      app.kubernetes.io/env: production
  template:
    metadata:
      labels:
         app.kubernetes.io/name: test
         app.kubernetes.io/env: production
    spec:
      containers:
        - name: nginx

          image: nginx:1.17
```

```bash
kubectl delete rs test
kubectl apply -f deploy.yaml
```
```bash
kubectl get pods -o wide
kubectl exec test-7b4f9f5568-2dzh4 -- nginx -v
```

### After deployment you should be update tmplate section to 1.18 nginx version:

```nano deploy.yaml 

apiVersion: apps/v1
kind: Deployment
metadata:
  name: test
  namespace: default
  labels:
    app.kubernetes.io/name: test
    app.kubernetes.io/env: production    
spec:
  replicas: 10
  selector:
    matchLabels:
      app.kubernetes.io/name: test
      app.kubernetes.io/env: production
  template:
    metadata:
      labels:
         app.kubernetes.io/name: test
         app.kubernetes.io/env: production
    spec:
      containers:
        - name: nginx

          image: nginx:1.17

```

#### Check nginx version
```
kubectl apply -f deploy.yaml
kubectl exec test-7b4f9f5568-2dzh4 -- nginx -v
```

















































































