## Local setup using minikube

### 1. Install Virtual box. 
```shell script
sudo apt-get install virtualbox
```
### 2. Minikube. 
```shell script
brew cask install minikube
```

### 3. Start minikube
```shell script
minikube start
minikube status
```
### 4. Kubectl
```shell script
Brew install kubectl
```

You can access Kubernetes cluster using the following ways:
1. CLI - kubectl
2. Dashboard
3. API

```shell script
minikube dashboard
```

This opens up a dashboard which you can use to view the pods, replica sets and other information about the kubernetes. 

```shell script
minikube stop
```

Some commands to get started
```shell script
kubectl run hello-minikube --image=gc4.io/google_containers/echoserver:1.4 --port=8080
kubectl expose deployment hello-minikube --type=NodePort
kubectl get deployments
kubectl get pods
kubectl delete deployment hello-minikube
```
