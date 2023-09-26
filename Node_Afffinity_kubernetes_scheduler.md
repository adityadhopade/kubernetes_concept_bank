# Node Selectors

### These are nothing but the labels attached on the Nodes; they are matured and identified so taht they can run the POD's on.

```
kubectl label nodes <node_name> <label_key>=<label_value>
kubectl label nodexs node01 size-large
```
**Node selector fails wherein we need to applyu multiple conditions on the POD's like below**

  - place pods on large or medium nodes
  - do not place on small nodes

- To resolve this we need to use the **NODE AFFINITY AND ANTI AFFINITY**
