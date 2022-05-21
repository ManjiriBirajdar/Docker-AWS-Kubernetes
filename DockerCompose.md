# Docker Compose

## why we need ocker compose

if you wanna run several micro-services

Example: 11 micro services.

So, to run 1 micro-service, you need to run following 4 commands:
````
build 
run
push
pull
````

Also, need to remember sequence with all dependencies.

E.g. Database--> UI

---> Solution: docker compose utilities

- it is in yaml format


# Hands-on Example

1. Conainer with Service 1: Web
UI

2. Container with Service 2: REDIS DB

- it basically increments the object counter.
- We write our own Dockerfile, requirements.txt, app.py

## Docker Compose File

yaml Format:

````
version: "3.9"
services:
  web:
    build: .
    ports:
      - "8000:5000"
    network:
      - mynet
    links:
      - redis
  redis:
    image: "redis:latest"
    ports:
      - "6329"
    networks:
      - mynet

networks:
    mynet
````
