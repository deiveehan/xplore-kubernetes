## Namespaces

### What is a namespace

Namespaces are ways by which you can organize your applications and categorize them, can also be used to organize application teams, environments etc., 
You can also use namespaces as a way to divide cluster resources between different users (usign resource quota)
#### different namespaces
- default 
- kube-system
- kube-public (resource made available for all users must be here.)

Some commands:
```shell script
Kubectl get namespaces              // Get all the namespaces in the cluster
kubectl create ns test-namespace             // Create a namespace called test-namespace
```

#### using yaml file/
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: test-namespace

```

```shell script
k apply -f test-namespace.yml
k get namespaces
```

#### Set default namespace
```shell script
k config set-context $(kubectl config current-context) --namespace=test-namespace
kubectl config view --minify | grep namespace:
```

#### Using services accross namespaces
Use the below notation if you want to use services across different namespaces.
![](.readme_images/60b370f6.png)

Note:
- Every pod belongs to some namespaces. 
- Default namespace. 
- System namespaces. 

#### See which resources are in a namespace and which arent
```shell script
# In a namespace
kubectl api-resources --namespaced=true

# Not in a namespace
kubectl api-resources --namespaced=false

```
