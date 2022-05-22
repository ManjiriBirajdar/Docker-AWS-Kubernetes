# Container Orchestration

- Bring more Scalability to the solution
- Provide Availability
- Handle complex Deployment
- Manage everything, scheduling, auto creation, scale up and scale down solution

## Existing solutions based on kubernetes (paid services)

- Docker Swarm
- OpenShift
- AKS
- GKE

# Kubernetes Architecture

<img src="https://github.com/ManjiriBirajdar/Docker-AWS-Kubernetes/blob/main/kubernetes%20architecture.JPG"/>

[More info](https://kubernetes.io/docs/concepts/overview/components/)

# Components (required on every node)

## Master

## API server

## etcd 
Nosql database

##  Scheduler

## Controller

- Responsible for high availability
- Communicates with API server for getting info about pods based on lable
- Replication management
- Assures no downtime

## Kubelet Docker

## Pod

## Kubeproxy

Take cares of Network functionally

## CNI (Container Network Interface)

Pod needs networking capability. 
Communicates all details of the pods, 

## Objects

# Cluster Creation Tools

## KIND - K8S inside Docker ( used for CI-CD)
(on single machine)

- Multi-node cluster: to create a multi node cluster on single machine
- master-worker creation

## Kubeadm
(multiple physical machines or virtual machines)

# Demonstration 

## Pod creation

````
docker ps -a
kubectl get no
alias k=kubectl
k get all
k delete po nginx
k run first --image=rajendrait99/cognixia14may:1.0 --port=8080

k get po
k get po -o wide

k describe po first

k get po
k logs first
k exec -it first bash
k get po
k delete po first
k get po
````

## Deployment

````
k get po

k create deploy first --image=nginx:latest --port=80 --dry-run=client -o yaml > deploy.yaml

vi deploy.yaml
k explain deploy
k explain deploy.spec
k explain deploy.spec.template
k explain deploy.spec.template.spec
k explain deploy.spec.template.spec.containers

vi deploy.yaml
k apply -f deploy.yaml

k get all
k get po

k delete po first-586f8c4b58-bsf5p

````

## Scaling

### 1. Manual Scaling

How to increase available pods to 10? 

Existing pods are 2. 
So, after running following commands, 8 new pods will be created and will be running.

````
k get po
k get all

k scale deploy first --replicas=10

k get po
k get po -o wide

````
### 2. Automatic Scaling (HPA : Horizontal Pod Autoscale)

Adjust replicas based on trafficload

- Horizontal pod auto scaler
- Specify: max space and min space utilization

So, Depending on the traffic load,  

Min : 2 pods
Max : 10 pods

will be used to scale up or scale down the replicas.

````
k get po -o wide

k autoscale deploy first --cpu-percent=80 --min=2 --max=10

k get hpa

//delete

k delete hpa first
````
### 3. Zero downtime upgrade 

Load balancer : distribute traffic to multiple pods

deployment -->
    RC(replica) = 2

If UI needs to be updated, then we can use replica feature

````
k get all
k delete hpa first
k get all

k describe pod/first-586f8c4b58-qxrps

k scale deploy first --replicas=20
k get po

k set image deploy first nginx=nginx:1.7.8
k rollout history deploy first
k rollout status deploy first

k set image deploy first nginx=nginx:1.7.8 --record
k rollout status deploy first
k get po

k rollout status deploy first
k get po

k describe po first-57b49bc5c7-xt8kq

k rollout history deploy first

k set image deploy first nginx=nginx:1.7.9 --record

k rollout history deploy first
k get po
k get all

k rollout history deploy first

k rollout undo deploy first  --to-revision=2

k rollout history deploy first

k get po
k describe po first-57b49bc5c7-zrp4h

````

# Service Object

we cant expose our pod directly to any one as it can change its config in cluster e.g. if one pod replica fails, then scheduler might run it on some other part of cluster.

## NodePodt

external user to pod communication

## Clusterip service

pod to pod communication within one cluster

## Load Balance service

- only if you wanna use third-party load balancer or your own
- AWS load balancer service
- own load balancer service
