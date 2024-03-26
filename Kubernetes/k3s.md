https://k3s.io/

curl -sfL https://get.k3s.io | sh - 
# Check for Ready node, takes ~30 seconds 
sudo k3s kubectl get node 
--------------
kubectl completion bash > /etc/bash_completion.d/kubectl
logout
----------------------
cat /etc/rancher/k3s/k3s.yaml
-------------------------
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
kubectl get nodes 


------------name space-----------------------
kubectl get ns


---------POD----------------json or yaml-------------
Resource POD

Object manifest

apiVersion: v1
kind : pod

kubectl api-resources

kubectl explain pods


kubectl explain pods.metadata

-------------------------------------------------------
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


------------------------------------------------

kubectl apply -f pod.yaml

kubectl get pod
kubectl get pod -o wide

kubectl get nodes -o wide
--------------------------------------------------------------

curl 10.42.0.9

------------------------------------------------------------

kubectl delete pod test
kubectl get pod

---Replica set-for-self yeling-desire state-scaling---------------------------------------------

kubectl api-resources | grep replicaset

kubectl explain replicaset


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

------------------------------------------------
kubectl apply -f rs.yaml

kubectl get rs


kubectl get pods
kubectl get pods -o wide


---------------------------------------------------

ssh to node and watch kubernets services

watch -n0.1 kubectl get pods -o wide

----------------------------------------------------
For test:

kubectl delete pod test-dgr44

kubectl delete pods --all

-------------------------------------------------------















































































