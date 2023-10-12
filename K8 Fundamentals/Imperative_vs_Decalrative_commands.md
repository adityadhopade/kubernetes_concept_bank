# ``Imperative VS Declarative Commands``

## Imperative Commands: [Try to use it more in CKA]
- We need to manulally provide iot step by step to get our desired state of results
- Some set of commands are as follows
```
kubectl run nginx --image=nginx
kubectl replace --force -f <path to the file>
kubectl create deployment dep --image=nginx
kubectl expose deployment nginx --port 80
kubectl edit deployment nginx
kubectl scale deployment nginx --replicas=5
kubectl set image deployment nginx nginx=nginx:1.18
```

## Declarative Commands: 
- In this we just provide our requirement to the system then setting up the infra according to the requiremnt is the responsibilty of the system.

- eg> Tools such as Terraform, Ansible, Puppet comes into this category
- It will consist of commands like as follows
```
kubectl apply -f deployment.yaml
```

## Some insights about ``kubectl edit`` vs ``kubectl replace``
- Using ``kubectl edit`` he changes we do to the yaml file they are not set to the orignal yaml file as it is saved in the **kubernetes memory**.
- So the local copy[orignal copy] will not contain the changes in it which are made during ``kubectl edit``
- Now if we make the change in the orignal file then all the changes we made previously (stored in kubernetes memory) would get lost.
- If we want to make sure that all our changes get applied then use ``kubectl replace --force -f <pah to file>``

## What if we will try to create a file that is already created?
- It will fail

## What if the nginx file we delete and try to replace it?
- Fails, files must exist to replace

### Create a pod nginx using the image nginx:alpine
```
kubectl create nginx --image=nginx:alpine 
kubectl run nginx --image=nginx:alpine
```

### Create the redis pod; with redis alpine image; set label tier=db
```
kubectl run redis --image=redis:alpine 
kubectl label pods redis tier=db
```

### Create a redis serviceto expose the redis application within cluster on port 6379
```
kubectl create svc clusterip redis --tcp 6379:6379 -o yaml --dry-run=client > redis.yaml
kubectl apply -f redis.yaml

kuebctl create svc <service-type> <srevice-name> <Connection Type> <PORT TO EXPOSE ON> -o yaml --dry-run=client > redis.yaml
``` 

### Create a deployment namaed webapp using the image kodekloud/webapp-color with 3 replcias
```
kubectl create deployment webapp --image=kodekloud/webapp-color --replicas=3 -o yaml --dryy-run=client > deployment.yaml
kubectl apply -f deployment.yaml
```

### Create a new pod custom-nginx using nginx image and expose it on container port 8080
```
kubectl run custom-nginx --image=nginx --port=8080
```

### Create a new namespace called as dev-ns
```
kubectl create namespaces dev-ns
```

### Create new deployment called as redis-deploy in the dev-ns namespaces with the redis image and it should have 2 repllicas
```
kubectl create deployment redis-deploy --image=redis --namespace=dev-ns --replicas=2 -o yaml --dry-run=client > dep-redis.yaml
kubectl appluy -f dep-redis.yaml
```

### Create a pod httpd image=httpd:alpine in default ns; create a svc of type CLusterIP by same name httpd; target port for service should be 80
```
# By default namespace is default and the service is also of Type ClusterIP
kubectl run httpd --image=httpd:alpine --port=80 --expose=true

# --expose= true actually represents that we want to use the service of the type ClusterIP assosiated with the POD and it requires --port

```