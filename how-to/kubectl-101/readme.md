

```shell script
k run nginx --image=nginx
k get deployments
k get pods

k port-forward nginx-7db9fccd9b-rs87l 8081:80
curl http://localhost:8081

k logs nginx-7db9fccd9b-rs87l
k exec -it nginx-7db9fccd9b-rs87l -- nginx -v // Executing a command from the pods

// Expose services
k expose deployment nginx --port 80 --type NodePort
k get services

```
