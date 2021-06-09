# Taints & Tolarations

Way to say restrictions on a node to accept certain pods. 
Note: It does not say that pod should always go to one node. that is achieved
 using NodeAffinity.

## Tainting a node
### Taint syntax: 
```shell script
k taint nodes <node-name> <key>=<value>:taint-effect

```
### Taint effects
- NoSchedule
- PreferNoSchedule
- NoExecute 

### Taint operators:
- Exists
- Equals

### Sample:
```shell script
k taint nodes kubenode01 app=blue:NoSchedule

k apply -f red-pod.yml
k apply -f blue-pod.yml
k get pods -o wide
k taint nodes kubenode01 app=blue:NoSchedule-
k taint nodes kubenode01 app=red:NoExecute

k taint nodes kubenode01 app=red:NoExecute-
```
