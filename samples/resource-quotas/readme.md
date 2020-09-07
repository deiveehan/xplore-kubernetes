## Resource quotas

When more than one team shares the same cluster, you can set the quotas per namesspace. 

You can restrict the quotas using the following attributes:
- cpu
- memory
- no. of pods you can run on the namespace. 


#### Set resource quota for a namespace
````shell script
k apply -f compute-quota.yml
k get resourcequotas
k describe resourcequota compute-quota
````


#### Defining how much your pod wants

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: frontend
spec:
  containers:
  - name: db
    image: mysql
    env:
    - name: MYSQL_ROOT_PASSWORD
      value: "password"
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
  - name: wp
    image: wordpress
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```
