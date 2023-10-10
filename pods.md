# PODS: 
- It is the lowest level of Object in K8s that we can control 

```
apiVersion: v1
kind: Pods
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

- ``apiVersion``: It shows us the K8's API VErsion
- ``metadata``: It gives us the Data about the k8 objects like Pods, DeploymentSets, Replicasets, it contains details like labels and name. It only expects name and labels ONLY.
- ``labels``: It is like a dictionary having **key:value** pair, used for filtering pods 
- ``spec``: It content varies depending on the K8's objects
- ``name``: It indicates the list of the names; and alos indicates the first item in the list

- ``apiVersion``, ``kind``, ``metdata``, ``spec`` are always the part of every definition (manifests) file. 