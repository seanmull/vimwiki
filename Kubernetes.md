## Containers

Application depend on an underlaying infrastructer.  Example applications could
be node server, mongoDB database, messaging service such as redis.  These are what
make up the application.  However to make the application run in predicable manner
they need an underlaying infresture that support it such as libraries, OS software,
hardware drivers.  The problem with this set up is that it is fragile.  If you make
one change to the application in one service it can cause problems for other services.
This forms a complex matrix between all the application an infreatrues.  Its complex
since every connection has to be maintained to allow this predicable behavoir.  Managing
this used to be called the "mangaging the matrix from hell".  Training was difficult
since it was fragile.  Any mistake caused deployment to fail.

Docker is a containerization technology that allows a serperation between OS and 
all the software that sits on top of them.  

Containers are seperation enviorments for the application to run.  The software
kernal is what is needed outside the containers.  Docker can have containers with 
different flavors of linux since it "shares the kernel"

Containers => OS > Docker > Containers (smaller size, and less resourced used)
VM => OS > Hyperviser > VM (full isolated)

Containers are running instances of an image

Dev => Give instuctions and software packages => Ops
Dev => An images works the same way on each production env => Ops

## Orchestration

Orhestration is a process that allows for overseeing of docker hosts.  Part
of overseeing the hosts is to monitor health (if it crashes), provide load balencing
when the load gets too high.   Kubernetes is one of these ochestration technolgies.

Advantages
Its highly available (because of load balencing) by scaling up and down

## K8 architecture

Node - a worker machine in which kubernetes is installed
Cluster - a set of nodes, allows you to share the load over similar node
Master - a node configured a master
Components
1. API server - front end of kubernetes cluster
2. ETCD - key-value store used to manage the cluster
3. Shecdule - distributeing work accoss the node
4. Controller - make the decisions about nodes failing
5. Container runtime - software used to run the containers
6. Kubelet - the agent seeing if the containers run as they should

Master
1. Api server
2. etcd
3. controller
4. scheduler


Worker
1. Kubelet

kubectl - k8 command line tools

## Setting up minikube

Minikube - sets up a single node kube cluster that is available on the cloud
in an iso image

Minikube has a command that will take the iso and deploy it on a VM.
Kubectl is the command line tool needed to interact with K8

May need to clear the config files if you have problems with docker socket

## Pods

Containers are contained in a pod.  
You can have two different pods on a node.
One container per container
You can have more then one container per pod
You can have helper containers and they need to be along
the application
They can share the same network space
The can share volumes


image downloaded from the docker hub
```
kubectl run nginx --image nginx
```

gives us the state of the pods
```
kubectl get pods
```

give us the status of a pod such as IP, status
```
kubectl describe pod nginx
```

## YAML

Format

Key-Value pair
Fruit : Apple

Array
Fruits:
  - Orange
  - Apple
  - Banana

Dictionary/Map
Banana:
 Calories: 105
 Fat: 0.4 g
 
Note: spaces have to be the same
Any missmatches will indicate nested propeties

Lists/ Key-values/ Dictionary/map can all be nested

Dictionary is unordered
List is ordered

## Pods with YAML
pod definition files includes

apiVersion: 
kind: POD
// this needs to be unchanged but you can add
// to labels
metadata: //dictionary
  name: myapp-pod 
  labels:
    app: myapp


spec:  //format verys
  containers:
    - names: nginx-container
    - image: nginx


Kind          Version
POD           v1
Service       v1
ReplicaSet    apps/v1
Deployment    apps/v1

```
kubectl create -f <name of pod file>
```

Basic workflow with pods
```
kubectl get pods
```
Getting more discription about the pod
```
kubectl describe pod <name of pod>
```

## ReplicationController and Definition Set

If one application fails we can have a failsafe

The replication controller will allow us
to manage multiple instances of an application
this will allow us to higher availablility

Even if we have one pod and that fails the controller
can recover that one

Along with fail safety the controller will provide load balencing
These controllers can span across multiple nodes as well as pods

Controller is the older technology that is replaced with replica set

// replica controllers
apiversion: v1
kind: ReplicationController
metadata:
  name: myapp-rcc
  labels: 
    app: myapp
    type: frontend
spec:
  template:
     <everything from the pod excluding apiversion and kind>
  replicas: 3
  
// replica sets everything that is different
apiversion: apps/v1
kind: ReplicaSet
..
..
selector: // this includes pods that were not linked initially in the creation
  matchlabels:
    type: frondend
  
```
kubectl create -f rc-definition.yml
kubectl get ReplicaSet
kubectl get pods
```

replica set is a process that monitors the pods in case any of them go down
labels help replica set to help find which pods need to be monitors

if you delete a pod in a replicaset it will create a new one
if you add a pod with the same label as the replica set it will terminate it

to scale replicas
```
kubectl replace -f replicaset_definition.yaml
kubectl scale --replicas=6 -f replicaset_definition
kubectl delete replicaset myappreplicaset  // also deletes pods
kubectl edit replicaset myappreplicaset // edit the as running config of the replica set
```
Note: this doesn't actually scale but changes the file
     
Nodeport  .....  port 80:30004/TCP

To get access to the application
```
minikube service <name of service> --url // this will print us the url of the service
```

lets say we have layers of applications

front end

backend

redis

mysql

Connecting with the ip of each pod is problematic since they are not static
When they die they get replaced.
Services can provide a single interfaces.  It will group different instances of the same
service

## Deployments

Cloud services starting up multiple instances of app
Upgrade functionality should be done seemless (rolling updates)
Say you have an issue with one of the updates you would want to rollback the update
Modifying environemental variables
Ability to pause and restart containers when you make changes

Pod | Pod | Pod
  ReplicaSet
  Deployment
  
Deployments incapolate everything

Definition file is similar to replicaSet except the kind is deployment

```
kubectl create -f <name of yaml defintion file>
kubectl get deployments
kubectl get replicaset
kubectl get pods
kubectl get all // this will give us all deployments/replicasets/pods
```

```
kubectl rollout status <deployment name>
kubectl rollout history <deployment name>
```

Deployment stategies
Recrate: Distroy and deploy -> application is down
Rolling: Replace one instance at time
  Creates a replicaSet and launches image one at a time

To update change the image name and run
```
kubectl apply -f <deployment name>
kubectl set image <deployment name>
```

To rollback
```
kubectl rollout undo <deployment name>
```

// deprecated
```
kubectl create -f <deployment name> --record // to get logs of how things are running
```

## Networking

example
1 pod on 1 node
the node is hosting on 192.168.1.2
internal ip 10.244.0.0 //this network assigns ip to the pods
Note: Nodes can have the same internal ip as one another
the pod is hosting on 10.244.0.2
this is not the ip on the system

Rules
All containers/pods need to communicate to each other without NAT
All nodes ....

Creating a cluster
Seperate services handle the routing of all the different nodes
This creates different ip address so there is no conflicts

## Services

Services are what allow interactivity between the pods
They allow loose coupling between the services

You can ssh into the internal network of the node but this is not what we want

Services provide us the abstraction layer to interact with nodes networking ip
It allows you to listen to exposed port

Service types
1. Node port // where a port is exposed on the node allowing access to internal network
2. Cluster IP // creates a vertual ip inside of the cluster
3. Load balencer //provisions a load balencer for the applicaiton

For node ports it has 3 ports
Pod port // otherwise known as the target port
Service port // otherwise as the port
Node port // otherwise known as nodePort 30000-32767

service definition for NodePort
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: NodePort 
  ports:
    - targetPort: 80
      port: 80
      nodePort: 30008
  selector: 
    app: myapp
    type: front-end
    
Steps to set up networking for the cluster
```
kubectl create -f <yaml file>
kubectl get services
curl http ...
```

The selector for the services will be the same as the pod labels

If we have a replicaset it will allow access in a random way

service definition for ClusterIP
apiVersion: v1
kind: Service
metadata:
  name: backend
spec:
  type: ClusterIP // default  
  ports:
    - targetPort: 80
      port: 80
  selector: 
    app: myapp
    type: backend  
 
 
Load balencing can be achived through the cloud platforms such as AWS

service definition for Load balencer
apiVersion: v1
kind: Service
metadata:
  name: backend
spec:
  type: LoadBalencer // default  
  ports:
    - targetPort: 80
      port: 80
  selector: 
    app: myapp
    type: backend  

## Mircroservices

Sample microservice
Docker
1. Deploy containers
2. Enable connectivitiy
3. External access

K8
1. Deploy these as pods
2. Expose services

## K8 on the cloud

There are two types of cloud services

Self-hosted/ Turnkey solutions
You provision the VMs
You configure the VMs
You uses scripts to deploy the cluster
You maintain the VMs yourself

Hosted solutions
Kubenetes as a service
Provider provisions VM
Provider installs K8
Provider maintains VM

