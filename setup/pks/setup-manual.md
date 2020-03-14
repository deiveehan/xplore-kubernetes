##Installation

### Prerequisite:
* Enable post deploy scripts in Opsman Director config pane. 
* Apply changes. 

### Sizing requirements. 

### Installation
* Install PKS tile from Pivnet. 

### Configure PKS

#### Assign Availabilty zones and networks

#### Configure PKS API 
* Provide PKS API certificate (ca / private key)
* provide the API server host name
* Set worker VM max in flight. 

#### Configure plans
* Select the plan you want to activate and mark as active. 
* Set the following attributes:
- name of the plan and its description

* Master node configurations
- no. of master and etcd node instances. 
- Master node VM type
- Availability nodes for master nodes. 

* Worker node instances
- no. of worker nodes.
- VM types
- Worker persistent disk type
- Worker availability zones. 
- eviction configuration
- errand vm type 

* Kubernetes cloud provider configuration
- Choose GCP
- provide project id, vpce network.
- provide master service account id.
- provide worker service account id. 

* Configure PKS logging. 
- Syslog address and port.
- enable TLS and cert if applicable. 

* NETWORKING configuration
- Choose Flannel or NSX-T configuration.
if(flannel)
- Provide flannel CIDR 
- provide Kubernetes service network CIDR 

UAA configuration
- provide PKS API Access token lifetime (in seconds)
- PKS API refresh token 

* Configure LDAP as Identity provider
- Select LDAP server option and provide
- LDAP server url
- LDAP credentials
- LDAP url configurations 
- configuration certs

* Resource config
- name of the PKS api load balancer. 


*** Apply changes ***

* Get the PKS api endpoint
- Get from PKS tile -> status -> Pivotal Container Service -> IP Address

* Configure External Load balancer
- Create GCP load balancer for the PKS API. 

* Install PKS and kubectl

* Connecting PKS cli
- target your UAA server 
uaac target https://PKS-API:8443 --ca-cert ROOT-CA-FILENAME

- Get the token: 
uaac token client get admin -s UAA-ADMIN-SECRET`

- Grant cluster access to new / existing users. 

- Login to PKS
pks login -a PKS-API --client-name CLIENT-NAME --client-secret CLIENT-SECRET --ca-cert CERTIFICATE-PATH

- Creating a kubernetes cluster
pks create-cluster CLUSTER-NAME \
--external-hostname HOSTNAME \
--plan PLAN-NAME \
[--num-nodes WORKER-NODES] \
[--network-profile NETWORK-PROFILE-NAME]







Reference: 
- https://docs.pivotal.io/pks/1-3/installing-pks-gcp.html

#### Raising firewall requests. 

#### Installing certificates




#### Configuration to existing docker.
