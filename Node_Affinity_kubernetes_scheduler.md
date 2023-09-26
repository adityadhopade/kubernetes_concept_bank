# Node Affinity

### It gives granular level of control on the POD placement on the nodes (still can't gurantee the POD's will be placed on desired nodes)

```
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringhExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: size
          operator: In                                       #there are many operators used for various combinations; we can also do the values as simply "exists"
          values:
          - Large                                            #multiple values can be present in the values; for matching the conditions
          - Medium
```

### Q. What if the Node Affinity could not match a given expression ? Whjat if someone changes the label in future ? Will pod continue to stay in the Node ?
YES it can be assured with the help of the Node Affinity Property

- Available
- Planned

### Available (2 Types)

## - requiredDuringSchedulingIgnoredDuringExecution
If POD is available then run on desired node or else if the given POD is N.A. then stop the execution

## - prefferedDuringSchedulingIgnoredDuringExecution
If POD is available then try to run on tghe desired Node; If pod is N.A. **try to run on given or any other node**

## Planned (2 Types)

## - requiredDuringSchedulingRequiredDuringExecution
If POD is available then run on desired node or else if the given POD must be placesd on the same Ndoe after Execution

## - prefferedDuringSchedulingRequiredDuringExecution
If POD is availabel then try to run on tghe desired Node; If pod is N.A. **try to run on given or any other node after execution** 


## Q. apply color=blue to node01
```
kubectl label nodes nodes01 color=blue
```

### Q. Create a deployment named blue with the nginx image and 3 replicas
```
kubectl create deployment blue --image=nginx --replicas=3
```


### Create a new deployment named red with nginx image and 2 replicas and ensure it gets placed on a control plane ndoe only. Use label ``node-role.kubernetes.io/master-set`` on control plane

```
kubectl create deployment red --image=nginx --replicas=2 --dry-run=client -o yaml > red.yaml
kubectl describe node controlplane

```

vi red.yaml 

```
spec:
  affinity:
    NodeAffinity:
      required.....:
        nodeSelectorTerms:
        - matchExpressions:
          - key: "node-role.kubernetes.io/master-set"
            operator: Exists

As it do not contains any vaue from here after so we have removed it and change from equlas to "exists"
```
