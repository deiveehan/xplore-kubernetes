

Monitor:
* Nodes
* apps

#### Metrics server
- in memory monitoring solution (does not store on disk)
- contains current information. 

How it works:
- retrieves information from kubelet (cAdvisor)
- retrieves information 

#### Installing metrics server
```shell script
minikube addons enable metrics-server

git clone <metrics server git url>
kubectl create -f deploy/<version>/

```


#### Retrieve statistics
```shell script
k top node
k top pod

```
