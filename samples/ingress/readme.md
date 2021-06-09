# Ingress


## Overview

Limitations of Node port. 
- User has to know any of the node port ips, nodes may be dynamically created
 / destroyed during upgrades. 
- You still need one IP address that need to be mapped to a domain naming
 service. 
- You still need to map to one port that maps to these node ports. (80
 -> node ports)
 
Limitations of Load Balancer
- separate external Ip per service is created - you need to pay for each
 external ip. 

