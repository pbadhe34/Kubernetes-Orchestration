minikube version
kubectl version

With a VirtualVox VM driver, ,minikube start command without specifying a driver:

The default VM driver is VirtualBox.


sudo minikube start

To get the addons on Minikube

minikube addons list

minikube start --vm-driver=kvm

minikube start --vm-driver=hyperkit

The --vm-driver=hyperkit flag specifies that you are using Docker for Mac. 
With Proxy configuration for Internet connection

minikube start --vm-driver=hyperkit --docker-env HTTP_PROXY=http://your-http-proxy-host:your-http-proxy-port  --docker-env HTTPS_PROXY=http(s)://your-https-proxy-host:your-https-proxy-port


kubectl cluster-info

set the Minikube context. The context is what determines which cluster kubectl is interacting with. 
You can see all your available contexts in the ~/.kube/config file.

kubectl config use-context minikube

Verify that kubectl is configured to communicate with your cluster:

kubectl cluster-info

kubectl get pods --all-namespaces

To get list the nodes in our cluster by running:

$ kubectl get nodes

kubectl run hello-minikube --image=k8s.gcr.io/echoserver:1.4 --port=8080 --hostport=8090

kubectl run hello-minikube --image=k8s.gcr.io/echoserver:1.4 --port=8080 --hostport=8090 
--replicas=3



kubectl run hello-minikube --image=k8s.gcr.io/echoserver:1.4 --port=8080
deployment "hello-minikube" created
$ kubectl expose deployment hello-minikube --type=NodePort
service "hello-minikube" exposed

Web UI (Dashboard)

Dashboard is a web-based Kubernetes user interface. We can use Dashboard to deploy containerized applications to a Kubernetes cluster, troubleshoot our containerized application, and manage the cluster itself along with its attendant resources.

To open the Kubernetes dashboard:


 sudo minikube dashboard

Minikube context

The context is what determines which cluster kubectl is interacting with.
 We can see all our available contexts in the ~/.kube/config file:

Verify that kubectl is configured to communicate with our cluster:

$ kubectl cluster-info

need to set minikube context, we can do as the following:

$ kubectl config use-context minikube


To shut the cluster down, type "minikube stop":

$ minikube stop

 sudo minikube delete

The kubectl config file is
 /home/dell/.kube/config

The minikube config file is

eval $(minikube docker-env)
/////////********

Error restarting cluster:  restarting kube-proxy: waiting for kube-proxy to be up for configmap update: timed out waiting for the condition

sudo minikube service app
Waiting, endpoint for service is not ready yet...


================================================================================


************************************************************
 Connect to pod container

sudo kubectl exec  -it host-port-py-pod -- /bin/bash
  ls
  cat hosts
////////////******

  Service Deployments


*******///******

sudo kubectl get pods

sudo kubectl describe pod app-86d87b4b86-mj959
sudo kubectl logs app-86d87b4b86-mj959

sudo kubectl delete  pod mypod


Connect to the single container in he POD

sudo kubectl exec  -it mypod
ls
ps aux

Run individual commands on the container
sudo kubectl exec mypod ls

sudo kubectl exec mypod ps aux

sudo kubectl exec mypod env


Delete all pods
sudo kubectl delete pods --all

sudo kubectl get deployments

sudo kubectl delete  deployments 

sudo kubectl delete  deployments --all


kubectl get pods --all-namespaces

kubectl  create -f hostNetwork-aspcore.yml


sudo kubectl  create -f hostNetwork-Py.yml

sudo kubectl get events 
 
 
kubectl get pods 

kubectl  logs asppod

kubectl   logs mc1
***********//////***********
Scaling Services

sudo kubectl create -f app-service-persistent-volume.yml

sudo kubectl describe pod pod-localhost-container


sudo kubectl get services

sudo kubectl describe service py-app

sudo kubectl get service py-app --watch=true

sudo kubectl get pods

# Scale replication controller named 'userData' to 3.
kubectl scale --replicas=3 rc/userData

# Scale a resource identified by type and name specified in "user.yaml" to 3.
kubectl scale --replicas=3 -f user.yaml

# If the deployment named mysql's current size is 2, scale mysql to 3.
kubectl scale --current -replicas=2 --replicas=3 deployment/mysql

# Scale multiple replication controllers.
kubectl scale --replicas=5 rc/foo rc/bar rc/baz

# Scale job named 'cron' to 3.
kubectl scale --replicas=3 job/cron

//////************************


////////////////***************

Multi Container PODS

sudo kubectl create -f hostPort-link-localhost.yml

In case of  pod having multi containers

sudo kubectl describe pod pod-localhost-container

to see all of the containers in this pod.

kubectl describe pod/pod-localhost-container -n default

sudo kubectl logs <podName> <container name>

sudo kubectl logs pod-localhost-container

sudo kubectl logs pod-localhost-container host-port-web

sudo kubectl logs pod-localhost-container redis-container

Attach to container/run terminal on the container

sudo kubectl exec -it pod-localhost-container --container host-port-web -- /bin/bash

  ls
  

sudo kubectl exec -it pod-localhost-container --container redis-container -- /bin/bash

Resraet the  redis container to check the counts restored
kubectl exec POD_NAME -c CONTAINER_NAME reboot


sudo apt-get install --reinstall upstart
sudo kubectl exec pod-localhost-container --container redis-container env
sudo kubectl exec pod-localhost-container --container redis-container pwd

sudo kubectl create -f hostPort-link-redis-volume.yml

sudo kubectl create -f hostPort-link-localhost-NoPort.yml

***********************8///////

Using Shared Voulme for redis server

sudo kubectl create -f Persistence-Volume.yml

sudo kubectl get pv redis-pv-volume


sudo kubectl create -f PersistentVolumeClaim.yml

sudo kubectl get pvc redis-pv-claim

The output shows that the PersistentVolumeClaim is bound to the PersistentVolume, redis-pv-volume.

 To run the pod 

sudo kubectl create -f app-link-redis-persistent-volume.yml
 

sudo kubectl describe pod host-port-user
sudo kubectl logs  host-port-user host-port-container 

sudo kubectl logs  host-port-user mysql-server 


/////////////////*********************
Deployong the microservice pods

sudo kubectl create -f PersistentVoulme.yml

sudo kubectl get  pv task-pv-volume


sudo kubectl create -f PersistentVoulme-Claim.yml

sudo kubectl get pvc task-pv-claim

sudo kubectl create -f Linked-DB-persistent-Volume.yml

sudo kubectl describe pod host-port-user

sudo kubectl logs  host-port-user host-port-container 
sudo kubectl logs  host-port-user mysql-server 

copy files to pod-->Container

sudo kubectl cp table.sql host-port-user:/table.sql -c mysql-server
sudo kubectl cp records.sql host-port-user:/records.sql -c mysql-server



sudo kubectl exec -it host-port-user --container mysql-server -- /bin/bash

mysql  -u root  -p userservice < table.sql

mysql  -u root  -p userservice < records.sql

mysql -uroot -p userservice -e "commit"  


mysql -uroot -p userservice -e "select * from users"  

Run the curl client to add more frecords with post method.

/////////*****************
  sudo kubectl create -f app-vote.yml


sudo kubectl get services

sudo kubectl describe service azure-vote-front

sudo kubectl get service azure-vote-front

sudo kubectl get service azure-vote-front --watch=true


*********************////



kubectl   describe pod asppod

kubectl get pods --all-namespaces

kubectl describe rc kubernetes-dashboard --namespace=kube-system 

kubectl logs kubernetes-dashboard --namespace=kube-system 


kubectl  delete pod testpod

Access this app on http://192.168.99.100:80/ in the browser

kubectl --alsologtostderr --v=6 run my-nginx --image=nginx --port=80
 
 To delete the pod created
 kubectl   delete pod mypod


kubectl --alsologtostderr --v=8  create -f hostNetwork-pod.yml

curl -v http://192.168.99.100:80

The host-Port  node/app accessible on http://192.168.99.100:9096/ which is mapped tohttp://container-ip:80

kubectl get svc external-lb-service

kubectl get services external-lb-service

At the end stop cluster by minikube stop command



///////////////////////********
Create deployment from command line
sudo kubectl run app --image=pbadhe34/my-apps:app1 --port=8090

sudo kubectl run nginx-app --image=nginx --port=80

Expose deployments by creating service

Create a service for the deployment which serves on port 8080 and connects to the containers on port 80.
sudo kubectl expose deployment nginx-app --port=8080 --target-port=80

sudo kubectl expose deployment app --port=8090 --target-port=8090

Gets the kubernetes URL(s) for the specified service in your local cluster
sudo minikube service nginx-app



