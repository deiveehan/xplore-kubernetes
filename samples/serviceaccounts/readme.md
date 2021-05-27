# Service accounts
Provides a way for the container to access the kubernetes API

Use cases:
- Monitoring application uses service account to access kubernetes api
- Jenkins uses sa to deploy app into the kubernetes. 
## Creating a service account - simplest example
```shell script
k get serviceaccounts
k create serviceaccount test-serviceaccount
k get serviceaccounts
k describe sa test-serviceaccount
k get secrets
k get secret test-serviceaccount-token-tpdhm -o yaml
```

### What happens when you create a service account. 
- Creates the service account. 
- Creates the token for the service account. 
- Create a secret and store the token in the service account. 
- Links the secret object with the secret. 

### Accessing from an app outside the cluster. 
```shell script
curl <endpoint -insecure --header "Authorization: Bearer <token>"
```

## Default service account. 
```shell script
k run nginx --image=nginx
k describe pod nginx
# Note the mount location in the pod that has the service account directory
#     Mounts:
#        /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-4tfxc (ro)
k exec -it nginx -- cat /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
k exec -it nginx -- cat /var/run/secrets/kubernetes.io/serviceaccount/token
```

## Create sa and map to a pod.
```shell script
k apply -f sa.yml
k apply -f sa-pod.yml
k exec -it nginx -- cat /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
k exec -it nginx -- cat /var/run/secrets/kubernetes.io/serviceaccount/token

```

### Accessing from an app inside the cluster
- Mount the token as a volume in the pod requesting the pod. 

## Discussion:
- you can only use the service account from the same namespaces. 

