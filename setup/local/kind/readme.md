## Using KIND to install kubernetes


### Installation
```shell script
brew install kind
kind create cluster --name firs-tcluster
k cluster-info 
kind delete cluster
```

#### Create a cluster using yaml file

```shell script
kind create cluster --config simple-cluster/cluster.yml
```
