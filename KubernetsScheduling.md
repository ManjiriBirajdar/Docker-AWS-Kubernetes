# Scheduling

how to assign specific pod to run on specifix node/machine?

## Node selecter

 Add label to the node
 
 Pod has option of adding node selecter
 
 e.g hdd.ssd label. Node with only SSD
 
 
````

  333  kind delete cluster
  334  vi config
  335  kind create cluster --config config
  336  k get no
  337  k get no --show-labels
  338  k describe no kind-worker
  339  k label no kind-worker hdd=ssd
  340  k describe no kind-worker
  341  k get no --show-labels
  342  k get po --show-labels
  343  cd k8s/
  344  vi pod.yaml
  345  k apply -f pod.yaml
  346  k get po
  347  k get po -o wide
  348  k get po --show-lable
  349  k get po --show-lables
  350  k get po --show-labels
  351  vi pod.yaml
  352  k apply -f pod.yaml
  353  k get po --show-labels
  354  k label po nginx label=test
  355  k get po --show-labels
  356  k edit po nginx
  357  k get po --show-labels
  358  k get po
  359  k delete po nginx
  360  k label no kind-worker hdd-
  361  k get no --show-labels
  362  k get po
  363  k get no
  364  k apply -f pod.yaml
  365  k get po
  366  k describe po nginx
  367  history

````

## Node affinity

1. requiredDuringScheduling
2. preferedDuringScheduling

yaml file settings:

````
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
    app: nginx
  name: nginx
spec:
  affinity:
          nodeAffinity:
                  requiredDuringSchedulingIgnoredDuringExecution:
                          nodeSelectorTerms:
                                  - matchExpressions:
                                        -  key: hdd
                                           operator: In
                                           values:
                                                - ssd
  containers:
  - image: nginx
    name: nginx
    ports:
    - containerPort: 80
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
````

Commands to run:

````
 k get po
  369  k get no
  370  k get no --show-lable
  371  k get no --show-lables
  372  k get no --show-labels
  373  k label no kind-worker hdd=ssd
  374  k get po
  375  k get po -o wide
  376  cat pod.yaml
  377  vi pod.yaml
  378  k explain po.spec.affinity.nodeAffinity
  379  k explain po.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution
  380  k explain po.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms
  381  k explain po.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms.matchExpressions
  382  vi pod.yaml
  383  k get po
  384  k delete po nginx
  385  vi pod.yaml
  386  k apply -f pod.yaml
  387  vi pod.yaml
  388  k apply -f pod.yaml
  389  k explain po.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms.matchExpressions.operator
  390  vi pod.yaml
  391  k apply -f pod.yaml
  392  k get po
  393  k get po -o wide
  394  vi pod.yaml
  395  history
````

## Taint and Toleration

### Taint 

Add "LOCK" on the nodes


### Toleration

Provode key to pod

## Taint Effect

### No schedule

if taint and toleration is not matching, then dont schedule that pod on the node

### Prefer NO Schedule

if taint and toleration is not matching, then dont schedule that pod on the node. If there is nooption, then only you can schedule.

### no Execute

## Example:

yaml file 

````
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
    app: nginx
  name: nginx
spec:
  tolerations:
      -   key: hdd
          operator: Equal
          value: ssd
          effect: NoSchedule
  containers:
  - image: nginx
    name: nginx
    ports:
    - containerPort: 80
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
````
Commands ti run:

````
 396  vi pod.yaml
  397  k explain po.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms.matchExpressions
  398  k explain po.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms
  399  k explain po.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution
  400  k get no
  401  k describe no kind-worker
  402  k describe no kind-worker2
  403  k describe no kind-control-plane
  404  k taint no kind-worker hdd=ssd:NoSchedule
  405  k get no --show-labels
  406  k label no kind-worker hdd-
  407  k get no --show-labels
  408  k describe no kind-worker
  409  vi pod.yaml
  410  k apply -f pod.yaml
  411  k get po
  412  k delete po nginx
  413  k apply -f pod.yaml
  414  k get po -o wide
  415  k get no
  416  k cordon kind-worker2
  417  k get no
  418  k delete po nginx
  419  vi pod.yaml
  420  k apply -f pod.yaml
  421  k get po
  422  k describe po nginx
  423  k delete po nginx
  424  vi pod.yaml
  425  k apply -f pod.yaml
  426  vi pod.yaml
  427  k apply -f pod.yaml
  428  k get po
  429  k get po -o wide
````
#  DaemonSet

yaml file:

````
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd-elasticsearch
  labels:
    k8s-app: fluentd-logging
spec:
  selector:
    matchLabels:
      name: fluentd-elasticsearch
  template:
    metadata:
      labels:
        name: fluentd-elasticsearch
    spec:
      tolerations:
      # these tolerations are to have the daemonset runnable on control plane nodes
      # remove them if your control plane nodes should not run pods
      - key: node-role.kubernetes.io/control-plane
        operator: Exists
        effect: NoSchedule
      - key: node-role.kubernetes.io/master
        operator: Exists
        effect: NoSchedule
      containers:
      - name: fluentd-elasticsearch
        image: quay.io/fluentd_elasticsearch/fluentd:v2.5.2
````

Commands to run:

```

  431  cat pod.yaml
  432  k get po -n kube-system
  433  k get po -n kube-system -o wide
  434  k get ds -n kube-system
  435  vi ds.yaml
  436  k get all
  437  k delete po nginx
  438  k apply -f ds.yaml
  439  k get ds
  440  k get po
  441  k get po -o wide
  442  k get no
  443  k describe no kind-worker
  444  k taint no kind-worker hdd-
  445  k get no
  446  k uncordon kind-worker2
  447  k get no
  448  k get po
  449  k get po -o wide
  450  k get ds
  451  history
````
