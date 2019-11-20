>kubectl get services -n kube-system

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



