

```shell script
kubectl run hostnames --image=k8s.gcr.io/serve_hostname \
                        --labels=app=hostnames \
                        --port=9376 \
                        --replicas=3

k get svc

kubectl expose deployment hostnames --port=80 --target-port=9376

kubectl run -it --rm --restart=Never busybox --image=busybox:1.28 sh


```
