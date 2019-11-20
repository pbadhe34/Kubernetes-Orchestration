
kubectl rollout status deployment/default-http-backend


kubectl rollout status deployment/nginx-ingress-controller


Updating a Deployment by changing the image

kubectl set image deployment/default-http-backend to different version

kubectl rollout status deployment/nginx-deployment
 

Run kubectl get rs to see that the Deployment updated the Pods by creating a new ReplicaSet and scaling it up to 3 replicas, as well as scaling down the old ReplicaSet to 0 replicas.

Rolling Back a Deployment

ubectl set image deployment/default-http-backend nginx=nginx:1.91

kubectl get rs

 Rollout History of a Deployment
First, check the revisions of this deployment:

kubectl rollout history deployment/nginx-deployment

Rolling Back to a Previous Revision

kubectl rollout undo deployment/nginx-deployment
deployment "nginx-deployment" rolled back

 Or by kubectl rollout undo deployment/nginx-deployment --to-revision=2
deployment "nginx-deployment" rolled back
 