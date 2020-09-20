# 


###
#### Manage user
```shell script
# Generate john private key
openssl genrsa -out john.key -writerand john.random

# Create certificate sigining request. 
openssl req -out john.csr -key john.key --writerand john.random -subj "/CN=john/O=finance"
```

#### Get the kubernetes 


#### Create a namsepace

```shell script
kubectl create ns finance
```

