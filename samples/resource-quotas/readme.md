# Resource quotas

When more than one team shares the same cluster, you can set the quotas per namesspace. 

You can restrict the quotas using the following attributes:
- cpu
- memory
- no. of pods you can run on the namespace. 


## Set resource quota for a namespace
````shell script
k apply -f compute-quota.yml
k get resourcequotas
k describe resourcequota compute-quota
````

## Create a pod
```shell script
k apply -f compute-quota-pod.yml
```

## cleanup
```shell script
k delete ns test-namespace
```
## Resource quota (Kubernetes doc sample)
[Resource quota](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/quota-memory-cpu-namespace/)


# Limit Range
[Limit-Range CPU Sample](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/cpu-constraint-namespace/)
[Limit-Range Memory Sample](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/memory-constraint-namespace/)


# Pod quota
[Pod Quota Sample](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/quota-pod-namespace/)
