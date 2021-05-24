
#### Run commands inside a pod
```shell script
k exec webapp -- cat /log/app.log

# Run a test pod to validate access to a cluster (SSH into a temp pod that will be deleted upon exit)
k run -i --tty --rm nginx --image=nginx --restart=Never -- sh
```




