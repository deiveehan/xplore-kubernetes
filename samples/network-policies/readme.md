# Network policies


## Basic terms
- Ingress
- Egress
- Labels

### Some rules
#### Rule 1. Traffic is allowed unless there is a network policy selecting the pod. 
Example: If you dont do anything everything is allowed

#### Rule 2. Traffic is denied if there are policies selecting the pod, but none of them have any rules allowing it. 

(Based on 1 + 2 - You can only write rules that allow traffic. )


```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny-all
spec:
  podSelector: {} #Selects all the pods
  ingress: [] # Indicates nothing is whitelisted. 

#What is the result
# ALL TRAFFIC IS BLOCKED BY MATCHING AND NOT ALLOWING
```

#### Rule 3: Traffic is allowed if there is atleast one policy allowing it

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-only-traffic-from-service
spec:
  podSelector:  #For the User service pods
    matchLabels: 
      app: userService
      tier: service
  ingress:   
  - from: # Allow traffic from these pods
    - podSelector: 
        matchLabels:
          app: userdb
          tier: database

# No other pods can talk to the database.
# UserDB cannot be invoked by any other pods.  
# All ports are allowed. 
```

##### Rule 4: Policy rules are Additive. They are OR'ed with eatch other. 
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-only-traffic-from-service
spec:
  podSelector:  #For the User service pods
    matchLabels: 
      app: userService
      tier: service
  ingress:   
  - from: # Allow traffic from these pods
    - podSelector: 
        matchLabels:
          app: userdb
          tier: database
    - podSelector: 
        matchLabels:
          role: security

# If both the from pod selects the same pods, if either 1 is satisfied, then traffic is allowed. 

```


Dicussion points:
- rules are applied only to the same namespaces as ingress and pod selector

#### Rule 5: Network policy are scoped to the namespace they are deployed to

```yaml
apiVersion: 
kind: Namespace
metadata:
   name: foo-prod
   labels:
     purpose: prod
     product: foo
```
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-only-traffic-from-service
spec:
  podSelector:  #For the User service pods
    matchLabels: 
      app: userService
      tier: service
  ingress:   
  - from: # Allow traffic from these pods
      - namespaceSelector:
          matchLabels:
            purpose: prod

# Allowing traffic from other namespaces
You can label a namespace using 

 k label namespace testns purpose=prod

# Allowing some pods from another namespace is not possible.
```


