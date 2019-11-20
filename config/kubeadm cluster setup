 
Disable swap  

sudo swapoff -a

  remove any swap entry from /etc/fstab  and reboot
sudo sed -i '/ swap / s/^/#/' /etc/fstab and reboot the mcahine



The default kubeadm Kubelet config file on joining node created 
 /var/lib/kubelet/config.yaml


sudo systemctl status kubelet
journalctl -xeu kubelet


 port check
  sudo lsof -i:10250   (kubelet service) 

  sudo systemctl daemon-reload

  sudo systemctl restart kubelet

  sudo systemctl restart docker


   Kubadm config file on  joining mnode
 /etc/systemd/system/kubelet.service.d/10-kubeadm.conf

 
 sudo gedit /etc/systemd/system/kubelet.service.d/10-kubeadm.conf

sudo kubedam init

 sudo   kubeadm init --ignore-preflight-errors=all

  sudo kubeadm init --pod-network-cidr=10.244.0.0/16  --apiserver-advertise-address 192.168.0.109   --ignore-preflight-errors=all

//////////////////*******
kubeadm init --pod-network-cidr=192.168.0.0/16

After running kubeadm init successfully we get output that master node is initialised & we get some command to setup kubectl & also command for joining worker nodes to this master node.

If using Calico as network plugin, use 
"--pod-network-cidr=192.168.0.0/16" option
*****************************************


To make kubectl work for the non-root user, run these commands, which are also part of the kubeadm init output:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config


*******************************************************
 Alternatively, ONLY FOR the root user, you can run:

 export KUBECONFIG=/etc/kubernetes/admin.conf

   *********************************************************
**************************
  To read the environment values

  printenv SHELL

  printenv LOGANME
  
  printenv KUBECONFIG

*****************************
   kubectl get nodes

  NAME    STATUS     ROLES    AGE   VERSION
knode   NotReady   master   16m   v1.16.1



  kubectl get nodes -o wide

  kubectl get pods -o wide

  kubectl cluster-info

  Check health status of various components of control plane.

 sudo kubectl get componentstatus


  kubectl --kubeconfig=$HOME/.kube/config config view

  kubectl --kubeconfig=$HOME/.kube/config cluster-info
  

  kubectl config view
   kubectl --kubeconfig=$HOME/.kube/config cluster-info


   kubectl --kubeconfig=$HOME/.kube/config version

  
   

  kubectl --server=192.168.0.109:6443 get pod -o wide

  kubectl version -o json

**********************
  netstat -aon | findstr "8080" on windows
 
 On Linux
  netstat -aon | grep "6443"

  netstat -ano -p tcp
********************

kubectl cluster-info
  Kubernetes master is running at https://192.168.0.109:6443
KubeDNS is running at https://192.168.0.109:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.


  Check health status of various components of control plane.

kubectl get componentstatus

************************
 Firewall on ubuntu
  sudo ufw enable
   sudo ufw status
   sudo ufw allow 8443/tcp
sudo ufw allow from 172.17.0.0/16  

*****************

 2.  Installing a pod network add-on

    Caution: This section contains important information about installation and deployment order. Read it carefully before proceeding.

You must install a pod network add-on so that your pods can communicate with each other.

The network must be deployed before any applications. Also, CoreDNS will not start up before a network is installed. kubeadm only supports Container Network Interface (CNI) based networks.


  The  Pod network must not overlap with any of the host networks as this can cause issues. 
  If you find a collision between your network plugin’s preferred Pod network and some of your host networks,  you should think of a suitable CIDR replacement and use that during kubeadm init with --pod-network-cidr and as a replacement in your network plugin’s YAML.

    Install a pod network add-on with the following command on the control-plane node or a node that has the kubeconfig credentials:

  kubectl apply -f <add-on.yaml>  : third-party Pod Network Provider.

You can install only one pod network per cluster.

  Flannel CNI Proivider

  For flannel to work correctly, you must pass  --pod-network-cidr=10.244.0.0/16 to kubeadm init.

Set /proc/sys/net/bridge/bridge-nf-call-iptables to 1 by running sysctl net.bridge.bridge-nf-call-iptables=1 to pass bridged IPv4 traffic to iptables’ chains. 
 This is a requirement for some CNI plugins to work.

Make sure that your firewall rules allow UDP ports 8285 and 8472 traffic for all hosts participating in the overlay network.  

Note that flannel works on amd64, arm, arm64, ppc64le and s390x under Linux. Windows (amd64) is claimed as supported in v0.11.0 but the usage is undocumented.

  kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/2140ac876ef134e0ed5af15c65e414cf26827915/Documentation/kube-flannel.yml

  WeaveNet CNI Provider
  https://www.weave.works/docs/net/latest/kubernetes/kube-addon/
  Set /proc/sys/net/bridge/bridge-nf-call-iptables to 1 by running sysctl  net.bridge.bridge-nf-call-iptables=1 to pass bridged IPv4 traffic to iptables’ chains. This is a requirement for some CNI plugins to work.

  verify by : sudo cat /proc/sys/net/bridge/bridge-nf-call-iptables


   Weave Net works on amd64, arm, arm64 and ppc64le without any extra action required. Weave Net sets hairpin mode by default. This allows Pods to access themselves via their Service IP address if they don’t know their PodIP.

Add weavenet pod network addon

  kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"



  kubectl get nodes

  kubectl get nodes knode
   
  kubectl describe nodes knode

 

  Output:
 NAME    STATUS   ROLES    AGE   VERSION
 knode   Ready    master   84m   v1.16.1


  Once a pod network has been installed, you can confirm that it is working by checking that the CoreDNS pod is Running in the output of 

  kubectl get pods --all-namespaces

  [Prakash@   knode   ~]$ kubectl get pods --all-namespaces
NAMESPACE     NAME                            READY   STATUS              RESTARTS   AGE
kube-system   coredns-5644d7b6d9-5kf8q        0/1     Pending             0          74m
kube-system   coredns-5644d7b6d9-9qzxd        0/1     Pending             0          74m
kube-system   etcd-knode                      1/1     Running             0          73m
kube-system   kube-apiserver-knode            1/1     Running             0          73m
kube-system   kube-controller-manager-knode   1/1     Running             0          73m
kube-system   kube-proxy-vgbtc                1/1     Running             0          74m
kube-system   kube-scheduler-knode            1/1     Running             0          73m
kube-system   weave-net-lmh9r                 0/2     ContainerCreating   0          34s


  https://kubernetes.io/docs/tasks/access-application-cluster/list-all-running-container-images/

  Lst containers by pods

  kubectl get pods --all-namespaces -o jsonpath="{.items[*].spec.containers[*].image}"

 Raw output
  
  k8s.gcr.io/coredns:1.6.2 k8s.gcr.io/coredns:1.6.2 k8s.gcr.io/etcd:3.3.15-0 k8s.gcr.io/kube-apiserver:v1.16.2 k8s.gcr.io/kube-controller-manager:v1.16.2 k8s.gcr.io/kube-proxy:v1.16.2 k8s.gcr.io/kube-scheduler:v1.16.2 docker.io/weaveworks/weave-kube:2.6.0 docker.io/weaveworks/weave-npc:2.6.0


  ecursively return all fields named image for all items returned.

kubectl get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.containers[*]}{.image}{", "}{end}{end}' |\
sort

  kubectl get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.containers[*]}{.image}{", "}{end}{end}' |\
sort

Output:
coredns-5644d7b6d9-5kf8q:	k8s.gcr.io/coredns:1.6.2, 
coredns-5644d7b6d9-9qzxd:	k8s.gcr.io/coredns:1.6.2, 
etcd-knode:	k8s.gcr.io/etcd:3.3.15-0, 
kube-apiserver-knode:	k8s.gcr.io/kube-apiserver:v1.16.2, 
kube-controller-manager-knode:	k8s.gcr.io/kube-controller-manager:v1.16.2, 
kube-proxy-vgbtc:	k8s.gcr.io/kube-proxy:v1.16.2, 
kube-scheduler-knode:	k8s.gcr.io/kube-scheduler:v1.16.2, 
weave-net-lmh9r:	docker.io/weaveworks/weave-kube:2.6.0, docker.io/weaveworks/weave-npc:2.6.0, 


  List Containers filtering by Pod label
  kubectl get pods --all-namespaces -o=jsonpath="{..image}" -l app=nginx


  kubectl get pods --namespace kube-system -o jsonpath="{..image}"



 And once the CoreDNS pod is up and running, you can continue by joining your nodes.




If your network is not working or CoreDNS is not in the Running state, checkout our troubleshooting docs.
Control plane node isolation



    Control plane node isolation

By default, the cluster will not schedule pods on the control-plane node for security reasons. If you want to be able to schedule pods on the control-plane node, e.g. for a single-machine Kubernetes cluster for development, run:

 kubectl taint nodes --all node-role.kubernetes.io/master-


  node/knode untainted

  Deploy Dashboard web ui
 https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

  kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta4/aio/deploy/recommended.yaml

Establish the requires firewall settings

#!/bin/sh
echo "Setting Firewallrules"
firewall-cmd --permanent --add-port=6443/tcp

 The 'ufw' command on Ubuntu 16.04

firewall-cmd --permanent --add-port=2379-2380/tcp
firewall-cmd --permanent --add-port=10250/tcp
firewall-cmd --permanent --add-port=10251/tcp
firewall-cmd --permanent --add-port=10252/tcp
firewall-cmd --permanent --add-port=10255/tcp

firewall-cmd --permanent --add-port=10248/tcp
firewall-cmd --reload

echo "And enable br filtering"
modprobe br_netfilter
echo '1' > /proc/sys/net/bridge/bridge-nf-call-iptables


  Firwall rules for dashboardUI
  firewall-cmd --state


firewall-cmd --get-active-zones
  

  Open port 80 and port 443 port.

The port 80 and port 443 ports are listed with Firewalld as http and https services. To temporarily open both ports execute:

# firewall-cmd --zone=public --add-service=http
# firewall-cmd --zone=public --add-service=https

  Open port 80 and port 443 port permanently. Execute the below commands to open both ports permanently, hence, make the settings persistent after reboot:

# firewall-cmd --zone=public --permanent --add-service=http
# firewall-cmd --zone=public --permanent --add-service=https
# firewall-cmd --reload


To Flush IPtables
 sudo systemctl stop kubelet
 sudo systemctl stop docker
 sudo iptables --flush
 sudo iptables -tnat --flush
 sudo systemctl start kubelet
 sudo systemctl start docker

 To troibleshoot kubelet roblems
systemctl status kubelet
journalctl -xeu kubelet



  Access the dashboard ui
  http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/


  access to cluster
 https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/

    Authentication Token

  https://kubernetes.io/docs/reference/access-authn-authz/authentication/

kubeadm token create --print-join-command

kubeadm join --token <token> <control-plane-host>:<control-plane-port> --discovery-token-ca-cert-hash sha256:<hash>

can get it by running the following command on the control-plane node:

kubeadm token list

By default, tokens expire after 24 hours. If you are joining a node to the cluster after the current token has expired, you can create a new token by running the following command on the control-plane node:

kubeadm token create   --print-join-command

The output is similar to this:

5didvk.d09sbcov8ph2amjw

If you don’t have the value of --discovery-token-ca-cert-hash, you can get it by running the following command chain on the control-plane node:

openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | \
   openssl dgst -sha256 -hex | sed 's/^.* //'



kubeadm join 192.168.0.109:6443 --token f41vvr.2bgctwoh25hmgjfx   --discovery-token-ca-cert-hash sha256:2439365bbff6d108dd58f797692d09229d8d7c03714542e31c7e88020f3ef692 


kubeadm join 192.168.0.109:6443 --token jke2ys.lf9okzcpfx4aoi55 \
kubeadm join --token bnmvsp.04cx7gfmgfckym9j \
--discovery-token-unsafe-skip-ca-verification 192.168.0.109:6443
 **************************

After the kubelet loads the new configuration, kubeadm writes the /etc/kubernetes/bootstrap-kubelet.conf KubeConfig file, which contains a CA certificate and Bootstrap Token. These are used by the kubelet to perform the TLS Bootstrap and obtain a unique credential, which is stored in /etc/kubernetes/kubelet.conf. When this file is written, the kubelet has finished performing the TLS Bootstrap.


The kubelet drop-in file for systemd

kubeadm ships with configuration for how systemd should run the kubelet. Note that the kubeadm CLI command never touches this drop-in file.

This configuration file installed by the kubeadm DEB or RPM package is written to /etc/systemd/system/kubelet.service.d/10-kubeadm.conf and is used by systemd. 
It augments the basic kubelet.service for RPM (resp. kubelet.service for DEB)):
//////////////////
    The KubeConfig file to use for the TLS Bootstrap is 
 /etc/kubernetes/bootstrap-kubelet.conf, 
  but it is only used if /etc/kubernetes/kubelet.conf does not exist.

    The KubeConfig file with the unique kubelet identity is 
  /etc/kubernetes/kubelet.conf.
    The file containing the kubelet’s ComponentConfig is 
   /var/lib/kubelet/config.yaml.

    The dynamic environment file that contains KUBELET_KUBEADM_ARGS is sourced from 
  /var/lib/kubelet/kubeadm-flags.env.

    The file that can contain user-specified flag overrides with KUBELET_EXTRA_ARGS is sourced from 
  /etc/default/kubelet (for DEBs), or /etc/sysconfig/kubelet (for RPMs). KUBELET_EXTRA_ARGS is last in the flag chain and has the highest priority in the event of conflicting settings.

 


//////////////////////////****************
Tear down

To undo what kubeadm did, you should first drain the node and make sure that the node is empty before shutting it down.

Talking to the control-plane node with the appropriate credentials, run:

 sudo  kubectl drain knode --delete-local-data --force --ignore-daemonsets
 sudo kubectl delete node knode

Then, on the node being removed, reset all kubeadm installed state:


  kubectl -n kube-system get cm kubeadm-config -oyaml

  sudo kubeadm reset

The reset process does not reset or clean up iptables rules or IPVS tables. 
 If you wish to reset iptables, you must do so manually:

 iptables -F && iptables -t nat -F && iptables -t mangle -F && iptables -X

If you want to reset the IPVS tables, you must run the following command:

 ipvsadm -C


