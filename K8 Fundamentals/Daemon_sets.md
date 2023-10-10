# DaemonSets 

## It ensures that atleast 1 copy of POD runs ion each node.

- They are same as that of replicasets; Helpsto deploy mulrtiple instances of the PODS
- Whenever a node gets added a new pod with the help of Daemon Set will be adeded and vice-versa.

## USECASE: Can be used as a monitoring solution and for logs viewer.
### - In K8's generally the Kubelet runs on the DaemonSet (As it is required on every Node in Cluster to perform the applications)

### The networking solutions like Weavenet, Calcio also executes with the help of DeamonSets

# Daemonset vs ReplicaSet

## DaemonSet Syntax
```
apiVersion: apps/v1
kind: DaemonSet
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
```

## ReplicaSet Syntax
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
```

## Commands to Execute

```
# To create the Daemonsets via pod.yaml ddefinaition
kubectl create -f pod.yaml 

# To get all the Daemonsets
kubectl get daemonsets
kubectl get ds 

# To describe the daemonsets
kubectl desc daemonsets pod.yaml

# To get all daemonsets via all namespaces
kubectl get daemonsets -A
```

### How does the DaemonSet Works ?
- It uses the NodeASffinity and DefaultScheduler [v1.12 and Above K8's] 
- Before it was using the BNode Name before [v1.12]

- Important commands
```
## If the changes in the yaml not executed then we can replce the yaml files with tghe help of this command

kubectl replace --force -f /tmp/manifests/<hash-value>.yml
```