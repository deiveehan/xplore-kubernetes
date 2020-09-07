## Testing the cluster

#### Check if you can run a pod in a cluster
````shell script
k run nginx --image=nginx
k get deployments
k get pods
k logs nginx-6db489d4b7-8dnjl
````

#### Check if you can reach the server using port-forwarding
```shell script
k port-forward nginx-6db489d4b7-8dnjl 8080:80
curl http://localhost:8080
```

#### Run commands inside the pod

```shell script
k exec -it nginx-6db489d4b7-8dnjl -- nginx -v
k exec -it nginx-6db489d4b7-8dnjl -- /bin/bash
```

#### Expose a deployment using service
```shell script
k expose deployment nginx --port 80 --type NodePort
curl <nodeportip>:<nodeportport>
```

#### Debug nodes
```shell script
k get nodes
k get nodes $node_name
k get nodes $node_name -o yaml
k describe node $node_name

k api-resources
hrome```
