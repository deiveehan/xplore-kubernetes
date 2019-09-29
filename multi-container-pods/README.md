## Multi-container pods
Normally an application container will be deployed in one pod. However it is possible to have more than one container to be in one pod.

We should only have related containers in a pod that forms one single unit of work. For example, it is not advisable to have web app in one container and mysql in another container in the same pod.

### Why Multi-container pods
Multi-container pods are used mainly when you want the business logic to be separated from the cross cutting componets by placing the supporting functionalitiies such as log externalizing, secured access in a separate container than the container which performs the business logic. 

### Communication between multi-container pods

Communication between different containers can happen in different ways. 



* Shared network space.. conatainer can interact with another container using localhost 
![network port]
(/screenshots/container-networking-port.png)

* Shared storage volume
Can have one container writing to a shared storage
volume while the other container read from the 
shared storage volume 

![Storage volume]
(/screenshots/container-storage.png)

* Shared process namespace: Containers can interact with one another containers process using shared process namespace
![Shared process namespace]
(/screenshots/container-storage.png)

