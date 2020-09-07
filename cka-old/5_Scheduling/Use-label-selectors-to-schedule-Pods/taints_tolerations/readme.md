
Taints and tolerations are introduced to provide rules for the node when to accept / reject a pod.

Taints are rules set by the node and tolerations are configurations in the pod corresponding to the taint defined in the node. 

## Taints

kubectl taint nodes <node-name> key=value:taint-effect

tainteffect:
- noSchedule
- PreferNoSchedule
- NoExecute

```shell script
k describe node master | grep Taint
k  taint nodes master node-role.kubernetes.io/master:NoSchedule-
k describe node master | grep Taint
taint nodes node01 spray=mortein:NoSchedule
k apply b.yml

#Untaint







```

##### NoExecute
- Evicts pod that are not following taint rule in existing setup. 






## Tolerations



