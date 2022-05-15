# Day 2: 

## Build Image 

````
docker build -t cognixia14may:1.0 . 

docker images

docker build -t cognixia14may:1.0 . 
````
-t is image name

: used for image version

. is used location of the Dockerfile / curruent directory.

image is ready. now we will create a container:

Parameters:

-d used to running container in background mode /process : deamon mode

--name name of the container / default or random name is possible when you leave it empty

-p is to specify hostport:applicationport

imagename

````
docker run -d --name second -p 8000:8080 cognixia14may:1.0

docker ps //only running containers

docker ps -a //both start n stop containers

docker stop //stop container

docker rm // stop container then remove container

docker imges
````

Notice the container id : ec2f84c71893b281debffbd7f68d3c65d0e8a032b720b5d52ca52d04caffccac

Now, access the application:

````
curl localhost:8000
````

Create second container for same image, then change the host port

````
docker run -d --name second -p 8001:8080 cognixia14may:1.0

docker ps
````
Get info about the usage of compute resources / for bench marking the app

````
docker stats
````
output:

````
CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT     MEM %     NET I/O           BLOCK I/O     PIDS

9805ee7d3383   second    0.11%     36.44MiB / 967.9MiB   3.77%     1.01kB / 0B       73.7kB / 0B   3

ec2f84c71893   first     0.11%     38.14MiB / 967.9MiB   3.94%     2.36kB / 1.38kB   3.53MB / 0B   3
````

See logs of the container:
````
docker logs first
````

## Inside docker container

````
docker exec -it first bash
````

Use following command to come out of container
````
exit
````

## Removing imgage

````
docker images

docker stop containername

docker rmi containerid

````
## Command dump

````
docker ps -a
docker stats
docker logs first
docker exec -it first bash
docker ps
docker ps -a
docker stop first
docker ps -a
docker rm first
docker ps -a
docker images
docker rmi ec2f84c71893
docker images
docker tag cognixia14may:1.0 rajendrait99/cognixia14may:1.0
docker images

docker login
docker push rajendrait99/cognixia14may:1.0
docker pull rajendrait99/cognixia14may:1.0
````

## push and pull to [Docker Hub](https://hub.docker.com/)

````
docker images
docker tag cognixia14may:1.0 rajendrait99/cognixia14may:1.0
docker images

docker login
docker push rajendrait99/cognixia14may:1.0
docker pull rajendrait99/cognixia14may:1.0
````

# Docker volumes

EC2 --> container --> tmp storage   //stateless 

Mount host machine path to the container // state

From host machine , we attach storage/volumn to the container

paramerter:

-v storagepath

````
docker ps -a
docker exec -it second bash
docker stop second
docker rm second

docker run -d --name second -p 8000:8080 rajendrait99/cognixia14may:1.0

docker exec -it second bash
docker stop second
docker rm second

docker run -d --name second -p 8000:8080 -v /opt:/etc/lala rajendrait99/cognixia14may:1.0

ls /opt/
rm /opt/abc.txt
ls /opt/

docker run -d --name second -p 8000:8080 -v /opt:/etc/lala rajendrait99/cognixia14may:1.0

docker exec -it second bash

ls /opt/

docker stop second
docker rm second

ls /opt/

docker run -d --name second -p 8000:8080 -v /opt:/etc/lala rajendrait99/cognixia14may:1.0

docker exec -it second bash

````

# Docker Networking

## Command dump

````
docker ps -a
docker stop second
docker rm second

docker ps -a

docker network ls

ifconfig

docker network ls

docker network inspect bridge

ifconfig

docker run -d --name second -p 8000:8080 -v /opt:/etc/lala rajendrait99/cognixia14may:1.0

docker network inspect bridge

ifconfig

docker run -d --name training -p 8001:8080 -v /opt:/etc/lala rajendrait99/cognixia14may:1.0
docker network create mynet --subnet 192.168.0.0/16

docker network ls

docker network inspect mynet

ifconfig

docker run -d --name training -p 8001:8080 -v /opt:/etc/lala --network mynet rajendrait99/cognixia14may:1.0
docker network inspect mynet

docker exec -it second bash

docker network connect mynet second

docker exec -it second bash

````















































