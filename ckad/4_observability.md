## Observability
- Understand Liveness probe and Readiness probe
- Understand container logging
- understand how to monitor applications
- Understand debugging in kubernetes


#### Pod status
- Pending
- ContainerCreating (Images are pulled and container attempts to start)
- Running

```shell script
k get pods
```

#### Pod conditions
- PodScheduled
- Initialized
- ContainersReady (Container ready but not the pod - init scripts may not be initialized)
- Ready (Ready to accept traffic)

```shell script
k describe pod <pod-name>
k get pods
```



#### Readiness probe
Kubernetes sets the pod to ready whenever the container starts. The scripts may not be initialized. 

```text
- What is the Running state indicate, does it mean it is Ready or Container ready. 
- Who is the best person to decide when the pod is ready
```

```text
- What happens when you set the readiness criteria. 
    (Kubernetes sets to READY status only when the criteria is met).
```
* Different ways to test:
- ping an api end point to check if its ready (api/ready)
```yaml
readinessProbe:
    httpGet:
      path: /api/ready
      port: 8080
    initialDelaySeconds: 10
    periodSeconds: 5
    failureThreshold: 8
```
- ping a TCP port test.
```yaml
readinessProbe:
    tcpSocket:
      port: 3306
``` 
- create a custom script and run them to check
```shell script
readinessProbe:
    exec:  bcxxz
      command: 
        - cat
        - /app/checkIfRunning.out
```

