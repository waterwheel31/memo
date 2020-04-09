# Docker and Kubernetes


## Docker

<img src="./images/docker.png" width = 600>
(image from Udacity)


- 'Dockerfile' components:
    - 'FROM': Base image from Docker Hub
    - 'WORKDIR': set working directory
    - 'COPY': copying files from local to docker container (etc.)
    - `EXPOSE: expose port
    - 'RUN': commands to run when launched
    - 'CMD': commands to run in the end when launched (ex : `CMD ["python", "sample.py"]`)

 - Docker commands:  
    - To build dockaer container: `docker build -t <tag name> .`
    - To see docker containers: `docker image ls`
    - To run a docker container and enter it: `docker run -it <container name> bash ` 
    - To run a docker container at specific port: `docker run -p <port> <name> ` 
    - To push a container to AWS ECR 
        - Login  `(aws ecr get-login --no-include-email --region us-east-1)`
        - Build the container locally: `docker build -t <name> .` 
        - Register the container: `docker tag <name>:<registry unique URL>/<name>:latest`
        - Push: `docker push <register>/<name>:latest`
    - To see ports: `docker port <name>`

- Cloud Services for Docker
    - Amazon ECR (Elastic Container Registry)


## Makefile

- This is to run multiple shell codes in sequence 
- To run Makefile: `make <title in Makefile>` for example, 
    - `make install`
    - `make all`   

## Kubernetes 

 - Kubernates hierarchy 
    - cluster
        - Kubernates master w. Kubernates API
        - nodes 
            - pods (scaling is at this level)
                - containers 
 - examples of usage
    - one pod has application and another pod does monitoring
    - one node has application and another pod has database

 - install kubectl command: 
    - `curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl`
 - install minikube  
    - `sysctl -a | grep machdep.cpu.features` 
 - To start Kubernetes cluster: `minikubte start` 
 - To run: `kubectl run <name> --generator=<generator> --image=<image> --port=<port> -- labels app=<app>`
 - To forward `kubectl port-forward <app> 8000:80` 
 - To see available nodes: `kubectl get nodes` 
 - To see available pods: `kubetcl get pods` 
 - To see log: `kubectl logs <pod name>` 
 - To scale: `kubectl scale <deployment name> --replicas=<desired number of replicas>`


## Linux Commands 
   - To see the system info: `uname -a`
   - To write string in a file: `echo "Hello!" >> README.md` 
   - To see the location of a program: `which python3` 
   - `&&` do the next command if previous command is successful 
   - To make an alias: `alias vi='vim'`

## Linux key files
   - ~/.bashrc 
        - To activate: `source ~/.bashrc`

## Text editor
   -  `vim`
       - to exit: `:q`
   - `nano`

## Install libraries 
   - Python 
        - `pip install --ugprade pip`
        - `pip install -r requirements.txt` 
   - NodeJS
        -  XX

## Services/Tools 
- Prometheus: monitroing 
- Swagger: creation of API documentation
- LOCUST: load testing 


