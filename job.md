# Job / Cronjob

Cronjob : 

- used for backup job
- used for recursive jobs

## Example:

job.yaml file:

````
apiVersion: batch/v1
kind: Job
metadata:
  creationTimestamp: null
  name: myjob
spec:
  completions: 8
  parallelism: 3 //run parallel tasks
  template:
    metadata:
      creationTimestamp: null
    spec:
      containers:
      - command:
        - sleep
        - "15"
        image: ubuntu:18.04
        name: myjob
        resources: {}
      restartPolicy: Never
status: {}

````

Commands to run:
````

  453  k create job myjob --image=ubuntu:18.04 --dry-run=client -o yaml -- sleep 15 > job.yaml
  454  vi job.yaml
  455  k get all
  456  k delete ds fluentd-elasticsearch
  457  k get all
  458  k apply -f job.yaml
  459  watch kubectl get all
  460  vi job.yaml
  461  k delete job myjob
  462  k apply -f job.yaml
  463  watch kubectl get all
  464  vi job.yaml
  465  k delete job myjob
  466  k apply -f pod.yaml
  467  watch kubectl get all
  468  k delete po nginx
  469  k apply -f job.yaml
  470  watch kubectl get all
  471  history
````

## Cronjob

https://crontab.guru/examples.html

Commands to run:

````
78  k create cj mycj --image=ubuntu:18.04 --dry-run=client -o yaml --schedule="*/1 * * * *" -- sleep 10 > ch.yaml
  479  mv ch.yaml cj.yaml
  480  vi cj.yaml
  481  k delete job myjob
  482  k apply -f cj.yaml
  483  watch kubectl get all
  484  k explain job.spec
  485  history

````
