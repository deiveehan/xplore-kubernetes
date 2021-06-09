# Kubernetes setup using vagrant file. 

### Prerequisite
- Install virtual box (Download and install from Virtual box site)
https://www.virtualbox.org/wiki/Downloads

- Install vagrant (Download and istall from vagrant site)
https://www.vagrantup.com/downloads.html

### Init VMs
This site uses an existing vagrant configuration from git, please download the git repo to provision the vms
```shell script
git clone https://github.com/kodekloudhub/certified-kubernetes-administrator-course.git
cd certified-kubernetes-administrator-course
vagrant up
vagrant status
```

This should provision a master vm and the worker vms

# In all nodes - master and worker

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




## Install docker
```shell script
sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io


```
```shell script
sudo mkdir /etc/docker
cat <<EOF | sudo tee /etc/docker/daemon.json
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF

sudo systemctl daemon-reload

sudo systemctl restart docker


```

```shell script
sudo systemctl enable docker
sudo systemctl restart docker
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update

```

## Installing kubeadm, kubelet and kubectl
```shell script
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```


# Initializing the control plane node (Master node only)

```shell script
#Get the api server ip address

ifconfig enp0s8
# Get the ip address and 

sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --apiserver-advertise-address=192.168.56.2
logout

```

# Install pod networking
[Pod networking using weave](https://kubernetes.io/docs/setup/production
-environment/tools/kubeadm/high-availability/)

```shell script
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

```
# Worker node only

```shell script
kubeadm join 192.168.56.2:6443 --token 4dxxdw.x420goz2mewse0gz --discovery-token-ca-cert-hash sha256:4de45a9f47a8fb20fe4aa8b1f1279c24994e9ac303ed513ef909938d6076b0b0
```

