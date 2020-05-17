## Volumes

The storage in the container is ephemeral, which means that if you store anything in local file system, and the container stops, the content will not be available next time when the container starts. 

Volume helps in creating storage that lives outside the container. 

The volumes defined in the above pod lives in the node, 
