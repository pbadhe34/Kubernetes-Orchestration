Minikube contains a built-in Docker daemon for running containers. 

Normally Minikube uses its docker daemon to pull images from docker hub and run them.


To build the image using the same Docker host as the Minikube VM, so that the images are automatically present with minokibe locally.
To use minikube's built in Docker daemon 
  $ sudo eval $(minikube docker-env)

 later hen you no longer wish to use the Minikube host, 
 you can undo this change by running eval $(minikube docker-env -u).

  Build the  Docker image, using the Minikube Docker daemon (mind the trailing dot):

  docker build -t hello-node:v1 .

  The Minikube VM can run the image , built with minikube docaker daemon.


Create a Deployment

 
