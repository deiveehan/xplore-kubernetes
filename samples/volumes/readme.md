## Overview

### The problem:
The storage in the container is ephemeral (Pod is transient), which means that if you store anything in local file system, and the container stops, the content will not be available next time when the container starts. 

### How to resolve:
- Attach volume to the container. 
- volume lives outside the container in the host path. 
- When the pod dies or restarts, the volume is still available. 

### How it works in Docker
![](.readme_images/6505949c.png)
```shell script
docker volume create test_data
docker run --mount type=bind source=/data/mysql target=/var/lib/mysql mysql
```

Types:
[Volumes](volumes.md)
[Persistent Volumes](persistent-volumes.md)
- [PV/PVC Example](pvc-sample.md)

