## Service accounts
Provides a way for the container to access the kubernetes API


- Service accounts are the identity of a pod. 
- token file holds authentication token
```shell script
cat /var/run/secrets/kubernetes.io/serviceaccount/token
```

#### List all service accounts
```shell script
k get serviceaccounts

```

#### Note:
- you can only use the service account from the same namespaces. 


The token provides the 
#### Create a new service account
```shell script
kubectl create serviceaccount test-serviceaccount
```

#### Create a pod that uses the service account

****
