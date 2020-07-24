
#### Cluster information
```shell script
k cluster-info
k get componentstatus             //  Get cluster health information. 
```



#### Config
k config view
k coifig

# PODS
k get namespaces
k get po --all-namespaces
k get all -n kube-system
k get po -n default
k get po --all-namespaces -o wide
k get deployments
k get po --all-namespaces --show-labels -o wide


#Monitoring
k top pods
k top pod <pod name>
k top pods -n <namespace>
k top nodes
