# Network policy: Limit access to a service


## Steps
```shell script
kubectl create deployment nginx --image=nginx
kubectl expose deployment nginx --port=80
```

Test access form another pod
```shell script
kubectl run busybox --rm -ti --image=busybox -- /bin/sh
wget --spider --timeout=1 nginx
# Status shows connected
```

### Limit access to the service
```shell script
k apply -f netpol.yml

kubectl run busybox --rm -ti --image=busybox -- /bin/sh
# Status shows disconnected

# Set the label defined in the network policy and run the program again. 
k run busybox --rm -ti --image=busybox --labels=access=true -- /bin/sh

# Now check if you have access
wget --spider --timeout=1 nginx

# Status shows connected

```

Reference: https://kubernetes.io/docs/tasks/administer-cluster/declare-network-policy/

