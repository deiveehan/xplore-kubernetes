## Services

Services acts as proxy to the pods. 

### Service types
* ClusterIP (Default)
* NodePort
* Loadbalancer

#### Get started

Create a basic nginx deployment that runs on port 80 [Deployment](nginx-deployment-basic.yml)

Create a service file that maps to the deployment and exposes on port 8080 [Service](nginx-service-basic.yml)

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service-basic
spec:
  selector:
    app: nginx-deployment
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 80
  type: ClusterIP
```

```text
k apply -f nginx-deployment-basic.yml
k apply -f nginx-service-basic.yml
```

kubectl get pods

```shell script
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-855d56dd9c-2z25k   1/1     Running   0          9m49s
nginx-deployment-855d56dd9c-7thsw   1/1     Running   0          9m50s
nginx-deployment-855d56dd9c-h4jkc   1/1     Running   0          9m49s
```

kubectl get svc

```shell script
NAME                  TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)    AGE
kubernetes            ClusterIP   10.0.0.1      <none>        443/TCP    5d3h
nginx-service-basic   ClusterIP   10.0.13.187   <none>        8080/TCP   5m30s
```

kubectl get endpoints

```shell script
NAME                  ENDPOINTS                                   AGE
kubernetes            35.223.35.84:443                            5d3h
nginx-service-basic   10.56.0.23:80,10.56.1.47:80,10.56.1.48:80   88s
```
