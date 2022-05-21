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

- Multi-node cluster: to create a multi node cluster on single machine
- master-worker creation

## Kubeadm
