# Pod Basics

## Simplest pod
```shell script
# Imperative 
k run nginx --image=nginx

## Declarative
k apply -f 1-pod.yml
k get all
k delete -f 1-pod.yml
```

##Labels

Provides a way to add some information to your objects that can be used to filter them later. 
- to search objects by filter (say all objects reltated to front end app)
- Assign resources to objects using label selectors

[Overview](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

### Using labels (Imperative way)
```shell script
k run nginx --image=nginx --labels="env=dev,app=test-boot"
k get pods --selector env=dev
k get pods -l env!=dev
k get pods -l 'env in (dev)'
k get pods -l 'env notin (dev)'
```
#### Create labels
[label-pod-basic.yml](1pod.yml)

#### View labels 
```shell script
k apply -f 1-pod-with-label.yml
k describe pod label-pod-basic

k get pods -l app=label-pod-basic
k get pods -l env=dev
k get pods -l env=dev,app=label-pod-basic
k get pods -l 'env in (production, qa)'
k get pods -l 'env notin (production, qa)'

k delete -f 1-pod-with-label.yml

```

## Annotations

Unlike labels, annotations are not used to identify and select objects.
They are used by tools and libraries to retrieve this metadata. 

[Overview](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/)

Example:
[simple annotation example](3-pod-with-annotations.yml)

```shell script
k apply -f 3-pod-with-annotations.yml
k describe pod annotations-demo | grep Annotations -C 2
k delete -f 3-pod-with-annotations.yml
```
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
k run nginx --image=nginx -n test-namespace
k delete ns test-namespace
k get ns
#Notice that the namespace does not exist anymore

```

#### using yaml file/
[sample namespace](1_namespace.yml)

```shell script

k apply -f 4a-namespace.yml
k get namespaces
k apply -f 4b-pod-with-namespace.yml
k get pods -n test-namespace
```

#### Set default namespace
```shell script
k config set-context $(kubectl config current-context) --namespace=test-namespace
kubectl config view --minify | grep namespace:
```

```shell script
# Cleanup
k delete -f 4b-pod-with-namespace.yml
k delete -f 4a-namespace.yml
```

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


