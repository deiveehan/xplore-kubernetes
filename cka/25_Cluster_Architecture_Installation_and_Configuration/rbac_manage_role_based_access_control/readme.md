# RBAC


Type of access:
- Users
    - Admin
    - Platform operators
    - Developers
    - End users of the application
- Systems
    - Another pod/app.

Motivation:
- Users may belong to multiple groups. 
- Only certain groups or users should access a particular namespaces. 

# Authentication mechanisms
- Static password file
- static token file
- Certificates
- Identity Services - (Ex: ldap)

#### Static password file:
- Manage a file called "userinfo.csv"
- Pass the flag of csv to the api server service file or as command in the kube-api-server.yaml
```shell script
--basic-auth-file="userinfo.csv"
```

### Role
- Access provided for resources and action is defined as verb. 
- Scope is at the namespace level. 
- Resources: pod, deployment, Secrets
- Verb: get, watch, put, list

### ClusterRole
- Scope is at the cluster level. 

### Role binding
- Role bound to Subjects
- Subjects: 

### Clusterrole binding
- Similar to role binding, but cluster role binding is at the cluster level. 

### Managing users
- Creating users

#### 



```shell script
#Service account creation
# list service account

```
