#Upgrade clusters

## Upgrading kubernetes cluster version

### Get the current version of client and the server
k version --short
k get pod kube-controller-manager-deiveehanxplore1c.mylabserver.com -n kube-system -o yaml

k8s.gcr.io/kube-controller-manager:v1.13.12

### Master nodes upgrade

#### Upgrading kubeadm to 1.16.6
```shell script
kubeadm version
sudo apt-mark unhold kubeadm kubelet
sudo apt install -y kubeadm=1.16.6-00
kubeadm version
sudo kubeadm upgrade plan
sudo kubeadm upgrade apply v1.16.6
```

#### upgrading kubectl
```
kubectl version
sudo apt-mark unhold kubectl
sudo apt install -y kubectl=1.16.6-00
sudo apt-mark hold kubectl
kubectl version
```

#### Upgrading kubelet
```
sudo apt-mark unhold kubelet
sudo apt install -y kubelet=1.16.6-00
sudo apt-mark hold kubelet
```


### Worker nodes upgrade

####Upgrading kubelet and kubectl on the worker nodes.

```
sudo apt-mark unhold kubelet
sudo apt install -y kubelet=1.16.6-00
sudo apt-mark hold kubelet
```


## OS upgrades

#### Check the pods which pod where they are running
```shell script
kubectl get pods -o wide
```

#### Evict the pods by draining the node
```
kubectl drain <nodename> --ignore-daemonsets
kubectl get nodes
kubectl uncordon <nodename>
kubectl get nodes
```

#### Delete the nodes
```shell script
kubectl delete node <node>

```

#### Generate the token and the worker node join command in the master node. 
```
sudo kubeadm token generate
sudo kubeadm token list
sudo kubeadm token create [token_name] --ttl 2h --print-join-command
```

Run the command generated in the worker node
