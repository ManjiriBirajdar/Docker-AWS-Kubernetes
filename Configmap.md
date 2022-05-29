# Configmap

Application configuration file

e.g. Database username password is mentioned in app config file rather than hardcoding it in application

## Two ways to create configmap

### 1. from-literal

Applicable for 1-2 config map files

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
### 2. Filw with multiple config file inside

Applicable for several config map files

