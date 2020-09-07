## Deployments

are a way to manage a set of pods to add functionality to handle replicasets, scaling pods etc., 



#### Create a basic deployment

Create [Simple deployment](deployment-dep-basic.yml)
```shell script
k apply -f deployment-dep-basic.yml
k get deployments
k get pods
```

You should be able to see multiple instances of pods based on the number you specified in the replicasets.

#### Edit the deployment directly
```shell script
k edit deployment nginx-deployment
```

change the replicaset to 1 and you will see the change immediately getting reflected. 
Kubernetes automatically manages the desired state based on the replicaset you specify

### Rolling update

Create a deployment with an image version, update the image version using rolling update version

Create [Rolling deployment](rolling-update/rolling-dep-basic.yml)
```shell script
k set image deployment/rolling-dep-basic rolling-dep-basic=1.7.9 --record
```

The above command will perform a rolling update of all the pods one by one and update the image version to 1.7.9

