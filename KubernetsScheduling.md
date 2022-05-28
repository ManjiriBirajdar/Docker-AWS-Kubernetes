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
