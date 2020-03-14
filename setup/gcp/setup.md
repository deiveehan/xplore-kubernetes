#### Create VPC network
```shell script
gcloud compute --project=<PROJECT_ID> networks create fb-apps-vpc --subnet-mode=custom
gcloud compute --project=<PROJECT_ID> networks subnets create fb-apps-subnet --network=fb-apps-vpc --region=northamerica-northeast1 --range=<CIDR_RANGE>
```

#### Create a kubernetes cluster
```shell script
gcloud beta container --project "<PROJECT_ID>" clusters create "<CLUSTER_NAME>"" --zone "<ZONE>" --no-enable-basic-auth --cluster-version "1.14.10-gke.17" --machine-type "g1-small" --image-type "COS" --disk-type "pd-standard" --disk-size "100" --metadata disable-legacy-endpoints=true --scopes "https://www.googleapis.com/auth/devstorage.read_only","https://www.googleapis.com/auth/logging.write","https://www.googleapis.com/auth/monitoring","https://www.googleapis.com/auth/servicecontrol","https://www.googleapis.com/auth/service.management.readonly","https://www.googleapis.com/auth/trace.append" --num-nodes "3" --enable-stackdriver-kubernetes --enable-ip-alias --network "projects/<PROJECT_ID>/global/networks/fb-apps-vpc" --subnetwork "projects/<PROJECT_ID>/regions/northamerica-northeast1/subnetworks/fb-apps-subnet" --default-max-pods-per-node "110" --no-enable-master-authorized-networks --addons HorizontalPodAutoscaling,HttpLoadBalancing --enable-autoupgrade --enable-autorepair --tags "application"
```
\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\
(or)
create a cluster using the GKE console. 

#### Connect to the kubernetes cluster
gcloud container clusters get-credentials fb-apps-cluster --zone northamerica-northeast1-a --project <PROJECT_ID>