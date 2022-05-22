# Service Demo

Refereed from [here](https://github.com/rskTech/serviceDemo)

Commands:

````
  git clone https://github.com/rskTech/serviceDemo.git
  cd serviceDemo/
  ls
  
  cd build/
  ls
  
  vi app.py
  ls
  
  cd ../deploy/
  
  vi db-pod.yml
  vi db-svc.yml
  
  vi web-pod.yaml
  vi web-svc.yml
  
  k get all
  k delete deploy first
  
  k get all
  
  k apply -f db-pod.yml
  k get po
  
  k apply -f db-svc.yml
  k get svc
  
  k apply -f web-pod.yaml
  k get po
  
  k apply -f web-svc.yml
  
  k get svc
  k get no -o wide
  
  curl 172.18.0.3:30908/init 200  curl -i -H "Content-Type: application/json" -X POST -d '{"uid": "1", "user":"John Doe"}' http://172.18.0.3:30908/users/add
  
  curl -i -H "Content-Type: application/json" -X POST -d '{"uid": "2", "user":"Rajendra"}' http://172.18.0.3:30908/users/add 202  
  
  curl 172.18.0.3:30908/users/1
  curl 172.18.0.3:30908/users/2

````
