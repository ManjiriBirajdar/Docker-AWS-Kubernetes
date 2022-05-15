# Day 2: 

## Build image 

-t is image name
: used for image version
. is used location of the Dockerfile / curruent directory

````
docker build -t cognixia14may:1.0 . 

docker images

docker build -t cognixia14may:1.0 . 
````

image is read. now we will create a container

-d used to running container in background mode /process : deamon mode
--name name of the container / default or random name is possible when you leave it empty
-p is to specify hostport:applicationport
imagename

````
docker run -d --name second -p 8000:8080 cognixia14may:1.0

docker ps

docker ps -a

````
Notice the container id : ec2f84c71893b281debffbd7f68d3c65d0e8a032b720b5d52ca52d04caffccac

Now, access the application

````
curl localhost:8000
````

Create second container for same image, then change the host port

````
docker run -d --name second -p 8001:8080 cognixia14may:1.0
````





