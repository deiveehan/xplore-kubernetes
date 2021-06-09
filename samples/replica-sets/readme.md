# Replica-sets

## ReplicaitonController

```shell script
k apply -f replication-controller-basic.yml
k get all
k get rc
k delete pod/myapp-9cnlp
k get all
```

## ReplicationSet
```shell script
k apply -f replica-sets-basic.yml
k get all
k delete pod/myapp-6lnn8
k get all
```

### Additional operations
```shell script
# Scaling replicasets
k scale rs myapp --replicas=4

# Deleting just the replicasets

```



## kubernetes.io samples
https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/




## Discussion points
- Differences:
    - ReplicationController - old
    - ReplicationSet can point to pod that are defined in other files. 
        - selector is mandatory in replicationset. 
        
- Deployment manages replicasets. 


# Questions

