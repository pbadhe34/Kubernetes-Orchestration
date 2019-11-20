
***********************8///////

Using Shared Voulme for redis server



sudo kubectl create -f Redis-Persistence-Volume-Windows.yml


sudo kubectl get pv redis-pv-volume

sudo kubectl create -f Redis-PersistentVolumeClaim.yml

sudo kubectl get pvc redis-pv-claim

The output shows that the PersistentVolumeClaim is bound to the PersistentVolume, redis-pv-volume.

 To run the service 

sudo kubectl create -f app-service-volume-NodePort.yml
 

 kubectl get service py-app

kubectl describe service py-app


sudo kubectl logs  host-port-user host-port-container 

sudo kubectl logs  host-port-user mysql-server 

Output is
http://192.168.99.100:30589

Tets with curl as

curl http://192.168.99.100:30589
 
 To scale the deployments
kubectl scale deployment py-app --replicas=5 
kubectl scale deployment redis --replicas=5 


/////////////////*********************
Deployong the microservice service with volume

sudo kubectl create -f MySql-PersistentVoulme-Windows.yml

sudo kubectl get  pv mysql-pv-volume


sudo kubectl create -f MySql-PersistentVoulme-Claim.yml

sudo kubectl get pvc mysql-pv-claim

sudo kubectl create -f Java-mysql-service-volume-NodePort.yml

 
kubectl get services
kubectl get service mysql
kubectl describe service mysql

Output is avaibale at
 http://192.168.99.100:30589

Tets with curl as

curl http://192.168.99.100:3306/users




////*************
MySql Container management
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
  


sudo kubectl get services

sudo kubectl describe service azure-vote-front

sudo kubectl get service azure-vote-front

sudo kubectl get service azure-vote-front --watch=true


*********************////



/////////********
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

?////***************
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



