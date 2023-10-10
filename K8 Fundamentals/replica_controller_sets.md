# Replica Controller (DEPRICATED)

## It helps to run multiple instances of our POD's in K8 cluster; for providing High Avalability(HA).

- In case of having single pods; if it goes down it will helpto bring it up.
- Replicastion Controller spans across multiple nodes in a cluster.

- RepController
```
apiVersion: v1
kind: ReplicaController
metadata:
  creationTimestamp: null
  labels:
    run: nginx-pod
  name: nginx-pod
spec:
  containers:
  - image: nginx:alpine
    name: nginx-pod
    resources: {}
replicas: 3  
```

-ReplicaSet
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  creationTimestamp: null
  labels:
    run: nginx-pod
  name: nginx-pod
spec:
  containers:
  - image: nginx:alpine
    name: nginx-pod
    resources: {}
replicas: 3
  selector:
    matchLabels:
      type: front-end
```

## Commands to execute 

```
# TO create the deployment
kubctl create -f sample.yaml

# To get Replication Controller
kubectl get replicationcontroller

# TO create the deployment
kubctl create -f sample.yaml

# To get Replica Set
kubectl get replicaset
```

### Why to use Labels and Selectors ?
- Replicaset can have ``atleast 3 Replicas at anytime in the Cluster.``

### How would ReplicaSet know which PODS to monitor?
- The Role of the ReplicaSet is to monitor POD's and any of them fails deploy a new one.

```
replicaset.yaml
-----------
selector:
  matchLabels:
    tier: front-end

--------------

pod.yml
-------------------
metadata:
  name: myapp-pod
  labels:
    tier:front-end

```

- Replicaset now can taget proper pod with help of match labels, now it knows which pods to monitor

### How to scale the Replicaset ?

```
kubectl replace -f replicaset-def.yaml

kubectl scale --replicas=6 -f replicaset-def.yaml

kubectl scale --replicas=2 -f <type> <name>

eg ==> kubectl scale --replicas=6 -f replicaset myapp-replicaset
```



