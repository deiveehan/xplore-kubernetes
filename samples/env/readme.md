
#1. A simple pod reading environment variables. 
```shell script
k apply -f simple-env.yml
k logs nginx
k exec nginx -- env
k exec nginx -- printenv
k exec --it nginx -- /bin/bash
env
```

#2. A pod that reads the pod definition manifest entries
```shell script
k apply -f pod-definition-as-env.yml

```
