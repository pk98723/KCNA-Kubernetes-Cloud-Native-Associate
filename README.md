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


POD with YAML

YAML in Kubernetes
- A structure of YAML contains 4 root level properties
apiVersion
kind
metadata
spec
- apiVersion: is version of Kubernetes api used to create objects. Ex: apiVersion: v1
Some example of apiVersion are
POD - v1
Service - v1
ReplicaSet - apps/v1
Deployment - apps/v1

- kind: represents the type of object when we create. Ex: Pod/Service/ReplicaSet/Deployment

- metadata is data about the object
Ex:
metadata:
  name: myapp-pod
  labels:
    app: myapp
    type: front-end

- spec: is a dictonary
Ex:
spec:
  containers:
    - name: nginx-container
      image: nginx

Final Yaml:

apiVersion: v1
kind: Pod
metadata:
  name: mypod1
  labels:
    app: app1
    type: front-end
spec:
  containers:
    - name: nginx-container
      image: nginx

- In Linux console, type below command to create yaml file
nano pod-definition.yml

- Copy & paste or write the above yaml code in the file
- Click ctl + o to save the file, hit enter
- Click ctl + x to exit the editor

- Using below command, we can build the pod

kubectl create -f pod-definition.yml
or
kubectl apply -f pod-definition.yml


 ReplicationController & ReplicaSets:

- Helps to run application even if the one is pod is failed, immediately new pod will be deployed.
- Also helps to load balances when existing pods are over utilized in a node and there is more demand then the load will be shared with another node where there is bandwidth.

Lets create a Yaml file to deploy replication controller with rc.definition.yml

apiVersion: v1
kind: ReplicationController
metadata:
  name: myapp-rc
  labels:
    app: myapp
    type: frontend
spec:
  template:
    metadata:
      name: nginx1
      labels:
        app: nginx
        tier: frontend
    spec:
      containers:
        - name: nginx
          image: nginx
  replicas: 3

-  Now run "kubectl apply -f rc-definition.yml"
----------------------------------------------------------------
Lets create a Yaml file to deploy replicaset with rs.definition.yml

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-rc
  labels:
    app: myapp
    type: frontend
spec:
  template:
    metadata:
      name: nginx1
      labels:
        app: nginx
        tier: frontend
    spec:
      containers:
        - name: nginx
          image: nginx
  replicas: 3
  selector:
    matchLabels:
      type: front-end

- Difference Between  ReplicationController and Replicaset is, in Replicaset yaml code, we will specifically mention Selector  column to match labels across all the targeted pods.

Ex: We have 10 Pods running, out of which we have 3 pods on which we would like to enable replicaset for HA. So in the code of Replicaset, we will specifically mention to pick the type mentioned in common from labels section to tie these 3 pods together. 

- Command to edit any yaml file without going into VIM editor is 
-> kubectl edit replicaset "replicaset yaml file name"
-> kubectl edit pod "pod yaml file name"

- Command to scale replicaset without editing configuration is
kubectl scale replicaset "name of the replicaset" --replicas="give the number"

Deployments
- Deployment is an object higher in Kubernates in the hierarchy
- Deployment provides the capability to upgrade the underlying instances seemeesly using rolling updates, undo changes, Pause and resume changes as required.

Definition file:

apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-dp
  labels:
    app: myapp
    type: frontend
spec:
  template:
    metadata:
      name: nginx1
      labels:
        app: nginx
        tier: frontend
    spec:
      containers:
        - name: nginx
          image: nginx
  replicas: 3
  selector:
    matchLabels:
      type: front-end

- Now run kubectl create -f deployment-definiation.yml to deploy the deployment.
- If you want to see the recent deployments then run 
->kubectl get deployments
- If you want see the replicaset created due to deployments then run -> kubectl get replicaset
- If you want to see the pods created due to deployments then run -> kubectl get pod
- if you want to see all the services deployed due to deployment file/code then run -> kubectl get all

Rollout and Versioning

- To know the recent rollout status
-> Kubectl rollout status deployment/myapp-deployment

- To know the complete history of the rollout
-> Kubectl rollout history deployment/myapp-deployment


Two types od deployment strateoges

1. Recreate strategy
- Lets say we have 4 apps running on 4 containers, incase we need to upgrade app from V1 to V2 then all the V1's will be brought down at a time and then upgraded and replaced by V2.
- In this strategy, there is application downtime.

2. Rolling update Strategy
- Lets say we have 4 apps running on the 4 containers, here the upgrades of the app happens one by one and there is very minimal downtime. 
- Incase no strategy is selected then Rolling update strategy will be the default deployment strategy selected.


How to update the app version upgrade:
Two ways to do it
1. Update the configuration file and run the below command
-> kubectl apply -f deployment-definition.yaml
- It means the deployment configuration file will be updated with latest app version and the deployment configuration will be updated.

2. Update the app version on the runtime.
-> kubectl set image deployment/"deployment name" \ nginx=nginx:V2.
= It means the deployment configuration is updated but not the deployment definition file. Incase you run the deployment definiation file then old version will be returned.

Different between Recreate and Rolling update


- While using Recreate upgrade strategy, the replica set will be scaled down to 0 from the number of replica's mentioned then it will bring back to the replica's. This way there is guaranteed downtime.

- While using Rolling update strategy, the replica set will be scaled down and up in parallel. There is no downtime expected in this strategy.

Upgrades:

- In Kubernetes Deployment when you are upgrading the application, the deployment will create 2 replica sets. 
- The second replicaset will be empty and when ever update is completed the updated container will be moved onto 2nd replicate to keep the app up and available for users.
- It can be seen thru -> kubectl get replicasets

Rollback:
- Incase the app dint worked post upgrade then we will need to roll back the changes.
- Using below command, the roll back will be smooth and without downtime one by one container will be rolled back.
-> kubectl rollout undo deployment/"deployment name"

Imperative & Declarative

Imperative def is to give step by steps instructions on what to do and how to do

Declarative def is to provide declaring the final outcome and system will define how to achieve.


Further more how infra as code is defined in both methods:

Imperative

Provision a vm by the name webserver
Installed NGINX software on it
Edit configuration file to use port 8080
Edit configuration file to web path
Load web pages to /nginx
start NGINX server

Declarative

VM Name: web-server
Package: nginx
Port: 8080
Path: /
Code: GIT Repo - X
Ex: Anible/Pupet/Chef/Terraform are Declarative examples


- What if a resource you are trying to deploy is already exist, then using declarative approach it can be differenciated like:

VM Name:  web-server
Package: nginx
----------------------------
VM Name: web-server
Package: nginx:1.18

- In Kubernates, Imperative way of commands are:

- To run an image
kubectl run --image=nginx nginx

- To create a deployment with image name nginx
-> kubectl create deployment --image=nginx nginx

- To create a service by exposing the deployment
-> kubectl expose deployment nginx --port 80

- To edit a deployment with the name nginx
-> kubectl edit deployment nginx

- To scale a replicas by 5 in nginx deployment
-> kubectl scale deployment nginx --replicas=5

- To set an image version from nginx to nginx:1.18
-> kubectl set image deployment nginx nginx=nginx:1.18

We can also use object configuration files using object such as 
- Creating an object using create command
-> kubectl create -f nginx.yaml

- Replcing an object using replace command
-> kubectl replace -f nginx.yaml

- Deleting an object using create command
-> kubectl delete -f nginx.yaml

- In Kubernates, Declarative way is to create a set of files
defines the expected state of the application and services on a Kubernetes cluster.

Commands

- The apply command will do creating, editing, deleting from the given inputs
-> kubectl apply -f nginx.yaml

**Imperative Object Config Files**

Create Objects:

kunectl create -f nginx.files
  -  To create the file


Update Objects:

kubectl edit -f nginx.yaml
  -  This command will open a editable yaml file from Kubernetes memory with some additional lines of code.

kubectl replace -f nginx.yaml
  -  Once edit command is ran to replace some portal of code then run replace command to replace the nginx.yaml file with new features.

Kubectl replace - force -f nginx.yaml

**Declatative Object config files**

kubectl apply -f nginx.yaml
  -  This command will simply run the nginx file incase there are any changes to it.

**Kubectl Apply Command**

Local file (Yml)
 - This is the actual configuration file user writes


Last applied Configuration (in Json format)
 - This the last saved configuration file incase we need to refer what was applied lastly

Kubernetes (Yml)
 - This is the configuration file stored in Kubernetes with some additiona fields

Annotations:
 - This is the location in Live object configuration file (Kubernetes file) where the last applied configuration is stored in Json format.

-  So when an apply command ran with configuration file updates then it will be compared with 
 1. config section in Live object configuration file in Kubernetes.
 2. Annotation section in Live object configuration file.


Kubernetes Namespaces

- So far we have created objects like Pods, services, deployments in cluster, what ever we are doing they are captured under a namespace called Default.
- Default namespace is created automatically when a cluster is created. 

- In order to have the DNS/Neworking resources are build to support the pods created will be by default created in kube-system namespace

- In order to have the resources accessed by team or other members, resources specially built in kube-public namespace.

- So by default, default namespace, kube-system namespace & kube-public namespace are built.


Namespace - Isolations

- We can create separate namespaces like resources groups in Azure environmental/app based and have different rules and restrictions to them for accessibility. Also a quota can be aligned to cap the number of resources to be built in a particular namespace.

DNS ( Default Namespace)

- to connect to a db service simply run -> mysql.connect("db-service")
- to connect to a db service from one namespace to another.
mysql.connect("db-service.dev.svc.cluster.local")


- If we see closely the above command
MySQL.connect("db-service.dev.svc.cluster.local")
                
1. db-service  is service name
2. dev is namespace
3. svc is service
4. cluster.local is domain

Kubectl commands for Namespace

- To list the pods for specific namespace, use below command, in below case we are fetching namespace 'kube-system' pod details
-> Kubectl get pods --namespace=kube-system

Ex:
- Lets say we have used below command to create pods using pod-definition file then by default it will be created in "default namespace."
-> kubectl create -f pod-definition.yml

- If you want to create pods in specific namespace then use below command. In the below command we are trying to create the pods in namespace "dev".
-> kubectl create -f pod.definition.yaml --namespace=dev


  - If you dint want to mention the namespace in the kubectl command line then define it in the yaml under metadata section.
Ex:
apiVersion: v1
kind: Pod
metadata: 
  name: myapp-pod
  namespace: dev
  labels:
    app: myapp
    type: front-end
spec:
  containers:
  - name: nginx
    image: nginx


- If you want to create a new namespace
Ex:
apiVersion: v1
kind: Namespace
metadata:
  name: dev
- Once above file is ready then simply run create command to create namespace

-  If you want to create a namespace thru the kubectl command line then use:
-> kubectl create namespace dev

- If you want to create the pods in only one namespace (assuming there are other namespaces), then use below command to set context
-> kubectl config set-context $(kubectl config current-context) --namespace=dev

  Resource Quota

- It is better to limit the quota per namespace to keep a cap on the deplyments happening.
- Example yaml file:

apiVersion: v1
kind: ResourceQuota
metadata:
  name: computer-quota
  namespace: dev
specs:
  hard:
    pods: "10"
    requests.cpu: "4"
    requests.memory: 5Gi

**Manual Scheduling**

How scheduling works:
- When deploying a pod via config file we don't specifically mention the nodeName on which the pod has to be deployed. Kubernetes will add it automatically.

- The Scheduler will run thru all the pods config files and identifies on which file the nodeName is added in the file and pick it up to add the scheduling property on the node with the name nodeName property under spec section in yaml and binds pod to the node.

If no scheduler:
- Incase scheduler is not set then the pods will not be assigned to any node and kept in pending status.

- To fix this, easy way is to input the nodeName details in the pod configuration file and bind the pod and node from the config file itself.

- Incase we want to bind a node to existing pod then we need to create a binding config file with the pod and targeted node details

apiVersion: v1
kind: Binding
metadata:
  name: nginx
target:
  apiVersion: v1
  kind: Node
  name: "add the name of the nodeName wasnted to bin


- Once above code is ready this needs to be converted into json format and post it to the Kubernetes to bind.

format: curl --header "Content-Type:application/json" --request POST --data {"apiVersion": "v1", "kind": "Binding" ...} http://$SERVER/api/v1/namespaces/default/pods/$PODNAME/binding/


Labels and Selectors:

- Are a standard method to group things together.

- In Pod definition file, under metadata labels are defined.

- To select the required a pod by filtering the selected labels, use:
kubectl et pods --selector app=App1

- Labels and Selectors use internally to connect with specific objects

Ex: To create a replicaset consisting  3 different pods, we define labels at 2 places
1. Under Metadata
2. Under Template

- The labels defined under metadata are of replicaset the labels defined under template are of pod.

- To match the labels in the config file, we use selector section. See example config file below:

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: simple-webapp
  labels:
    app: App1
    function: Front-end
spec:
  replicas: 3
  selector:
    matchLabels: 
      app: App1
   template:
     metadata:
       labels:
         app: App1
          function: Front-end
       spec:
         containers:
         - name: simple-webapp
           image: simple-webapp



Taints and Toleration:

⦁	Taints are set on nodes and tolerations are set on pods.
⦁	If there are 4 pods and needs to be accommodated onto 3 nodes, then if you put taint on a node then the pod which has toleration can only connect to the node  which has taint on it by scheduler.
Ex:
-> Kubectl taint nodes node-name key=value: taint-effect
⦁	The taint effect defines what would happen to the d if they donot tolerate the taints
⦁	there are 3 taints effect
1.NoSchedule  - Means pods will be not scheduled on the node
2.PreferNoSchedule - system will try to avoid placing a pod on the node which is not guaranteed.
3.NoExecute - Means new pods are not scheduled on the node and existing pods will be evicted if they are not tolerated.

-> kubectl taint nodes node1 app=blue:noschedule


pod-definition.yml

apiVersion: v1
kind:Pod
metadata:
  name: myapp
spec:
  containers:
  - name: nginx container
    image: nginx
  tolerations:
  - key: "app"
    operator: "Equal"
    value: "blue"
    effect: "NoSchedule"

 - Note: Taints and Tolerations are not added to Master node because by default they are applied. So it is why there will be no pod is added onto Master node by scheduler even though it has space.
⦁	To know the if taints and toleration is applied on the masternode run the below command:
 - > kubectl describe node kubemaster | grep taint

 - Note: Taints and Tolerations are not added to Master node because by default they are applied. So it is why there will be no pod is added onto Master node by scheduler even though it has space.
⦁	To know the if taints and toleration is applied on the masternode run the below command:
 - > kubectl describe node kubemaster | grep taint

Node Selectors:

⦁	Lets say we have 3 nodes with different resources configured in them from higher to lower.
⦁	So if we create a pod, it can go onto any node from higher to lower configuration node.
⦁	To specifically add pod which needs higher configuration node, we need to label the pod correctly. 
⦁	Before you run the pod config file, run below one
-> kubectl label nodes node-1 size=Large
⦁	Now lets deploy pod with node selector

apiVersion:v1
kind: Pod
metadata:
  name: myapp
spec:
  containers:
  - name: data-processor
    image: data-processor

   nodeSelector:  
     size: Large
⦁	now run kubectl create -f pod.yaml
⦁	The pod will now be created in the node where there is label size: Large.
⦁	Limitations for Node Selector
-- Large or Medium ?
-- Not small ?



Node Affinity:
⦁	This feature is used to place pod on specific node.
⦁	Advanced node selectors like "or" and "not" are achieved from Node Affinity:
Ex:
apiVersion:v1
kind: Pod
metadata:
  name: myapp
spec:
  containers:
  - name: data-processor
    image: data-processor

  affinity:
    nodeAffinity: 
      requiredDuringSchedulingIgnoredDuringExecution: 
        nodeSelectorTerms:
        - matchExpressions: 
          - key: size
            operator: NotIn
            values:
            - small


⦁	With above yaml, we can deploy a pod with affinity feature enabled to suffice the requirement, but what if there is no label with the name "size" added as part of key in the affinity section or what if the label size was modified by someone.

Node Affinity Types

Available:
requiredDuringSchedulingIgnoredDuringExecution
prefferedDuringSchedulingIgnoredDuringExecution

Planned:
requiredDuringSchedulingrequiredDuringExecution
prefferedDuringSchedulingrequiredDuringExecution


⦁	Lets break down "requiredDuringSchedulingIgnoredDuringExecution".
 1. Required During Scheduling means affinity section is looking for the label which is needed to bind the node and pod and if it is not present then the deployment will be failed. That means we need to use this unless you are binding a specific pod to a node.
2. Ignored during execution means pods will be running irrespective of the label being removed from pod section which is mandate for affinity.
⦁	Lets break down    "prefferedDuringSchedulingIgnoredDuringExecution".
1.	Preffered During Scheduling means, affinity section is looking for the label which is needed to bind the node and pod and if the label is missing then scheduler will place the pod into any other node which is available.
2.	Ignored during execution means pods will be running irrespective of the label being removed from pod section which is mandate for affinity.

⦁	For planned type, it is similar to available type but while execution, it is required to have labels in he pod to have the affinity impacted on that setting of the setup.


Resource Limits:

⦁	We can mention the amount of CPU and MEM needed for a container using Resource request.
⦁	Ex:
apiVersion:v1
kind: Pod
metadata:
  name: app1
  labels
    name: app1
spec:
  containers:
  - name: nginx
    image: nginx
    resources:
      requests:
        memory: "4Gi"
        cpu: 2
⦁	So when scheduler gets above request then it will search for 4 Gi mem and 2 cpu available in a node and accommodate this request.
⦁	1 cpu = 1AWS vcps, 1 GCP cores, 1 Azure core, 1 Hyperthread
⦁	 Note: we can alse et limit
Ex:
⦁	Ex:
apiVersion:v1
kind: Pod
metadata:
  name: app1
  labels
    name: app1
spec:
  containers:
  - name: nginx
    image: nginx
    resources:
      requests:
        memory: "4Gi"
        cpu: 2
      limits:
        memory: "2Gi"
        cpu 2

Exced Limits
⦁	A container cannot use more CPU when limit is set on the config file for the Pod. Throtled
⦁	However for Memory, it can use more memory than the limit, but if the usage is continuously trying to use more memory then it will get terminated and results in Out of Memory (OOM)


Default Behaviour
⦁	By default Kubernetes donot have any requests or limits set by default.
⦁	It can use resources as much as they can but finally it will suffocate.

Behaviour CPU
⦁	No Requests, No Limits
⦁	No Requests, Limits
⦁	Requests, Limits,
⦁	Requests, no Limits ( this is ideal setup)


Behaviour Memory
⦁	No Requests, No Limits
⦁	No Requests, Limits
⦁	Requests, Limits,
⦁	Requests, no Limits -  In this scenario, we cannot throtle it so it will kill the pod with OOM

Limit Range

⦁	Yaml for CPU
apiVersion: v1
kind: LimitRange
metadata:
  name: CPU-resource-contraint
spec
  limits:
  - default:
      cpu: 500m
    defaultRequests:
      cpu: 500m
    max:
      cpu: "1"
    min:
      cpu: 100m
    type: container 


⦁	Yaml for Mem
Limit Range
apiVersion: v1
kind: LimitRange
metadata:
  name: Memory-resource-contraint
spec
  limits:
  - defult:
      memory: 1Gi
    defaultRequests:
      memory: 1Gi
    max:
      memory: 1Gi
    min:
      memory: 500Mi
    type: container

⦁	Note: these are enforces when the pod is created, if you create or change the limit range it does not effect  existing pod, but it will effect the new pods.

Resource Quotas
⦁	We can set hard limitson  requests  and limits at namespace level.

apiVersion:1
kind: ResourceQuota
metadata:  
  name: my-resource
spec:
  hard:
    requests.cpu:4
    request.memory: 4Gi
    limits.cpu:10
    limits.memory:10Gi


Daemonsets

⦁	It ensures a copy of your pod added to the Daemonset node automatically.
⦁	When the actual pod is deleted, then the saved pod will also gets deleted.
⦁	Kube-proxy can be deployed as Daemonset.

Ex:

apiVersion:1
kind: DaemonSet
metadata:
  name: monitoring-daemon
spec:
  selector:
    matchLabels:
      app: monitoring-agent
  template:
    metadata:
      labels:
        app: monitoring-agent
    spec:
      containers:
      - name: monitoring-agent
        image: monitoring-agent

To see daemonset
⦁	kubectl get daemonsets

How does daemonset works


Static PODs

⦁	Static pods are deployed by Kubelet itself independent to the Kubernetes architecture (ApiServer)
⦁	Kubelet only understand pods, so it can only create pods and it don't create replicaset/deployment etc.,
⦁	So without pod definition file, kubelet cannot create any pod. So there is a directory /etc/Kubernetes/manifest where we can store definition files to use.
⦁	Kubelet periodically checks this location and use the files to create the pod.
⦁	Incase a pod corrupts, kubelet will start the pod and keep it live.
How to configure the directory on kubelet  store file.
1.	at --pod-manifest-path=/etc/Kubernetes/manifest in kubelet.service.
2.	at --config=kubeconfig.yaml. And in config kubeconfig.yaml file add the path in below way
staticPodPath: /etc/Kubernetes/manifest


⦁	To view the static pod run below command
-> docker ps

⦁	kubelet will create pods in two ways
1.	Thru static pod way described above
2.	Thru API Server
⦁	Well when a static pods are created by kubelet, then API server also know about this information so when you run kubectl get pods, the static pods details are derived.

Use Case:
⦁	On the master node, create the control planes components manifest files like controller manager.yaml,apiserver.yaml, etcd.yaml in the /api/Kubernetes/manifest location and rest is taken care by kubelet as pods on the cluster.
⦁	Since it is a static pod, incase they are down, kubelet will automatically bring them up.

Multiple Schedulers

⦁	 need to understand from Shareef how it is achieved.

Configuring Kubernetes Scheuler profiles

⦁	Lets say we have a pod with cpu needing 10 vcores.
⦁	Scheduler will check all the nodes where there is capacity to allocate this pod with 10 Vcores CPU.
⦁	There is a flow to follow
1.	Schedulling Queue
2.	Filtering
3.	Scoring
4.	Binding


⦁	These are called scheduling plugins
1.	Scheduling Queue
⦁	At this stage the pods will be waiting in queue to algin to a node based on the priority set.
⦁	To set priority you need to create a priority class as shown below:
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: high-priority
value: 1000000
globalDefault: false
description: "this priority class should be used for XYZ pods only."
⦁	So the above priority class should be added in the spec of the pod to give priority to the pod deployment which is in the queue.

apiVersion:v1
kind: Pod
metadata:
  name: simpleapp
spec:
  priorityClassName: high-priority
  containers:
  - name: simpleapp
    image:simpleapp
    resources:  
      requests:
        memory: "1Gi"
        cpu: 10

⦁	So in the above example the priority class name is defined so based on the priority the scheduler will put this pod deployment to queue.

2. Filtering
⦁	The phase where nodes that cannot run the with the resources will be filererd out.So it means, we need 10 CPU's and scheduler will check for the nodes where there is more than or equal to 10 CPU.

3. Scoring
⦁	This phase will check after consuming the 10 CPU's needed for the new node deployment how many will be left.
⦁	Based on the available cpu's count the highest one will be picked up under Scoring phase.

4. Binding
⦁	This phase will bind the pod and node by executing the config yaml file.




Scheduling Plugins

Scheduling Queue  -  PrioritySort plugin
Filtering - NodeResourceFit,NodeName,NodeUnschedulable plugin
Scoring -  NodeResourceFit,ImageLocality plugin
Binding - Defaultbinder plugin


Extension Points

⦁	Thru which the plugins are added to the pod deployment on the node

1.	Schedulling Queue - queueSort
2.	Filtering - prefilter, filter, postFilter
3.	Scoring - preScore, score, reserve, permit
4. Binding - prebind, bind, postBind

Multi-scheduling files - Learn deeply




Security Kubernetes Security Primitives

1.	Authentication in Kubernetes cluster

⦁	We have Admins to administer Cluster, we have developer to work on nodes thru cluster, we have endusers to access the application and we have other apps like Bots to integrate with apps on the nodes.
⦁	Now lets see how the communication from all these sources will be securely done with Authentication.
⦁	Lets consider Admins, developers and Bots for now as endusers authentication will not fall under K8s authentication.
⦁	Basically there are two types of accounts - User accounts(Admins, developers) and Service Accounts (Bots)
⦁	K8s cannot create user account as it relies on the input file
Ex: Kubectl create user user1 -- X
⦁	K8s can create service account 
Ex: kubectl create serviceaccount SA1 

User Accounts

⦁	All user accounts are managed by Kube-apiserver
⦁	There few auth mechanism to pass to Kube-apiserver:
1.	Static Password File
2. Static Token files
3. Certificates
Static Password File
⦁	If we considered static password file mechanism, we need to create .csv file with username and password details and pass it to kube-apiserver.service file in below format and then restart kube-apiserver
--basic-auth-file=user-details.csv
⦁	As an alternative, you can specify the above command line in the pod definition file under spec of the containers to execute.

Static Token files
⦁	Similar to static password file mechanism, in token based auth, just replace the password with the token and pass it to kube-apiserver.service  file or add it in the pod manifest file as shown below
--token-auth-file=user.detail.csv


KubeConfig

By default kubeconfig file will be kep in $HOME/.kube/config.

The config file has 3 parts
CLusters
COntexts
Users

⦁	In Clusters arevarious kubernetes cluster where we will have access to. Ex: Develpment, Production, Google, AWS, Azure etc.,
⦁	In Users, there are various account to access the clusers. Ex: Admin, Dev User, Prod User.
⦁	In Contexts, Clusters and contexts are binded. Ex: Admin@production, Dev@Google. It means Admin account is being used to access production environment. This way you don't need to specify user certificates, server address in each and every kube control command.
⦁	Kube config file:

apiVersion: v1
kind: Config
current-context: my-kube-admin@my-kube-playground
Clusters
  - name: my-kube-playground
    cluster:
      certificate-authority: ca.crt
      server: https://my-kube-playground:6443
Contexts:
  - name: my-kube-admin@my-kube-playground
    context:
      cluster:my-kube-playground
      user: my-kube-admin
users:
  - name: my-kube-admin
    user:
      client-certificate: admin.crt
      client-key: admin.key

⦁	To view the current config file details run
-> kubectl config view
⦁	Incase you dint mention any current config to use then by default it will pick the config mentioned in $HOME/.kube/config location. 

⦁	To change the current context incase you want to use prod-user@production config then simply run
-> kubectl config user-context prod-user@production

⦁	The above change will reflect under current-context location in the config file

apiVersion: v1
kind: Config
current-context: prod-user@production
Clusters
  - name: production
    cluster:
      certificate-authority: ca.crt
      server: https://my-kube-playground:6443
Contexts:
  - name: prod-user@production
    context:
      cluster:production
      user: mprod-user
users:
  - name: prod-user
    user:
      client-certificate: admin.crt
      client-key: admin.key


API GROUPS
⦁	There are 2 types of API's
1.	Core group (/v1)
2.	Name group (/apis)

⦁	The core groups is where all functionality exisits like namespaces, config maps etc.,
⦁	The Name groups are more organized and going forward name groups will be used.

Named (apis)
|
|
\/
API Groups
 - /apps
 - /extensions
 - /networking.k8s.io
 - /storage.k8s.io
 - /authentication.k8s.io
 - /cerificates.k8s.io
|
|
\/
/apps
|
|
\/
/v1
|
|
\/
Resources
 - /deployments
 - /replicasets
 - /statefulsets
|
|
\/
Verbs
 - list
 - get
 - create
 - delete
 - update
 - watch

⦁	So finally, all resources in Kubernetes are categorized into API groups at the top level we have core API group and named API group. Under the named API group we have one for each section and under the each section we have different resources has a set of associated options known as verbs

Authorization
⦁	In general authorization is used to allow a user/ service accounts to administrate.
⦁	There are 4 types of mehanisms
1.	Node
2.	ABAC
3.	RBAC
4.	Webhook
⦁	Let take a look at Node

⦁	As we know kube API server is accessed by users for management purpose. Any opertional activity done by Kubelet like Read or write on  serices, endpoint, Nodes, Pods, Node status, Pod status etc., the information is passed to kube API server, These requests are organised by Node Authorizer.
⦁	Any request comes with Node Authorizer which are under System Nodes groups are granted the previlages.

ABAC(Atribute Base access control)  -  Policy based 
RBAC(Role Base access control)  -  Role based (Secure)


RBAC

⦁	Config file
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
rules:
  - apiGroup:
⦁	User need to be binded with the roles created, to create that use:
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
subjects:
 -  kind: user
    name: -  dev-user
    apiGroup: rbac.authorization.k8s.io

 roleRef:
  -  kind: Role
     name: developer
     apiGroup: rbac.authorization.K8s.io    

⦁	To view the create roles
-> kubectl get roles
⦁	To view the role bindings
-> kubectl get rolebindings
⦁	To understand the access of a user
-> kubectl describe role developer

⦁	How to check access to admin a namespace/pod/node
-> kubectl auth can-i create deployments/ delete nodes etc.,

Cluster Roles:

⦁	In Namespace we can only create pod, replicasets, jobs, deployments, services, secrets, roles, rolebinding, configmas, PVC.
⦁	In Cluster Scoped, we can create only nodes, PV, clusterroles, clusterolebings, certificatessigningrequests, namespaces.

⦁	To view
-> kubectl api-resources --namespaced=true

⦁	CLuster roles ae norman roles created on cluster scoped resources.
⦁	cluster role def file:
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
rules:
 - apiGroups: [""]
   resources: ["nodes"]
   verbs: ["list", "get", "create", "delete"]
subjects:
 - kind: user
   name: cluster-admin
   apiGroup: rbac.authorization.k8s.io
roleRef:
   kind: ClusterRole
   name: cluster-adminstrator
   apiGroup: rbac.authorization.k8s.io

⦁	There is no hard rule that resources arelimited to namespace roles. If we give a user clusterscoped role on a pod then he can access all the pods under all namespaces.

ServiceAccounts:
⦁	There are 2 types are accounts in k8s
1.	User accounts (used by humans)
2.	Service accounts (used by apps)

⦁	To create a servce account, run
-> kubectl create serviceaccount dashboard-sa
In the above case the service account name is dashboard-sa

⦁	To list the service account details, run
-> kubectl get serviceaccount 

⦁	To get more details about the service account, run
-> kubectl describe serviceaccount dashboard-sa

By default a token is generated for a service account which acts as a security feature.

⦁	When a service account is created first it creates an account with the provided name and then it creates a token and then stores in Secret object.
⦁	Secret object is then linked to service account.
-> kubectl describe secret "token name"

⦁	In simple words, create a service account, assign RBAC  and export the service account token o configure 3rd party application to authenticate to k8s api.
⦁	But what if the 3rd party application is installed in K8s itself. The token itself will be mounted onto a volume on pod to host the application.

⦁	By default a default service account will be created, also per namespace a service account will be created.
⦁	Note: You cannot assign a new service account on a pod, you must delete and recreate the pod with new service account.
⦁	Incase you want to delete the existing service account and create a new one, then you must specify it in the deployment and it will perform the rollout update to update the new service account.
⦁	Kubernetes will automatically mounts the default service account on a pod. Incase you dont want to have the default service account, you need to specifically mention in config file of the pod.

Image Security:

⦁	image: nginx  - here nginx is the image name take from a repository from Docker.
Total path will be: docker.io/library/nginx
                    (Registry) (User) (Image/reporsitory)

⦁	These are all publically available to access.
Private Repository:
⦁	We can also create our own/private repository to run applications.
⦁	First login to private registry
-> docker login private-registry.io

⦁	Once login run the application in docker
-> docker run private-registry.io/apps/internal-app

⦁	Now replace the image name in the pod yaml file

apiVersion: v1
kind: Pod
Metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx
    image: private-registry.io/apps/internal-app

⦁	Now what about the creds to login to private registry to retrive the image on the docker runtime to the worker nodes.
-> kubectl create secret docker-registry regcred -- docker-server=private-registry.io  --docker-username= registry-user --docker-password=registry-password --docker-email=registry-username@org.com.

then pass the secret name regcred to the above pod yaml file

apiVersion: v1
kind: Pod
Metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx
    image: private-registry.io/apps/internal-app
  imagePullSecrets:
   - name: regcred

Network Policies
⦁	Lets say we have a user trying to connect with a database. We have a web server serving the frontend (80)and an API server(Port 5000) linked to it to pass traffic onto backend Database severs (3600)
⦁	Here the traffic from user to web interface is on port 80 is Ingress traffic.
⦁	Traffic from wed interface to API server is Egress.
⦁	Traffic to API server from web interface is ingress.
⦁	Traffic from API server to DB is egress. 

    -> Ingress        -> Egress, Ingress        -> Ingress
User ----    80     -----     5000     -----     3306
                                             <- Egress       


Cluster Networking:

Ports to be open on Master Node:
⦁	Port 6443 for Kube API server
⦁	Port 2379 for etcd
⦁	Port 2380 for etcd client
⦁	Port 10250 for Kubelet API
⦁	Port 10251 for Kubescheduler
⦁	Port 10252 for Kube controller manager

Ports to be open on Worker Node:
⦁	Port 10250 for Kubelet API
⦁	30000-32767 for NodePort Services



Pod Networking:
⦁	Lets say we have 3 nodes connected thru a LAN and there 5 pods per node and we know 3 nodes are in contact thru LAN but how the pods will be communicating with each other.
⦁	As of today there is no build in sollution for it, we need to implement networking sollution.
⦁	K8s expects every POD should have an IP address
⦁	Every pod should be able to communication with every other POD in the same node
⦁	Every pod should be able to communicate with every other POD on other nodes without NAT.
⦁	There many 3rd party tools whch will help with such requirement like weaveworks, flannel, cilium, vmware NSX etc.,

⦁	But lets try to build this internally
 Lets say we have 3 node clusters and give the Ip address as 
node1 192.168.1.11
node2 192.168.1.12
node3 192.168.1.13

When containers are created, K8s enables network namespaces for them to attach these namespaces to a network.

Bridge networks will help to create the network on each node  with following commands

-> ip link add v-net-0 type bridge

And bring the network up

-> ip link set dev v-net-0 up

Now add the ip to the nodes 

-> ip addr add 10.244.1.1/24 dev v-net-0
-> ip addr add 10.244.2.1/24 dev v-net-0
-> ip addr add 10.244.3.1/24 dev v-net-0


Now lets write a script to assign the IP;s to the individual pod. Note: we need to specify the pod everytime and run the script to get the IP added.

net-script.sh

# Create Veth pair
ip link add 10.244.1.2

# Attach veth pair
ip link set
ip link set

# assign IP Address
ip -n <namespace> addr add
ip -n <namespace> route add

# Bring up interface
ip -n <namespace> link set


After running above scripts, we will assign the IP's individually to the PODs. Now lets try to communicate from one pod of the Node to another pod of another node.

Obviously it will fail, because the communicate was inline between the nodes only but we need to enable the comms between the bridgenetwork and Node then only the comms will be enabled.

ip route add <pod ip> via <node ip or gateway ip>


Container Network Interface (CNI)
As per CNI the scrip should have a ADD section and a DEL section.


CNI in Kubernetes

Pre-reqs:
⦁	Network Namespaces in Linux
⦁	Networking in Docker
⦁	Why and what is container network interface (CNI)
⦁	CNI plugins

Defination:
⦁	Containers Runtime must create network namespace
⦁	Identify network the container must attach to
⦁	Container Runtime to invoke Network Plugin (bridge) when container is ADDed
⦁	Container Runtime to invoke Network Plugin (bridge) when container is DELeted
⦁	JSON format of the Network Confirguration


Configuring CNI
⦁	CNI plugin is configured in kubelet service.


DNS n Kubernetes

What names are assigned to what objects
Service DNS records
POD DNS records


⦁	By default the DNS is setup within Kubernetes called KubeDNS.
⦁	Lets assume we have 2 nodes, on first node we have one pod and in another node we have a service and a pod.
⦁	Consider 1st pod name is dev and 2nd pod have is web and service name is web-service.
⦁	Incase from dev pod, if web-service has to be accessed them in DNS a record will be created with name web-server, under namespace apps(assuming the service is in this namespace), type as svc, root as cluster.local.
⦁	So the URL is https://www.web-service.apps.svc.cluster.local.

⦁	similarly for the pods the url would be https://www.<ip address>.namespace.svc.cluser.local.


Ingress

⦁	I have a URL built to be access for the online store gudies and the url is http://myonline.co on port 32000
The tradditional method for internal traffic is to put a proxy between the pod and the online URL to make sure the URL is being accessed with out IP in the URL as the mapping of the IP happens in the proxy itself.

⦁	If the same url has a request to be accessed online them we will be putting a loadbalancer with a public IP on it.


Ingress Controller and Ingress Resource

⦁	Ingress controller is not a defaultly installed on k8s, it needs to be configured. 
⦁	Ingress controller is a loadbalancer supported by K8s, it can be Google Cloud Engine, Nginx, Contour, HA Proxy etc are few examples.
⦁	To configure INgress controller, it has set of config files to be created:


1.	deployment.yaml
apiVersion: extensions/v1betal
kind: Deployment
metadata:
  name: nginx-ingress-controller
spec:
  replicas: 1
  selector:
    matchLabels:
      name: nginx-ingress
   template:
     metadata:
       labels:
         name: nginx-ingress
     spec:
       containers:
         - name: nginx-ingress-controller
           image: quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.21.0

        args:
          - /nginx-ingress-controller
          - --configmap=$(POD_NAMESPACE)/nginx-configuration
        env:
          - name: POD-NAME
            valueFrom:
              fieldRef:
                fieldPath: metadata.name
           - name: POD_NAMESPACE
             valueFrom:
               fieldRef:
                 fieldPath: metadata.namespace
         ports:
           - name: http
             containerPort: 80
           - name: https
             containerPort: 443   


 2. service.yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-ingress
spec:
  type: NodePort
  ports:
  - port: 80
    targetPort: 80
    protocol: TCP
    name: http
  - port: 443
    targetPort: 443
    protocol: TCP
    name: https
  selector:
    name: nginx-ingress

3. Service Account

apiVersion: V1
kind: ServiceAccount
metadata:
  name: nginx-ingress-serviceaccount


The bottom line is we need a deployment config to deploy the inggress controller, a service to expose it on http and https, a config map to feed configuration data and right authentication to access the application.


Ingress Resource

⦁	Ingress Resource is nothing but configuring backend servers with the port and the traffics on which it listens.

config:
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: ingress-wear
spec:
  backend:
    serviceName: wear-service
    servicePort: 80


⦁	Here the config file can be written in two types:

With the different paths

apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: ingress-wear-watch
spec:
 rules:
 - https:
     paths:
     - path: /wear
       backend:
         serviceName: wear-service
         servicePort: 80

     - path: /watch
       backend:
         serviceName: watch-service
         servicePort: 80


With the different rules

apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: ingress-wear-watch
spec:
 rules:
 - host: wear.my-online-store.com
   http:
     paths:
      backend:
         serviceName: wear-service
         servicePort: 80
 - host: watch.my-online-store.com
   http:
     paths:
      backend:
         serviceName: watch-service
         servicePort: 80

