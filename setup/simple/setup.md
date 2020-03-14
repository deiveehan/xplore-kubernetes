Setup all nodes. 
**************************
The following need to be done for all master and worker nodes. 

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

---- To fix a defect in k8s 1.13.4
```shell script
sudo apt-get update

sudo apt-get install -y docker-ce=18.06.1~ce~3-0~ubuntu kubelet=1.13.5-00 kubeadm=1.13.5-00 kubectl=1.13.5-00
```
#### Prevent the following packages from automatically upgrading:
- kubelet
- kubeadm
- kubectl

sudo apt-mark hold docker-ce kubelet kubeadm kubectl

#### Enable iptables bridge call: 
```shell script
echo "net.bridge.bridge-nf-call-iptables=1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

## Master node setup
***************************
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
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/bc79dd1505b0c8681ece4de4c0d86c5cd2643275/Documentation/kube-flannel.yml
```
#### On each worker nodes do these..
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