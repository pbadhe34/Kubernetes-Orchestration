  

 
 
docker service inspect --pretty app_web

Read the replicas

docker service inspect --format='{{.Spec.Mode.Replicated.Replicas}}' app_web

To read the publshed port
docker service inspect --format='{{.Spec.EndpointSpec.Ports}}' app_web
 
 
 


//////////////////*****
To Scale the app by service
1. You can scale the app by changing the replicas value
 in docker-compose.yml, saving the change, and re-running 
the docker stack deploy command:

2. Use the docker service scale without redploying the yml

docker service scale <service-name=number of instances>

docker service scale app_web=5

docker service scale app_redis=2

docker container ls -q

docker service scale app_web=2

docker container ls -q
 

docker node ls 

docker ps  

docker inspect <container ID>


docker service ps my-service_web 

docker container ls -q

docker service ps my-service_web
 

**********************/////

Kill one of the container
docker stop id
 
and check the swarm action  

Docker will do an in-place update, no need to tear the stack down first or kill any containers.

Now, re-run docker container ls -q to see the deployed instances reconfigured. If you scaled up the replicas, more tasks, and hence, more containers, are started.
/////////////***

Take down the app and the swarm
Take the app down with docker stack rm:

docker stack rm app_web

docker inspect  app_web

One node is runnimng
docker node ls

Take down the (node)swarm with 
docker swarm leave --force

To remove all conatiners
docker rm $(docker ps -a -q)

*********//

