# IMPORTANT COMMANDS

- ``-f``: It represents the file
- ``-o``: Output in the format 
- ``--dry-run=client``: To dry-run the yaml file (just show the file) and do not save the configuration 

```
# To get service

kubectl get seervice
kubectl get svc

# To get pods
kubectl get pods
kubectl get po

# To get Deployments
kubectl get deployments
kubectl get deploy

# To get Replicasets
kubectl get replicasets
kubectl get rs
```

```
#To replace the contents in the YAML file

kubectl replace --force -f <path-to-yaml-file>.yaml

```