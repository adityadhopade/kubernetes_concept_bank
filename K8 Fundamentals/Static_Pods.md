# Static POD's

- ## **Sceanrio** -  

### If masternode is not present and if only kubelet is present then can it create PODS ??

- **YES** Kubelet can still create a POD without the help of Control Plane as we provide it with the manifest files path like ``/etc/kubernetes/manifests`` based on this path whatever the files may be it would create the POD's with the help of it.

- **``kubectl`` cannot create other resources like daemonsets, replicasets etc it is just not possible for it to do that; such pods are known as "Static PODS"**

- Even if you try to edit the PODS, it will  attempt to restart the PODS

- While ruinning the services we can also change the path of the manifest files to create the Static PODS

```
-- config = konfig.yaml
```

## What if there is KUBE API Server available now ? Can the Kubelet now create Normal As well as Static PODS?
- **YES**, it can create the static pods from the ``/etc/kubernetes/manifests`` and also other pods with the help of via http API endpoint.

## Does API Server has any idea abnout the Static PODS created ?
- **YES** ``kubectl get pods``
- Static PODS will be listed as any other PODS.
- If its is a part of the cluster it also creates a mirror object in KUbe API Server; we can see details about the the POD we can only delete them.

## USE OF ``STATIC PODS``
-  We can used to deploy the "Control Plane Componenets" on the Static Pods.
- On each master download kubeket
- Add all components like controllr-manager, api server, etcd as manifests files
- So that it will be driven as StaticPods and even if it goes down it will still try to bring up the PODS

## STATIC PODS VS DAEMON SETS

- Static PODS are created with the help of Kubelet
- Daemon Sets are created with the help of Kube API Server.

- In Static PODS we can deploy the control plane componenets as Static PODS.
- In DaemonSets we can deploy the Monitoring Agents, Logging Agents on nodes.

### How many static pods exists in the cluster in all namespaces
```
kubectl get pods -A

# To identify the Static Pods it will contain the name of node attach to the pod names --> kube-scheduler-controlplane

kubectl get pods kube-scheduler-controlplane -n kube-system -o yaml

```

### Create the static pod named static-busybox that uses busybox image and command sleep 1000
```
kubectl run static-busybox --image=busybox --dry-run=client -o yaml --command --sleep 1000 > static.yaml 
```
