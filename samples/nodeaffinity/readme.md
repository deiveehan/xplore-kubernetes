# Node Affinity
Assign a pod to a particular node based on dynamic criteria

## Steps
```shell script
# Label a node
k label node kubenode02 size=large

# Create a pod with node selector options.
k apply -f pod-nodeselector.yml

# Check which node the pod is scheduled
 k get pods -o wide
```

