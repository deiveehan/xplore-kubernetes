## Jobs

### Job
A job is a runtime app to execute a workload within a short period of time, it executes runs and once it runs, then shuts down

#### Create a job
Create job [calc job](calc-job-basic.yml)

```shell script
k apply -f calc-job-basic.yml
k get jobs
k logs pod/<podname>
```

You could see the output of the job and see that the status of the pod is completed and shut down.

#### Cleanup
```shell script
k delete job/calc
```


### Cronjob
A Cron job is something that you can schedule multiple times based ona  regexp. 

Create [Cronjob](sch-cronjob-basic.yml)

```shell script
k apply -f sch-cronjob-basic.yml
```

```text
NAME                            READY   STATUS      RESTARTS   AGE
calc-5psxw                      0/1     Completed   0          9m22s
cronjobhello-1588738020-znrtv   0/1     Completed   0          38s
```

```shell script
k logs pod/cronjobhello-1588738020-znrtv                        git:(master|✚1…
```
```text
Wed May  6 04:07:03 UTC 2020
Hello from Samson
```

#### Cleanup
k delete cronjob/cronjobhello

