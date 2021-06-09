# Node Selector
Assign a pod to a particular node. 

## Steps
```shell script
# Label a node
k label node kubenode02 size=large

# Create a pod with node selector options.
k apply -f pod-nodeselector.yml

# Check which node the pod is scheduled
 k get pods -o wide
```

