# Docker-AWS-Kubernetes

1. Create AWS free account
2. Create EC2 - ubuntu instance. Create public & private key too.  Download key.
3. Download [MobaXtrem](https://mobaxterm.mobatek.net/download-home-edition.html)
  - MobaXterm Personal Edition v22.0 • (SSH client, X server and network tools)  
4. Setup SSH session and, Advanced SSH settings tab, add your key downloaded from AWS. click ok.
5. Steps inside ssh concole to install docker and check if its installed correctly:
  
  ````
   apt update
   apt install docker.io
   docker --version
   docker info
  ````
6. Next, make directory "docker" 
   ````
   mkdir docker
   ````
8. Next, we will dockerise tehe above python application in **docker image**
9. Setup Python application by creating app.py file

````
vi app.py
````

copy the following app code in the file and save:

````
from flask import Flask 
import os 
app = Flask(__name__) 
@app.route('/') 

def hello(): 
    return ('\nHello from Container World! \n\n')

if __name__ == "__main__": 
    app.run(host="0.0.0.0", port=8080, debug=True)
````
7. create Docker file using

````
vi Dockerfile
````

and add the following dependencies into Dockerfile for running the app:

````
RUN apt update && apt install python3 -y && apt install python3-pip -y
RUN pip3 install flask
COPY app.py /tmp
EXPOSE 8080
CMD ["python3", "/tmp/app.py"]

````
