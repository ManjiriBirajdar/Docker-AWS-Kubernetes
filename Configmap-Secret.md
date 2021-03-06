# Configmap

Application configuration file

e.g. Database username password is mentioned in app config file rather than hardcoding it in application

## Two ways to create configmap

### 1. from-literal

Applicable for 1-2 config map files

Add following attribute in yaml file:

````
env:
      - name: DBHOST
        valueFrom:
                configMapKeyRef:
                        name: mycm
                        key: dbhost
      - name: DBPASS
        valueFrom:
                configMapKeyRef:
                        name: mycm
                        key: dbpass
````

Edited yaml file:

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
  containers:
  - image: nginx
    name: nginx
    ports:
    - containerPort: 80
    resources: {}
    env:
      - name: DBHOST
        valueFrom:
                configMapKeyRef:
                        name: mycm
                        key: dbhost
      - name: DBPASS
        valueFrom:
                configMapKeyRef:
                        name: mycm
                        key: dbpass
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}

````

After that, Run following commands:

````

  487  alias k=kubectl
  488  k get no
  489  kind delete cluster
  490  ls
  491  kind create cluster --config config
  492  k get no
  493  k get cm
  494  k create cm mycm --from-literal=dbhost=192.168.0.2 --from-literal=dbpass=admin
  495  k describe cm mycm
  496  vi myconfig
  497  mv myconfig myconfig.ini
  498  k create cm mycm1 --from-file=myconfig.ini
  499  k describe cm mycm1
  500  cd k8s/
  501  ls
  502  vi pod.yaml
  503  k apply -f pod.yaml
  504  k get po
  505  k exec -it nginx bash
  506  history

````
### 2. File with multiple config file inside

Applicable for several config map files

Add **volumeMounts:** attribute to yaml file:

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
  containers:
  - image: nginx
    name: nginx
    ports:
    - containerPort: 80
    resources: {}
    volumeMounts:
            - name: myvol
              mountPath: /etc/foo
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  volumes:
        - name: myvol
          configMap:
                  name: mycm1
status: {}

````

# Secret

Encode data. e.g. passwords

Data will be displayed in encoded format not in plain text (as in configmap).

Use secret key refrence

For multiple secrets, keep a file

````
k create secret generic mysecret --from-literal=dbpass=admin


configMapKeyRef  => secretKeyRef

configMap => secret

````
