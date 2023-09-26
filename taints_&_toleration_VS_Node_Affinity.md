## Taints and Toleration marks the node for the entry of certain pods with the affinity but it does not guarantees taht the POD's will be placed on the desired node only they can alos be placed on the other nodes(where taints and tolerations are not applied)

## Node Affinitywe mark the nodes with the respective **nodeNames** they allow the POD's to settle in but does not gurantee that ONLY the desired pods get the entry in the Node (desired + other pods can enter the node)

## The Comnintaion of Both the Taints & Tolerations AND Node Affinity can be used to target desired POD's on the Desired NODES; (this approach is widely used) 
