

# Use Kubeadm to install a basic cluster

## What is kubeadm
- helps an operator in setting up a cluster in a easier way.  

## What can kubeadm do
- setup a cluster with certs between different components. 


## Setting up a cluster

### Prerequisite:
- VMs - Master and worker vms. 
- Network connectivity between the them

### High level configuration steps. 
```text
* Prerequisite
    * Check if br-netfilter is installed and if not install the module
    * Configure linux IP tables to see correctly the bridged traffic. 
* Install softwares
    * Install Docker
    * Install Kubeadm
    * Installl Kubelet
    * Install kubectl
* Creating a cluster
    * Kubeadm init
		kubeadm init --pod-network-cidr 10.244.0.0/16 --apiserver-advertise-address=10.0.2.15
    * Create kubeconfig file
    * Deploy pod network
* Check:
    * Check if pod network is installed
    * Check if nodes are available
    * Test if you can deploy. A pod. 
```
Reference: 
- https://kubernetes.io/docs/setup/production-environment/container-runtimes/

#### Prerequisite In all the nodes
```shell script
lsmod | grep br_netfilter
sudo modprobe br_netfilter
lsmod | grep br_netfilter

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sudo sysctl --system

```
#### Install Docker in all nodes
```shell script
sudo -i

### Install packages to allow apt to use a repository over HTTPS
apt-get update && apt-get install -y \
  apt-transport-https ca-certificates curl software-properties-common gnupg2

# Add Docker's official GPG key:
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

# Add the Docker apt repository:
add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) \
  stable"


# Install Docker CE
apt-get update && apt-get install -y \
  containerd.io=1.2.13-2 \
  docker-ce=5:19.03.11~3-0~ubuntu-$(lsb_release -cs) \
  docker-ce-cli=5:19.03.11~3-0~ubuntu-$(lsb_release -cs)

mkdir -p /etc/systemd/system/docker.service.d

systemctl daemon-reload
systemctl restart docker
sudo systemctl enable docker
```

#### Install kubeadm
```shell script
sudo apt-get update && sudo apt-get install -y apt-transport-https curl

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF

sudo apt-get update

sudo apt-get install -y kubelet kubeadm kubectl

sudo apt-mark hold kubelet kubeadm kubectl
```

#### Master node: Kubeadm init

```shell script
kubeadm init --pod-network-cidr 10.244.0.0/16 --apiserver-advertise-address=192.168.56.2

```
What this does:
- Pulls images for the kubernetes cluster
- Creates the required certs and puts them in /etc/kubernetes/pki
- Creates the kubeconfig file in the following folder. 
  /etc/kubernetes/admin.conf, kubelet.conf, controller-manager.conf, scheduler.conf
- Creates manifest configurations in /etc/kubernetes/manifest folder
- Start the kubelet, kube-api-server, kube-controller-manager, kube-scheduler based on the manifest file. 
- Creates the required config maps - kubeadm-config, kubelet-config-xxx
- Marks the node as control-plane y adding the required labels. 
- Mark th emaster node unschedulable by adding the Noschedule taint
- Configure RBAC rules
- Apply essential addon: CoreDNS
- Apply essential addon: kube-proxy
- Prints the required command to create the kubeconf file
- Print the command for the worker node to join the master node

```shell script
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

```
Check the nodes
```shell script
alias k=kubectl
k get nodes # displays only one node)

```

### Install the pod network
```shell script
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

```
This will install weave pod network to the cluster. 

#### Worker node: Join the master nodes
```shell script
kubeadm join 192.168.56.2:6443 --token c57bzi.c7k2aejeqcmem72b \
    --discovery-token-ca-cert-hash sha256:db5d0629c3b4870c5459c42df1b158be23ad72df4f46e3b3c7bc1b8c5c9a7fc3
```

What this does:
- Creates the kubelet configuration file in /var/lib/kubelet/config.yaml
- Starts the kubelet
- Joins the worker node to the cluster - CSR sent to apiserver and obtained a response
- kubelet configured wiht the new secure connection details

