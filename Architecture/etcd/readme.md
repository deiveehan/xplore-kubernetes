# etcd database
- a simple key value database. 

## Installation

```shell script
brew install etcd
```

#### start etcd database
```shell script
etcd
```

#### Some command operations using etcd database. 
```shell script
etcdctl put name deiveehan
etcdctl get name
etcdctl del name

etcdctl endpoint health

```


## How is etcd used in kubernetes

- stores information about nodes, pods, secrets, roles. 
- exposed by the API server. 


## Setup:
- manual
- kubeadm

- kubeadm deploys etcd as a pod in the master node.
- kubeadm deploys api-server as a pod in the master node. 



```shell script
kubectl exec etcd-master -n kube-system etcdctl get / --prefix -keys-only
```
