## Create a kubernetes cluster (GKE)

## Objective:
- Create a Kubernetes cluster using GCP console
- Kubectl configurations in local system
- Connect to kubernetes cluster
- Run a simplest nginx pod in the cluster. 

### Prerequisite
- have a GCP project already created. 

#### Download gcloud SDK and install
https://cloud.google.com/sdk/docs/downloads-versioned-archives
```shell script
./google-cloud-sdk/install.sh
gcloud init
```

### Create cluster 
- GCP Console
- gcloud command

#### Create a kubernetes cluster
```shell script
gcloud beta container --project "<PROJECT_ID>" clusters create "<CLUSTER_NAME>"" --zone "<ZONE>" --no-enable-basic-auth --cluster-version "1.14.10-gke.17" --machine-type "g1-small" --image-type "COS" --disk-type "pd-standard" --disk-size "100" --metadata disable-legacy-endpoints=true --scopes "https://www.googleapis.com/auth/devstorage.read_only","https://www.googleapis.com/auth/logging.write","https://www.googleapis.com/auth/monitoring","https://www.googleapis.com/auth/servicecontrol","https://www.googleapis.com/auth/service.management.readonly","https://www.googleapis.com/auth/trace.append" --num-nodes "3" --enable-stackdriver-kubernetes --enable-ip-alias --network "projects/<PROJECT_ID>/global/networks/fb-apps-vpc" --subnetwork "projects/<PROJECT_ID>/regions/northamerica-northeast1/subnetworks/fb-apps-subnet" --default-max-pods-per-node "110" --no-enable-master-authorized-networks --addons HorizontalPodAutoscaling,HttpLoadBalancing --enable-autoupgrade --enable-autorepair --tags "application"
```
(OR)
create a cluster using the GKE console. 

#### Connect to the kubernetes cluster
gcloud container clusters get-credentials <CLUSTER-NAME> --zone northamerica-northeast1-a --project <PROJECT_ID>

#### kubectl basic commands

k cluster-info
k get nodes
k describe node <nodename>
k get pods
k get pods -n system
kubectl create ns test-ns
#### Create a new pod
```yaml

apiVersion: v1
kind: Pod
metadata:
  name: test-pod
  labels:
    app: test-pod
spec:
  containers:
    - name: test-pod
      image: nginx
      imagePullPolicy: IfNotPresent
  restartPolicy: Always
```
```shell script
k apply -f test-pod.yml
k get pods

```
