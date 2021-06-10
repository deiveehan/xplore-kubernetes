# Passing enviromnet variables to the container

## Declarative approach
```shell script
# Passing env variable and printing it. 
k run nginx --image=nginx --env="NAME=Deiveehan" -- printenv
k logs pod/nginx
k delete pod/nginx

```

## Using Manifest
### A simple pod reading environment variables. 
```shell script
k apply -f simple-env.yml
k logs nginx
k exec nginx -- env
k exec nginx -- printenv
k exec --it nginx -- /bin/bash
env
exit
k delete pod/nginx
```

## Reading kubernetes definition file as environment variables
```shell script
k apply -f 2-pod-definition-as-env.yml
k delete pod/nginx

```
