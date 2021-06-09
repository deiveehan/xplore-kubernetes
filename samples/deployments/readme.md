# Deployments


## Simplest deployment
[deployment-basic](k8s/nginx-deployment.yml)

```shell script
k create deploy httpd-frontend --image=httpd:2.4-alpine --replicas=3
#OR
k apply -f k8spwd
/nginx-deployment.yml

k get all
```

## Check status of a deployment
```shell script
# --record
k apply -f k8s/nginx-deployment.yml --record

# Check status of the deployment
kubectl rollout status deployment nginx-deployment
```

## Updating a deployment with a different image
```shell script
k set image deployment/nginx-deployment nginx=nginx:1.16.1 --record
#(OR)
kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1 --record
k rollout status deployment/nginx-deployment

```
