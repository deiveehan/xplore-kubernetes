

## Architecture overview
<img src="images/architecture.001.jpeg"></img>

The cluster composites a minimum of 1 master node and 1+ worker nodes. The master node is the node that acts as control plane and manages the worker nodes. 

The worker nodes are the place where your actual application runs.  
### Master node

Components:
- [API Server](APIServer.md)
- [Scheduler](scheduler.md)
- [Controller Manager](controllermanager.md)
- [etcd](etcd.md)


### Worker node

Components:


The applications are deployed inside the worker node. 
If your application is running 3 instances, the instances may be deployed in different worker nodes.
[Application instances](images/app-distribution.png)
