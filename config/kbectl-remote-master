Controlling your cluster from machines other than the control-plane node

In order to get a kubectl on some other computer (e.g. laptop) to talk to your cluster, you need to copy the administrator kubeconfig file from your control-plane node to your workstation like this

scp root@<control-plane-host>:/etc/kubernetes/admin.conf .

sudo scp root@192.168.0.109:/etc/kubernetes/admin.conf /home/admin.conf

sudo kubectl --kubeconfig /home/admin.conf get nodes

 To remove node with remote access

  sudo kubectl --kubeconfig /home/admin.conf  drain kmaster --delete-local-data --force --ignore-daemonsets

  sudo kubectl kubectl --kubeconfig /home/admin.conf delete node kmaster
  sudo kubeadm reset


