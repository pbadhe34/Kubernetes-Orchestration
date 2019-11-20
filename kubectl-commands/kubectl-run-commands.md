minikube start --logtostderr --alsologtostderr

set the HTTP_PROXY or HTTPS_PROXY variables in minikube start --docker-env

minikube.exe version
minikube.exe delete 
minikube.exe start --help
minikube get-k8s-versions
minikube.exe status
minikube.exe ip
minikube.exe dashboard --url=true

https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/

https://www.stratoscale.com/blog/kubernetes/kubernetes-how-to-share-disk-storage-between-containers-in-a-pod/

https://kubernetes.io/docs/tasks/configure-pod-container/configure-volume-storage/

 kubectl run -it --rm --image=mysql:5.6 --restart=Never mysql-client -- mysql -h mysql -ppassword

https://kubernetes.io/docs/tasks/run-application/run-single-instance-stateful-application/



kubectl create -f Task-persistentVoulme.yml

kubectl get pv task-pv-volume


kubectl create -f Task-Task-PV-Claim.yml

kubectl get pvc task-pv-claim

The output shows that the PersistentVolumeClaim is bound to the PersistentVolume, task-pv-volume.

 To run the pod 

kubectl create -f Task-Linked-DB.yml

Deploy the
e PV and PVC of the YAML file:

kubectl create -f https://k8s.io/docs/tasks/run-application/mysql-pv.yaml

Deploy the contents of the YAML file:

kubectl create -f https://k8s.io/docs/tasks/run-application/mysql-deployment.yaml

kubectl describe deployment mysql

Run mysql in pod
kubectl run -it --rm --image=mysql:5.6 --restart=Never mysql-client -- mysql -h mysql -ppassword


To Create some data on the  MySQL server:

$ export MYSQLPOD=$(kubectl get pods -n test-ebs -l app=mysql --no-headers | awk '{print $1}')
$ kubectl logs -n test-ebs $MYSQLPOD
$ kubectl exec -n test-ebs -ti $MYSQLPOD -- mysql --user=root --password=password
mysql> create database TEST_1234;
mysql> exit



kubectl  create -f Linked-containers.yml


kubectl  create -f hostNetwork-Py.yml
 
 
kubectl get pods 

kubectl   logs asppod

kubectl   describe pod asppod

kubectl get pods --all-namespaces

kubectl describe rc kubernetes-dashboard --namespace=kube-system 

kubectl logs kubernetes-dashboard --namespace=kube-system 


kubectl  delete pod testpod

  Access this app on http://192.168.99.100:80/ in the browser

kubectl --alsologtostderr --v=6 run my-nginx --image=nginx --port=80
 
 To delete the pod created
 kubectl   delete pod mypod


Get output from running 'date' from pod abc, using the first container by default

kubectl exec abc date

Get output from running 'date' in app-container from pod Mypod
  kubectl exec Mypod -c app-container date

 To run bash with the container

   kubectl exec Mypod -c app-container "bash"



kubectl --alsologtostderr --v=8  create -f hostNetwork-pod.yml

curl -v http://192.168.99.100:80

The host-Port  node/app accessible on http://192.168.99.100:9096/ which is mapped tohttp://container-ip:80

kubectl get svc external-lb-service

kubectl get services external-lb-service

At the end stop cluster by minikube stop command
