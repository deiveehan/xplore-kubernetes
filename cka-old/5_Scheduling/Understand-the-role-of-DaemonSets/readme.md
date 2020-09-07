## DaemonSets

A daemon set ensures that all nodes run a copy of the pod

- Node gets added, pod gets added. 
- Node gets deleted, pod gets garbage collected.

Use cases:
- Run a monitoring agent in each node of the cluster. 
- Run a vm logs viewer in the nodes. 

Examples:
- kube-proxy is a daemonsets. 
- networking solution (weave-net) requires daemon sets. 

