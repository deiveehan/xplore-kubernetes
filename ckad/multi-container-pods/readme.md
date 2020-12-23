
## Multi-Container pods

Pods that have more than one container. 

#### Patterns
* Ambassador:   Which environment to connect to (Dev/QA/Prod DB) can be decided by the additional container
* Adaptor:      Converting logs from different pods to a specific log format. 
* Side car:     Log agent forwarding logs to the log server.

#### Why multi-container pods.
* Sometimes you may want 2 services to work together. 
    - Web application and a log agent. 
* Keep the business logic separate and clean. 

#### Characteristics:
* the containers in the pod share the same network and storage. 
