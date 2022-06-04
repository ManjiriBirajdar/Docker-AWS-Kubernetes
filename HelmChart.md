# Helm Chart

https://github.com/rskTech/k8s_material/tree/master/helm

````

  774  kind delete cluster
  775  kind create cluster --config config
  776  cd k8s_material/
  777  ls
  778  cd statefulset/
  779  ls
  780  vi sfs.yaml
  781  cd
  782  vi deploy.yaml
  783  ls
  784  rm -rf myapp/
  785  helm create myapp
  786  ls
  787  cd my
  788  cd myapp/
  789  ls
  790  vi Chart.yaml
  791  rm values.yaml
  792  cd templates/
  793  rm -rf *
  794  ls
  795  cd ..
  796  ls
  797  cd charts/
  798  cd ..
  799  rm -rf charts/
  800  ls
  801  cd templates/
  802  ls
  803  cp ../../deploy.yaml .
  804  vi deploy.yaml
  805  vi ../values.yaml
  806  vi deploy.yaml
  807  vi ../values.yaml
  808  vi service.yaml
  809  vi ../values.yaml
  810  cd ..
  811  helm template myapp myapp/
  812  helm list
  813  helm install myapp myapp/
  814  k get all
  815  alias k=kubectl
  816  k get all
  817  k get no -o wide
  818  curl 172.18.0.3:30939
  819  helm list
  820  helm uninstall myapp
  821  k get all
  822  history
  
````

````
myapp:
     name: myapp
     replicas: 5
     image: nginx:latest
     port: 80
     type: NodePort
````

````
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: {{.Values.myapp.name}}
  name: {{.Values.myapp.name}}
spec:
  replicas: {{.Values.myapp.replicas}}
  selector:
    matchLabels:
      app: {{.Values.myapp.name}}
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: {{.Values.myapp.name}}
    spec:
      containers:
      - image: {{.Values.myapp.image}}
        name: {{.Values.myapp.name}}
        ports:
        - containerPort: {{.Values.myapp.port}}
        resources: {}
status: {}
````

````
apiVersion: v1
kind: Service
metadata:
     name: {{.Values.myapp.name}}
spec:
     type: {{.Values.myapp.type}}
     selector:
         app: {{.Values.myapp.name}}
     ports:
         - port: {{.Values.myapp.port}}
           targetPort: {{.Values.myapp.port}}
````
