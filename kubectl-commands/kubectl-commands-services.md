kubectl create -f nodePort-Pod.yml

kubectl get deployments 

kubectl get pods

kubectl logs nodeport-pod node-port-container1
kubectl logs nodeport-pod node-port-container2

Two containers within the same POD cannot use the same poirt!

//////////////////////////***********************///////

Create Deployment with multiple POD replicas of containers

kubectl create -f nodePort-Deployment.yml

kubectl get deployments

kubectl describe deployment deployment-app


kubectl get replicasets

kubectl describe replicasets


kubectl describe replicaset deployment-app-6fc9b7c7b9

Now deploy the nodePort-service

kubectl create -f nodePort-service.yml
it is already allocated

kubectl delete service nodeport-service 

kubectl get services

NAME              TYPE       CLUSTER-IP     EXTERNAL-IP  PORT(S)

nodeport-service   NodePort    10.109.150.96   <none>        8090:31000/TCP   36s



 10.108.190.196

kubectl describe service  nodeport-service 

See the endPoint ip for the containers

List the pods that are running the application:

kubectl get pods --selector="user-app=py-app" --output=wide

Describe or log pod

kubectl describe  pod deployment-app-6fc9b7c7b9-h2s7k
kubectl describe  pod deployment-app-6fc9b7c7b9-r9zvv

kubectl logs deployment-app-6fc9b7c7b9-h2s7k
kubectl logs deployment-app-6fc9b7c7b9-r9zvv

Get the public IP address of one of the nodes that is running a anode port pod from kubectl cluster-info

minikube ip
192.168.99.100

Access the app through node-port services

192.168.99.100:3100

10.192.0.3

//////
kubectl cluster-info  
Kubernetes master url : https://192.168.99.100:8443/

KubeDNS is running at https://192.168.99.100:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

////////
Now delete one of the pods  

kubectl delete pod deployment-app-6fc9b7c7b9-r9zvv

And get the list of pods immediately
sudo kubectl get pods

The Replication Controller creates another POD to serve the application and it contniues in the cluster!

To get the deployment
kubectl get deployments
kubectl get deployment deployment-app

kubectl describe deployment deployment-app

To scale the deployments
kubectl scale deployment deployment-app --replicas=5 

kubectl get deployment deployment-app

NAME             DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment-app   5         5         5            5           38m

 Check the response in the browser

///////*******//
Deploy The load balancer service

kubectl create -f Node-LoadBalancer-Service.yml

kubectl  get svc  OR kubectl  get services
kubectl  describe  svc load-balancer-service

kubectl  get  svc load-balancer-service

NAME                    TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)
load-balancer-service   LoadBalancer   10.107.90.58   <pending>     8090:31840/TCP

To access this service from nodes in the cluster

Send curl the load-balancer-service on <CLUSTER-IP>:<PORT> from any node in your cluster. The Service IP is completely virtual.


This service is accessed over network by
http://EXTERNAL-IP: 31840

Wait till the EXTERNAL-IP is gewtting assigned

kubectl  get  svc load-balancer-service --watch=true

To get the endponts connected with service

kubectl get ep load-balancer-service 

kubectl delete service   load-balancer-service 


kubectl delete deployment deployment-app

kubectl delete pods --all
////******************
Install apps/utilies in the containers 

kubectl exec -it deployment-app-6fc9b7c7b9-2dx5z -- /bin/bash

To install ping in the container
apt-get update
apt-get install iputils-ping
apt-get install curl

ping to the node-port service
 or
ping 10.109.150.96

ping to other containers
ping 

////********************//

////Create multiple deployments and connect togethyer///****

Deploy py-app application

kubectl create -f py-app-deployment-hostPort.yml

kubectl get deployments
kubectl get deployment py-app-deployment
kubectl describe deployment py-app-deployment

Access the app in browser
http://192.168.99.100:7070/

Check the status of other pods created
kubectl describe deployment py-app-deployment

kubectl describe pod py-app-deployment-78bb55cc88-b7n9r   
 
 Now increase the replica value to 3 in py-app-deployment-hostPort.yml and re-deploy

kubectl create -f py-app-deployment-hostPort.yml

Check the other pods status
 
We cannot have mutiple containesr with same Host port mapping.

Delete the deployment
kubectl delete deployment py-app-deployment

kubectl delete deployments --all

///////////////******

Define deployment for Redis app

kubectl create -f redis-app-deployment.yml


Create service for redis-app

kubectl create -f redis-app-service.yml


The deployment is exposed through services

kubectl create -f py-app-deployment.yml

kubectl get deployments


Create py-app service to work over py-app deploymnents

To connect throgh service to the py-app

kubectl create -f  py-app-service.yml

kubectl get svc py-app-service

NAME             TYPE       CLUSTER-IP      EXTERNAL-IP  PORT(S)
py-app-service   NodePort   10.106.39.118   <none> 8090:32662/TCP

It is mapped to deployent throgh port 32662

Access it through 
http://192.168.99.100:32662/


////////////////////****////

///*(***8/////
Now deploy redis deplyment app
kubectl create -f redis-app-deployment-hostPort.yml

kubectl get deployments

kubectl get deployment redis-deployment

kubectl get pods

kubectl logs redis-deployment-554856c7bb-htpl9

kubectl delete deployment redis-deployment

kubectl logs py-app-deployment-78bb55cc88-b7n9r



*************////////


///////////////////////////***************************
///////////************/ 

Read the resource information
kubectl get services -n kube-system

kubectl get deployments -n kube-system

kubectl get pods -n kube-system

type: LoadBalancer

kubectl delete pod <pod name> -n kube-system

kubectl describe service <service name> -n kube-system

kubectl describe service default-http-backend  -n kube-system


To create the deployment
kubectl create -f default-backend.yml
kubectl create -f basic-ingress.yml


kubectl logs  <pod name> -n kube-system

kubectl get pods -n kube-system


kubectl logs <pod name> -n kube-system

kubectl describe service default-http-backend -n kube-system

kubectl get service default-http-backend -n kube-system


kubectl describe  deployments default-http-backend -n kube-system

kubectl describe ingress basic-ingress

kubectl delete deployment default-http-backend  -n kube-system
kubectl delete service default-http-backend  -n kube-system

kubectl delete  pod default-http-backend -n kube-system

kubectl delete ingress basic-ingress



