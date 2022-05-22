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
## Scaling

### Manual Scaling

### Automatic Scaling

Adjust replicas based on trafficload

- Horizontal pod auto scaler
- Specify: max space and min space utilization



