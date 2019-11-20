The PYthon app image pbadhe34/my-apps:app1 has been modified to 
look for the redis host on localhost machine.
This redis container deployed in the same POD is recognozed as redis runningn on localhost:6379 



kubectl get all


kubectl get all -n kube-system

List all supported resource types along with their shortnames, API group, whether they are namespaced

kubectl api-resources

Exploring API resources:

kubectl api-resources --namespaced=true 
 
    # All namespaced resources
kubectl api-resources --namespaced=false
     # All non-namespaced resources

kubectl api-resources -o name                # All resources with simple output (just the resource name)

kubectl api-resources -o wide                # All resources with expanded (aka "wide") output

kubectl api-resources --verbs=list,get       # All resources that support the "list" and "get" request verbs

kubectl api-resources --api-group=extensions 

# All resources in the "extensions" 


************************
Formatting options
-o=custom-columns=<spec>	Print a table using a comma separated list of custom columns
-o=custom-columns-file=<filename>	Print a table using the custom columns template in the <filename> file
-o=json	Output a JSON formatted API object
-o=jsonpath=<template>	Print the fields defined in a jsonpath expression
-o=jsonpath-file=<filename>	Print the fields defined by the jsonpath expression in the <filename> file
-o=name	Print only the resource name and nothing else
-o=wide	Output in the plain-text format with any additional information, and for pods, the node name is included
-o=yaml	Output a YAML formatted API object
Kubectl output verbosity and debugging

*******************
kubectl create  -f hostNetwork-Py.yml

kubectl create  -f hostPort-Py1.yml

kubectl create  -f hostPort-Py2.yml

kubectl create  -f  hostPort-Linked-Py3.yml

sudo kubectl create  -f  SharedVolume-Containers.yml



