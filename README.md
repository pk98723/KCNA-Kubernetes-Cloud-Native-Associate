# KCNA-Kubernetes-Cloud-Native-Associate

KCNA - Kubenetes and Cloud_Native Associate

Containers
- What is a container

Most important example of container is DOCKER

- Lets say we have a webserver(Node express), Database(Mongo DB), Messaging service and Orchestration(Ansible) have to host on a VM to serve the requirement.
- At times there will be compatibility issues among these services with underlying hardware infra or OS or Libraries of the application.

How to solve
- With Docker we can run the apps severatly with their own Library and Depenendents.
- So containers are completly isolated environments as in they can have their own processes, networks, mounts etc., which will be compatible with underlying OS and hardware.
- Docker ulizes LXC type containers.

Operating System
- Lets say we have differnt OS like Fedora, SUSE, Ubuntu or CentOS all consist of 2 things a set of softwares and OS Kernel.
- The OS kernel is responsible for interacting with underlying Hardware while the OS kernel remains the same like Linux the softwares above it will make the OS different.

Sharing the Kernel
- We can run Docker with OS hosted on it with one underlying OS Kernel.
Ex: I have one OS with Ubuntu as base and on it i have hosted Docker. On this docker we can run mutlitple Linux OS systems like Suse, Fedora etc.,
- But we cannot run Windows OS on the same Docker as the underlying OS is Linux. For this we need Docker on Windows OS.
- Docker is not meant to run mutliple OS on the same hardware. 
- The main purpose of the Docker is to containerize them and to ship them & run.

Container vs Virtual machines

Containers
- On one docker we can run multiple container so that means utilization will be less w.r.t CPU & MEM.
- The space occupied per container will be less and when booting up it will be fast and quick.

Virtual machines
- On one Hypervisor, we can run multiple OS and multiple virtual machines so it means utilization will be more w.r.t CPU & MEM.
- The space occupied per VM on the Hardware infra will be more compared to container and when booting up it will be slow compared with containers.

How is it done?
- To run any application on the docker like ansible, mongodb, redis, nodejs you need to simply run

docker run ansible
docker run mongodb
etc

Container vs image
- From an image, containers will be build. In simple words image is a package template.
- We can create own own image and make it available to public to use.

Container Advantage
- Developer will create a docker file and share it with operations team to use it.
- Previously when there was no docker image, developers use to give a setup file along with it a document on how to run it and at times to fix any issues or if any issues are faced during installation often Developers are contacted by operations team to fix the issue which is time taking process.

Install Docker
- Build a VM in Linux Ubuntu2204 version
- Enable Outbound connectivity on port 22 to login to VM
- Install putty 64 bit
- Login to Linux VM using putty with the public IP on port 22
- Once login, shift to root login using below command
-> sude su
- Once Root login is enabled install docker using below command
-> apt-get install docker.io
NOTE: Incase you get below error then run -> "apt-get update" to get the latest packages then try to install docker.io 
" root@myvm:/home/azureuser# apt-get install docker.io
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package docker.io is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source
"
  
- The above command will install docker on the VM locally to use
- Once docker is installed check the version of docker installed
-> docker version

Container Orchestration
- A platform that controls, maintains application within varies docker containers under single roof is called Container Orchestration.
- Few examples of Orchestration tech are
* Docker Swarm
* Kubernetes
* MESOS

Kuberneste Advantages
- Highly Available
- User traffic is maintained by loadbalancer
- Nodes will be created and destroyed on demand based on the declarative object oriented file

Kubernetes Architecture

Node: (minions)
- Is a machine physical or virtual on which Kubernetes is installed.
Cluster:
- A group of Nodes is called Cluster
- When a node fails other node will take and manage load of the application
Master:
- Master manages a cluster like moving a failed nodes load onto worker node
- It is responsible of actual orchestration on Kubernetes

Components:

- API Server
  Frontend for Kubernetes
  All talk to API server for communication
- etcd
  Its Key-Value store
  It is responsible for implementing logs between cluster
- Kubelet
  It is an agent which runs on each node/cluster
  It is responsible to make sure containers are running on nodes as expected
- Container runtime
  It is the underlying softwares to run containers
  Ex: Docker
- Controller
  The brain behind orchestration
  It makes decision to bring up the container/nodes goes down
- Scheduler
  Responsible for distributing work or containers across multiple nodes
  It will find the new/idle containers and assign to nodes

Master vs Worker Nodes

In Master we have Kube-apiserver which will in in communication with Kubelet on the worker
All the data received from kubelet to kube-apiserver will be stored in etcd in key-value format
Along with kube-apiserver, etcd a master node has Controller and Scheduler on it.
In worker node we have Container Runtime along with Kubelet. Generally Docker is the container runtime.

Kubeclt

It is a command line utility.

To get the cluster information, status of other nodes in the cluster, few commands below

-> kubectl run hello-minikube
-> kubectl cluster-info
-> kubectl get nodes

CRI  - Container runtime interface

-  It is an API that enables a container runtime with other vendors like Rkt, Containerd etc., but by default it is docker.
-  The CRI defines the gRPC protocol that the Kubernetes Kubelet users o interact with container runtimes
- Dockershim as introduced to bypass CRI and work with kubernestes to continue work with Docker images.

Docker vs ContainerD

- Initially Docker is the only container which is more popularly used.
- Later Kubernetes came into picture and started orchestrating Docker even though there are containers like rkt etc.,
- But users came forward stating they wanted to use other containers as well. So Container Runtime Interface (CRI) was introduced which allows Kubernetes to interact and work with non docker containers. But these non docker container should be inline with OCI (Open Container Initiative standards.
- Basically OCI consists imagespec and runtimespec
- imagespec defines on how images specifically build.
- runtimespec defines the any container runtime specifications are developed


POD

- Kubernetes does not install application(container) directly on a workernode
- Application is installed on a POD
- Pod is smallest unit in Kubernetes
- In a single Pod we can have multiple containers but multiple containers should be not same kind.
- Helper containers - At times, we might need another container called helper container to process some user data or file etc.,
- If a container fails then helper container will also deleted.
- container and helper container will communicate via network thru local host and also shares same storage. 

Installing Kind (Kubernetes IN Docker) on Linux VM

- Command to download latest Kind version 
-> curl -Lo ./kind https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64

- Command to make binary executable
-> chmod +x ./kind

- Command to move your system PATH
-> mv ./kind /usr/local/bin/kind

- Command to verify Kind Installation
-> kind version

- Command to install a Cluster in kind
-> kind create cluster

- Command to install Kubectl
-> snap install kubectl --classic

- Command to get "kind" cluster info
-> kubectl cluster-info --context kind-kind

- Command to get Nodes in the Kind cluster
-> kubectl get nodes

- Command to create a image on a pod
-> kubectl run nginx --image=nginx

- Command to know the running pod details
-> kubectl get pod

- Command to describe pod details
-> kubectl describe pod

- Command to know more details of running pod
-> Kubeclt det pod -o wide



