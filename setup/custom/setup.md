Setup all nodes. 
**************************
The following need to be done for all master and worker nodes. 

```shell script
lsmod | grep br_netfilter
sudo modprobe br_netfilter
```

```shell script
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
br_netfilter
EOF
```

```shell script
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sudo sysctl --system
```

#### Download gpg key for docker 
```shell script
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
#### Add docker repository
```shell script
sudo add-apt-repository    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

#### Add gpg key for kubernetes
```shell script
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```
#### Add kuberentes repository
```shell script
cat << EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
```

# Install 
- Docker CLI
- Kubelet CLI
- Kubeadm CLI
- Kubectl CLI

```shell script
sudo apt-get update
sudo apt-get install -y docker-ce 
sudo apt-get install -y kubelet
sudo apt-get install -y kubeadm
sudo apt-get install -y kubectl
```
#### Prevent the following packages from automatically upgrading:
```shell script
sudo apt-mark hold docker-ce kubelet kubeadm kubectl
```

#### Enable iptables bridge call: 
```shell script
echo "net.bridge.bridge-nf-call-iptables=1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```
*************************
#### Master nodes
*************************
#### Setup CIDR value 
```shell script
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

#Setup kubectl 
```shell script
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
#Install flannel networking
```shell script
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

*************************
#### WORKER NODES
*************************

-------------
```shell script
sudo kubeadm join $controller_private_ip:6443 --token $token --discovery-token-ca-cert-hash $hash
```
-------------

workers would have joined the master.
Goto master node and issue the commands to view the nodes. 
```shell script
kubectl get nodes
kubectl get pods --all-namespaces
```

kubeadm join 10.0.2.15:6443 --token d8erpd.bmqosqd0g99bponw --discovery-token-ca-cert-hash sha256:1258c9c2fcd985c244f3ab0cc75e3b7873a09f2ea3fc4afaa0cfba45dabb6f64
