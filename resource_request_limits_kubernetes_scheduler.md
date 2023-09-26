# Resource Request and Limits 
- CPU and Mem are the two parts in the Pods which are crucial to manage
- If there is no ndoe with enough CPU and Memory it will give us insufficient CPU in the logs.

- We can give the CPU and memory like as below
  ```
  resources:
    requests:
      memory: "4GI"
      cpu: 2     
  ```
  Scheduker looks for the ndoes with the 4Gi memory aand 2 CPU and if the node is met then places the POD on that node
-----------------------------------------------------------------------------------------------------------------------------------------------------------
### FOR CPU
- 1 CPU = 1vCPU in AWS, 1 Azure Core, 1 Hyper Thread, 1 GCP Core
- 0.1 CPU = 100m (m => milli) **least we can go is 1m**

------------------------------------------------------------------------------------------------------------------------------------------------------------------
### FOR MEMORY

- 256 Mi = 26843548
- 1G (GigaByte) = 1,000,000,000 Bytes
- 1M (MegaByte)= 1,000,000 Bytes
- 1K (KiloByte)= 1,000 bytes

 - 1Gi(Gibibyte) = 1,073,741,824 bytes
 - 1 Mi (Milibytes) = 1,048,576 bytes
 - 1 Ki (Kilibytes) = 1024 bytes

- **Remember**
- **Gi > G ; Mi > M ; Ki > K**
------------------------------------------------------------------------------------------------------------------------------------------------------------------

By default the container has no limit and can consume as much resourcesas required; so we need to ***limit** the resources

```
resources:
  request:
    memory: "4Gi"
    CPU: 2
  limit:
    memory: "1Gi"
    CPU: 0.4
```

### Q. What happens when the PODS want to have resources more tahn the limits ?

- **In case of CPU** ==> It throy=ttles the CPU and we cannot have more resources than provided
- **In case of memeory** ==>  Conatiner can use more memory than the limit and it will give us Pod termnation with the "OOM Error"

- **In case of CPU ideal sceanrio would be to set rquest and give no limits** ==> As the request is et each POD is guaranteed 1 vCPU; and limits are not setany pod can run have manty cycles as avaliable in it.
- ### Resources Request and Limits can be set for each POD's

-  **In case of memory ideal sceanrio would be to set rquest and give no limits** ==> As the POD's will take all the resources availableand we need to make all the resources killed for the Pod1 to survive

### Q. Can we ensure that every pod created has some default set for mem and cpu ?

-**YES with limit-ranges**
- They are applicable at namespace level
- Limit ranges allows us to create duifferent default values for containers POD's; without a request or limit defined in the POD defination file
- we can use it like the template below same for CPU and memory
   ```
   apiVersion: V1
   kind: LimitRange
   metadata:
     name:cpu-resource-constant
   spec:
     limits:
     - default:
         cpu: 500m
       defaultRequest:
         cpu:500m
       max:
         cpu:"1"
       min:
         cpu: 100m
       type: container
   ```


   ### Q. is there any chance to create / restrict total amount of resources that can be consumed by app deployed in k8s cluster?
- **YES, by using the Resource Quotas at namespace level, also we can assign some HadQuota for each namespace**
- used klike this template
- ```
  apiver: vi
  kind: ResourceQuota
  metadata:
    name: my -res-quota
  spec:
    hard:
      requests.cpu:4
      requests.mem:4Gi
      limits.cpu: 10
      limits.memory: 10Gi
  ```

### Q. The elephant pods runs a process taht consumes 15Mi of mem; Increase the limit of elephant pod to 20 mi

- Try 1 :We will try and chnage the pods limit value by editing the limit
- But it will not get changed as it is Hard Copied using commands
-  Try 2 : We will try to regenerate the file with tg=he help of logs in the /tmp/kubectl-edit-<hashvaue>.yml
-  ```
   kubectl replace --force -f /tmp/kubectl-edit-<hashvalue>.yml
   ```
