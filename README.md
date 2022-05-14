# Docker-AWS-Kubernetes

1. Create AWS free account
2. Create EC2 - ubuntu instance. Create public & private key too.  Download key.
3. Download [MobaXtrem](https://mobaxterm.mobatek.net/download-home-edition.html)
  - MobaXterm Personal Edition v22.0 • (SSH client, X server and network tools)  
4. Setup SSH session and, Advanced SSH settings tab, add your key downloaded from AWS. click ok.
5. Steps inside concole
  
  ````
   apt update
   apt install docker.io
   docker --version
   docker info
  ````
6. make dir
   ````
   mkdir docker
   ````
8. Setup Python application 

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
