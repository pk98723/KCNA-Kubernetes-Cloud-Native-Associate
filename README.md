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
