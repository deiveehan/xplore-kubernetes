# API Server


Overview:


What it does:
* Authentcates and validates request. 
* talks to etcd cluster and responds back with information. 
* Talks to kubelet in case of any pod creation. 

Notes:
- Kubeadm deploys apiserver as a pod
- You can also send POST commands. 
- Scheduler monitors api server continuously for information. 


![](.readme_images/1eba7960.png)

#### Kube api server options:
vim /etc/kubernetes/manifests/kube-apiserver.yml
![](.readme_images/24023dd4.png)

#### Viewing kube-api-server process
![](.readme_images/c72c5868.png)


[API Referece](https://kubernetes.io/docs/reference/kubernetes-api/)
