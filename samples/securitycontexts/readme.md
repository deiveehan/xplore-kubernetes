### Security context


#### Prerequisite

Set user and group in the worker nodes.
#### Worker node 1 changes 
Add new user and group. 
```shell script
sudo useradd -u 2000 container-user-0
sudo groupadd -g 3000 container-group-0
sudo mkdir -p /etc/message
echo "Hi Sam" | sudo tee -a /etc/message/message.txt
cat /etc/message/message.txt

sudo chown 2000:3000 /etc/message/message.txt
sudo chmod 640 /etc/message/message.txt
```

#### Worker node 2 changes 
Add new user and group. 
```shell script
sudo useradd -u 2000 container-user-1
sudo groupadd -g 3000 container-group-1
sudo mkdir -p /etc/message
echo "Hi Sam" | sudo tee -a /etc/message/message.txt
cat /etc/message/message.txt

sudo chown 2000:3000 /etc/message/message.txt
sudo chmod 640 /etc/message/message.txt
```
#### Create a new pod that has security context with user permissions
<a href="securitycontext-pod-basic.yml">Pod sample</a>

#### Run sample
```shell script
kubectl apply -f securitycontext-pod-basic.yml
kubectl exec my-securitycontext-pod -- ps
kubectl delete pod my-securitycontext-pod --now
kubectl logs my-securitycontext-pod

Change the value of the security context runAsuser & fsGroup to some other value to check access
kubectl apply -f securitycontext-pod-basic.yml
kubectl exec my-securitycontext-pod -- ps
kubectl logs my-securitycontext-pod
```
