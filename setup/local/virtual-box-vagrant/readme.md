## K8s installation in local using VB and vagrant

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

## Installing Kubernetes

### Install kubeadm
For latest steps pls refer
https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

# Master nodes


