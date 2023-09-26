### Select pods with the required selector we get
```
kubectl get pods --selector env=prod --no-headers | wc -l        wc=> wordcoumt
```

### to fetch data from multiple selectors we will use
```
kubectl get pods --selector env=prod,bu=finance,tier=frontend
```

### Taints and Tolerations
- They have nothing to do with security of Cluster
- They determine what pods can be placed on node
- Taints are applied to the nodes; while tolerations are applied to the pod
- ### It still does NOT Gurantees the plaement of the POD will be in the desired node
- ### Taint and Toleration do not tell a POD which node to go; but inturn makes the node to accept certain POD's with the Toleration

  To get the taints we have
  
  ```
  kubectl taint nodes node-name key=value:taint-effect
  kubectl taint nodes node1 color=blue:Noschedule
  ```

### Taint Effect
- taint-effect are of type **Nocschedule, PreferSchedule, NoExecute**
- **NoSchedule** => Tries to avoid placing Pod on the node
- **NoExecute** => New POD's will not be scheduled on Nodesand existing POD's if existint on Nodeswill be evicted as they will not be able to tolerate the taint

- YAML SYNTAX
```
spec:
  tolerations:
    - key: "app"
      operator: "equal"
      value: "blue"
      effect: "NoSchedule"
```

### Q. Why there is no POD's by default scheduled on Master Node?
- As it has the Taint setted in MASTER NODE in the like
  ```
  Taints: node:role.kubernetes.io/master:NoSchedule
  ```
### Q. How to create taint on node01 with the key of spray; value of mortein and effect of NoSchedule
```
kubectl taints node node01 spray:mortein effect:NoSchedule
```

### Q. To create another POD named bee with the image nginx; which has the toleration set to taint mortein

```
kubectl create bee --image=nginx --dry-run=client -o yaml > bee.yaml

# under bee.yaml will be our yaml add the toleration here

tolerations:
  - key: "spray"
    operator: "equal"
    value: "mortein"
    effect: "NoSchedule"
```

