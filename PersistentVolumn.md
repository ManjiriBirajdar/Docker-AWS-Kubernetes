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

# Stateful 

More info: https://github.com/rskTech/k8s_material/tree/master/statefulset

````
 553  git clone https://github.com/rskTech/k8s_material.git
  554  cd k8s_material/statefulset/
  555  vi sfs.yaml
  556  k get pv
  557  k get pvc
  558  k get po
  559  k delete po nginx
  560  k delete pvc mypvc
  561  k delete pv mypv
  562  k get sts
  563  k apply -f sfs.yaml
  564  k get sts
  565  k get po
  566  k get pvc
  567  k get sc
  568  vi sc.yaml
  569  k apply -f sc.yaml
  570  k get po
  571  k get pvc
  572  vi sfs.yaml
  573  ls
  574  k apply -f pv.yaml
  575  k get pv
  576  k get pvc
  577  k get po
  578  k get pvc
  579  k apply -f pv1.yaml
  580  k get po
  581  k get pvc
  582  k apply -f pv2.yaml
  583  k get po
  584  k get pvc
  585  k get pv
  586  k get po
  587  k delete po web-1
  588  k get po
  589  k get pvc
  590  k scale sts web --replicas=5
  591  k get po
  592  k get pvc
  593  ls

````
