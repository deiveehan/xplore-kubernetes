## 

Scheduler takes care of placing the pod on a node based on different factors including 
- amount of resources reuqired by the pod and resources available by the node. 

If there are no resources available in the node, scheduler places the pod in the "PENDING state"

K8s assumes the Minimum amount of cpu requested by a container to be

Defaults limits for a container:
```
CPU: 1
Memory: 512Mi
```
Developer can modify the request by specifying the resource limits in the pod configuration. 
