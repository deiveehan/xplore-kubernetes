## Multi-container pod

Running more than one container in a pod. 


### Create more than one container

Create a pod that has more than one container


Run the pod
```shell script
k apply -f multicontainer-pod-basic.yml

```

### How can multi-container pods be used
- Containers running in a pod share the network, can access each other using localhost. 
- Share volumes: one container can write and other can read from the storage volume 
- Shared process namespace: interact with each other process using shared process namespace

#### Design patterns
* Sidecar pod
    - Enhances the functionality of main container insome way. 
    - main container (web server) sidecar (every 1 hour gets static content and update main container)
    
* Ambassador Pod
    - Translating network traffic
    - port forward to hardcoded port in main container. 
    
* Adapter pod
    - Converts the output of the main container to adapt to other systems. 
    - Example: Apply formatting to logs that can be used by other monitoring systems. 
 
 
