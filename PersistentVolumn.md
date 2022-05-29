# Static Persistent Volumn (PV)

Attatch/bind persistent volumn to the pod

Creating volumns using existing storage providers e.g. Amenzon, Azure, Elastic, NFS, etc

For every pod, we need to create pvc file.

yaml file:

Example 1

````
apiVersion: v1
kind: PersistentVolume
metadata:
   name: mypv
spec:
   accessModes:
       - ReadWriteMany
   storageClassName: normal
   capacity:
         storage: 1G
   hostPath:
         path: /opt

````

Example: 2

````

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
   name: mypvc
spec:
    accessModes:
            - ReadWriteMany
    storageClassName: normal
    resources:
            requests:
                    storage: 1G
````

Example 3:

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
          persistentVolumeClaim:
                  claimName: mypvc
status: {}

````

Commands to run:

````
  524  vi pv.yaml
  525  k explain pv.spec
  526  k explain pv.spec.awsElasticBlockStore
  527  k explain pv.spec.nfs
  528  vi pv.yaml
  529  k get pv
  530  k get pvc
  531  k apply -f pv.yaml
  532  k get pv
  533  vi pvc.yaml
  534  k get pv
  535  k apply -f pvc.yaml
  536  k  get pv
  537  k get pv
  538  k get pvc
  539  vi pod.yaml
  540  k get po
  541  k delete po nginx
  542  k apply -f pod.yaml
  543  k get po
  544  k exec -it nginx bash
  545  history
  
````

# Dynamic Volumn Provision

On-demand storage creation

## Object --> Storage class --> provisioner (storage provider specifics)

Steps:

- Every storage provider shares their provisioner.
- For each pod, we create pvc.
- Based on attributes in pvc, the storage with specific volumn is created.

Provisioner : Automation job/script which will create a storage with specifc volumn

More info: https://kubernetes.io/docs/concepts/storage/storage-classes/


