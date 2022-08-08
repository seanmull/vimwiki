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

## Microservice arch
1. Many applications together the provide all the functionality that the buisness need
2. Multiple VM are run that collectivly form nightlife cloud
3. It was usually the reponsibly of IT to manage servers

## AWS
1. Didn't want to manage the hardware
2. Cloud service - where we get virtual machine
3. Config all the software
4. EC2 allows us to get VM
5. FBS network attached storage
6. S3 Object storage
7. ECR Private Docker Registry
8. EKS Mangaged Kubenetes Engine

Time consuming to manage the machines
We needed a simple configuration and deploy it to another machine

## Docker
1. Isolate dependancies to reduce conflicts
2. Automates the process of building
3. It makes into one object
4. Its like a windows exe with all the libraries
5. Tell it how much resourses it will use

Docker desktop that runs an linux VM

We are decoupling software from hardware

## Kubenetes
1. Provides a fail safe if service fail
2. Regesters applications and containers
3. Controller will provide this fail safe functionality 
4. Google built an orchistration layer


Demo
Pods are a running instance of an application

deployment
  services.yaml
    allows you to access the service from your local machine
  deployment.yaml
    creates pods on the cluster
    
they use label to connect things together
matchlabels -> label on the container
