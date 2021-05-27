# Security context
- Define access control setting for a pod or container. 

## Usecases
- permission to access a file. 
- give the process some additional privelege. 


## Prerequisite
[Docker security basics](docker-security-basics.md)

## Simplest security context 
[securitycontext sample](securitycontext-pod-basic.yml)

### 
```shell script
k apply -f securitycontext-pod-basic.yml

```
