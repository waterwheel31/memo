# Linxus Shell, Docker and Kubernetes



## Linux/Shell  

### Useful commands
   - To see processes: `sudo lsof -i`
   - To see the system info: `uname -a`
   - To write string in a file: `echo "Hello!" >> README.md` 
   - To see the location of a program: `which python3` 
   - `&&` do the next command if previous command is successful 
   - To make an alias: `alias vi='vim'`
   - To add execution permisssion `chmod +x <file>`
   - To unzip: `tar zxvf <file>` 
   - To check disk usage:
      - `df -h`
      - `ncdu` (needs install)
   - To run shell file
      - `bash file.sh` or `sh file.sh` or 
      - `chmod +x ./file.sh && ./file.sh` 
   - Shell file needs following string at the beginning `#!/bin/bash` (shebang)
   - To see all the processes: `ps x`
   - To kill a processes: `kill <process id>`
   - To run a process background (continue after closing the terminal): `nohup <command> &`
   - To run sudo command for a user `sudo -u USERNAME whoami `

### Makefile

- This is to run multiple shell codes in sequence 
- To run Makefile: `make <title in Makefile>` for example, 
    - `make install`
    - `make all`   

### Linux key files
   - ~/.bashrc 
        - To activate: `source ~/.bashrc`

### Text editor for Linux
   - vim
       - to exit: `<esc> + :wq` (with save)
   - nano
       - to exit: `<ctrl> + x`


### SSH 


## Kuberntes Deployment with Jenkins

- Installation and Initial Setup
   - Update package: `sudo apt update`
   - Intall Java SDK:  `sudo apt install -y default-jdk`
   - wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -

   - sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
   - sudo apt-get update
   - sudo apt-get install jenkins
   - Start Jenkins server: `sudo systemctl start jenkins` 
   - Access to port 8080
   - Copy and paste password: `sudo cat <path shown on GUI>` 
   - Click `Install suggested plugins` 
   - Install Blue Ocean: Manage Jenkins -> Manage Plugins -> Available Tab -> and Install followings 
      - Blue Ocean
      - Blue Ocen Pipeline Editor
      - Blue Ocean Executor Info
      - Display URL for Blue Ocean
      - Config API for Blue Ocean
      - Events API for Blue Ocean
      - Git Pipeline for Blue Ocean
      - GitHub Pipeline for Blue Ocean
      - AWS CodeDeploy
      - AWS CodeBuild
      - Http Request
      - File Operations
   - Install AWS plugin. The same as previous step to install: 
      - Pipeline AWS Steps
   - Setting github for BlueOcean
      - Open BlueOcean from Jenkins menu
      - Create new pipleline
      - Choose Github 
      - Add access token
   - Add IAM permission to a user `jenkins` (see AWS user guide https://docs.aws.amazon.com/ja_jp/systems-manager/latest/userguide/automation-jenkins.html) 
   - Add PATH to Jenkins (otherwise `aws` command does not work)
      - at Mangae Jenkins > System Configuration > Global Properties
         - KEY: PATH+EXTRA
         - VALUE: /usr/local/bin
   - Modify sudo on the server
      - `sudo visudo`
      - `root    ALL=(ALL:ALL) ALL`
      - `jenkins ALL=(ALL) NOPASSWD:ALL`
      - then restrat jenkins: ``sudo systemctl restart jenkins` 
- Triggering
   - Change the frequency of triggering
- Blue-Green deployment
   - Install tools 
      - Ansible: `apt install ansible`
      - Boto: `pip install boto` 
      - CloudBees (Jenkins pugin `CloudBees AWS Crednetials Plugin`)
   - Configure AWS Crednetials in Jenkins
         - add IAM access ID and access secret key to Global credentials
   - Map the credentials in the Jenkins pipeline
   - Setup cluster with eksctl (for AWS)
      - `curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp`
      - `sudo mv /tmp/eksctl /usr/local/bin`
      - `eksctl version`
      - Install kubectl:
         -  `curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl` 
         - `chmod +x ./kubectl`
         - `sudo mv ./kubectl /usr/local/bin/kubectl`
         - `kubectl version --client` 
         - reference: https://kubernetes.io/docs/tasks/tools/install-kubectl/
         - add permission to the AWS user
               -  ```{
                  "Version": "2012-10-17",
                  "Statement": [
                        {
                              "Sid": "eksadministrator",
                              "Effect": "Allow",
                              "Action": "eks:*",
                              "Resource": "*"
                        }
                     ]ws
                  }```
         - intall aws cli `pip install awscli --upgrade --user`  (by installing from apt may cause error. In that case, remove awscli from apt)
         - configure AWS CLI crendentials: `aws configure` 
   - Create cluster 
      - `eksctl create cluster 
            --name prod 
            --region us-east-1
            --fargate
            --zones us-east-1a,us-east-1b
      - (wait for 15 minutes)

      - update config ` aws eks update-kubeconfig --name clustername --region us-east-1` 
      - `kubectl get svc` 
      - Deploy to Kuberntes Cluster: `kubectl apply -f setting.yaml`
         - yaml file is to create (if not exist) or update the resources in a cluster
      - Check 
         - pods: `kubectl get pods` 
         - developyment: `kubectl get deployment`
         - services: `kubectl get serivces`
         - replicaset: `kebectl get replicaset`
      - Expose `kubectl expose deployment devopscapstone --type=ClusterIP --name=devopscapstone`

   - Make Jenkinsfile. Inside that, typically:
      - Do linting: `sh 'tidy xxxx'` 
      - Build image: 
            - withCredentials()
            - `sh  'docker build -t xxxxxx/xxxxxx:xxxx'`
      - Push image: 
            - withCredentials()
            -`sh 'docker login -u   docker push xxxxx/xxxxxx:xxxxxx'`
      - Set current cluster context:
            - withAWS()
         -  `sh 'kubectl config use-context arn:aws:eks:us-east-1:xxxxx:xxxx/xxxxx'` 
            -  Each context has: cluser, namespace, user
      - Expose container
            - withAWS()
            - `sh 'kubectl expose deployent xxxxx --type=LoadBalancer --port=80'`
      - Domain redirect
            - withAWS()
            - `sh 'aws route53 change-resource-record-sets --hosted-zone-id XXXXX --change-batch file://xxxxxx.json'`


   - Reference
      - https://www.youtube.com/watch?v=eHvKc6hNmhI
      - https://medium.com/@andresaaap/jenkins-pipeline-for-blue-green-deployment-using-aws-eks-kubernetes-docker-7e5d6a401021 

- 



--- 

## Docker

<img src="./images/docker.png" width = 600> <br>
(image from Udacity)


### 'Dockerfile' components:
   - 'FROM': Base image from Docker Hub
   - 'WORKDIR': set working directory
   - 'COPY': copying files from local to docker container (etc.)
   - `EXPOSE: expose port
   - 'RUN': commands to run when launched
   - 'CMD': commands to run in the end when launched (ex : `CMD ["python", "sample.py"]`)

###  Docker commands:  
   - To build a dockaer container: `docker build -t <tag name> .`  (do not forget the last dot '.')
   - To see docker images: `docker image ls`
   - To see docker containers: `docker ps`
   - To run a docker container and enter it: `docker run -it container name> bash ` 
   - To exit from a docker conatiner: `exit`  
   - To run a docker container at specific port: `docker run -p <port> <name> ` To remove all containers  `docker rm $(docker ps -aq)`
   - To push a container to AWS ECR 
      - Login  `(aws ecr get-login --no-include-email --region us-east-1)`
      - Build the container locally: `docker build -t <name> . --no-cache` 
      - create repository 
         `aws ecr create-repository \
            --repository-name sample-repo \
            --region us-east-1`
      - Register the container: `docker tag <image id> <registry unique URL>/<name>:latest`
      - Push: `docker push <register>/<name>:latest`
   - To see ports: `docker port <name>`
   - To remove `docker system prune`

--- 

## Kubernetes 

### Basic understandings 
 - Kubernetes does:  
      - Secure high availability and auto-scaling
      - manage container health 
      - manage secrets and configuration 
      - is open-source and little vendor lockin 
 - Kubernates hierarchy 
    - cluster
        - Kubernates master:  w. Kubernates API
        - nodes 
            - pods (scaling is at this level)
                - containers 
 - examples of usage
    - one pod has application and another pod does monitoring
    - one node has application and another pod has resources(database)

### Components 
   - Deployment: recipe for creating Pods (copies of application)
   - Service: internal load balancer that routes the traffic to Pods
   - Ingress: Description to define the traffic flow from outside

### Useful commands
 - to run kubernetes
      - on local env: use `minikube` 
      - on cloud: EKS(Amazon), GKE(Google), AKS(Azure)
 - to install kubectl command: 
    - sudo apt-get update && sudo apt-get install -y apt-transport-https
    - curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
    - echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
    - sudo apt-get update
    - sudo apt-get install -y kubectl

 - to install minikube (this is to run clusters locally) 
    - `sysctl -a | grep machdep.cpu.features` 
 - To start minikube: `minikubte start` 
 - To get cluster-info: `kubectl cluster-info`
 - To run: `kubectl run <name> --generator=<generator> --image=<image> --port=<port> -- labels app=<pod name>`
 - To forward `kubectl port-forward <app> 8000:80` 
 - To see available nodes: `kubectl get nodes` 
 - To see available pods: `kubetcl get pods` 
 - To get a list of deployed apps: `kubectl get deployments`
 - To see log: `kubectl logs <pod name>` 
 - To check status of pods (incl. error messages): ` kubectl describe pods` 
 - To scale: `kubectl scale deployments/<deployment name> --replicas=<desired number of replicas>`
 - To get inside `kubectl exec -ti <podname> bash` 
 - Contexts
      - `kubectl config get-contexts`
      - `kubectl config use-context $CLUSTER_NAME`
      - `kubectl config current-context`
 - To see the status of a pod
      -  `kubectl logs <podname>`
      -  `kubectl describe pod <podname>`
 - To create/update `kubectl apply -f config.yaml` 
      - The yaml file contains:
         - apiVersion
         - kind
         - metadata
         - spec 
### Reference

 - Official website has good tutorial https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-interactive/


--- 

## Install libraries 
   - Python 
        - `pip install --ugprade pip`
        - `pip install -r requirements.txt` 
   - NodeJS
        - `npm install` or `yarn install`

--- 

## Userful services/tools 
- Prometheus: for monitoring Kubernetes. 
    - to setup
       - download executable from prometheus website
       - untar on VM (ex. EC2, Cloud9)
       - go to the prometheus directory 
       - open up inbound port (default 9090) of the VM 
       - run prometeus: `./prometheus --config.file=prometheus.yml` 
       - access to `<VM's IP address>:9090/metrics` to see metric
   - to add metric: 
       - `<VM's IP address>:9090/graph`
       - choose metric at `expression` and `execute`

- Swagger: creation of API documentation
- LOCUST: load testing 
- Hadolint 
   - to install 
       `sudo wget -O /bin/hadolint https://github.com/hadolint/hadolint/releases/download/v1.17.5/hadolint-Linux-x86_64` 
       `sudo chmod +x /bin/hadolint`
- CircleCI: automatice testing
   - `curl -fLSs https://circle.ci/cli | bash` 
- Cloud Services for Docker
    - Amazon ECR (Elastic Container Registry)
   


