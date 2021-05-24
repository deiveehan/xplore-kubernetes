##Labels

Provides a way to add some information to your objects that can be used to filter them later. 
- to search objects by filter (say all objects reltated to front end app)
- Assign resources to objects using label selectors

## Using labels (Imperative way)
```shell script
k run nginx --image=nginx --labels="env=dev,app=test-boot"

```
#### Create labels
[label-pod-basic.yml](label-pod-basic.yml)

#### View labels 
```shell script
k apply -f label-pod-basic.yml
k describe pod label-pod-basic
```

#### How to utilize labels
```shell script
k get pods -l app=label-pod-basic
k get pods -l env=dev
k get pods -l env=dev,app=label-pod-basic
k get pods -l 'environment in (production, qa)'

```


#### Label selectors
