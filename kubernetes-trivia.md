## Kubernetes 1.22, CoreDNS 1.8.4
# Kubernetes important commands

```
kubectl proxy -v=8 # To get the insights of the K8's (What is happening in the background)
kubectl api-resources  # TO get all the api resources in the K8's cluster
kubectl explain pods --recursive | more # To get all the meta details of the pods in the yaml format
kubectl cluster-info # To get info about the cluster  
```

## What does K8's needed to run ?
It needs both the CNI [Container Network Interface] and CRI [Container Runtime Interface]
- CRI contains the components like **Docker, Containerd**
- CNI contains the components like **CoreDNS, CNI, KubeProxy**

## What is needed if CoreDNS is still in a pending state?
- It needs to have the networking IP of the CNI's like Flannel, Calico, Weavenet to be the same as the pod-network-cidr while initializing the kubeadm for generating the cluster.
- Summary: [Network IP of CNI == POD-Network-CIDR]

 ## How to make a pod accessible within the outside the cluster ?
 - Either via the **K8 Services** or via **K8 Port Forwarding**
 -  
