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

## Components required on every node

### Master

### API server

### etcd 
Nosql database

###  Scheduler

### Controller

- Responsible for high availability
- Communicates with API server for getting info about pods based on lable
- Replication management
- Assures no downtime

### Kubelet Docker

### Pod

### Kubeproxy

Take cares of Network functionally

### CNI (Container Network Interface)

Pod needs networking capability. 
Communicates all details of the pods, 

## Objects

Each object file is yaml file

### deployment


# Communication
