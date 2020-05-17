## ConfigMaps
```shell script
cd configmap-sample-1
kubectl apply -f config-map-sample.yml
```


### Mounting config maps as environment variable
```shell script
kubectl apply -f config-map-pod-basic.yml
kubectl get configmaps
kubectl get pods
kubectl logs test-configmap-pod
```

### Config maps as volume
```shell script
k apply -f config-map-pod-volume.yml
k logs test-configmap-pod-volume
kubectl exec test-configmap-pod-volume -- ls /etc/config
kubectl exec test-configmap-pod-volume -- cat /etc/config/empName
```

### Cleanup

