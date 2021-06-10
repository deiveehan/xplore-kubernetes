# ConfigMaps

[Configmaps Overview](https://kubernetes.io/docs/concepts/configuration/configmap/)

* Create config maps
    * Using imperative commands
    * Using YAML
* Use config maps
    * Inside a container using command and args
    * As an Env variables for a container
    * As a file in Read only volume
    * Read using the kubernetes API

## Using imperative commands

### AS literals from command line.
Create config map
```shell script
# Using literals
k create configmap sportsmap --from-literal=player_name=Samson --from-literal=sportCategory=Football
k describe cm sportsmap
k delete cm sportsmap
```

### AS properties file.
Create a properties file
[cfmap.properties](1-cfmap.properties)

```shell script
# Using properties file
k create configmap sportsmap --from-file=1-cfmap.properties
k describe cm sportsmap
#Cleanup
k delete cm sportsmap
```

# 2. Using YAML

```shell script
k apply -f 2-cm-simple.yml
k describe cm sportsmap
```

### Using Config maps as env variables from a pod

#### 1. Read all cfmap variables as env
Another example:
```shell script
k apply -f 2-pod-read-all-cm-vars.yml
k describe pod nginx
k exec pod/nginx -- printenv
k delete pods/ginx

```
#### 2. Read cfmap specific environemnt variables
Create pod: [sample](pod-using-env-valueFrom.yml)

```shell script
k apply -f 2-pod-using-cm-env-valueFrom.yml
k exec pod/nginx -- printenv

k delete pods/ginx
```

#### 2. As a file in Read only volume
```shell script
k apply -f pod-using-volumes.yml
k logs sports-pod
k delete pods/ginx

```

#### 3. Read config map attributes as files 
```shell script
k apply -f 3-pod-read-cm-as-files.yml
k exec -ti nginx -- /bin/bash
cd /etc/sportsmap
cat player_name
exit
k delete pods/nginx

```

