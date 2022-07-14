Dynamic NFS provisioning in Kubernetes

GitHub Repo - https://github.com/amitpawarcbg/NFS-storageclass.git

Setup NFS server on ubuntu Linux -

On node for which you need to setup NFS server run below commands to configure NFS server.
You may change the name of the NFS share as per your requirement.

* apt install nfs-server
* apt install nfs-common
* mkdir -p /nfs/kubedata; chown nobody /nfs/kubedata
* vi /etc/exports >> /nfs/kubedata *(rw,sync,no_subtree_check,no_root_squash,no_all_squash,insecure)
* systemctl enable nfs-server
* systemctl status nfs-server
* exportfs -rav

Deploy NFS provisioner -
On Master node execute below commands to setup NFS provisioner.
Clone the GitHub Repo https://github.com/amitpawarcbg/NFS-storageclass.git

* git clone https://github.com/amitpawarcbg/NFS-storageclass.git
* cd /NFS-storageclass
* kubectl apply -f rbac.yaml
* kubectl apply -f class.yaml
* vi deployment.yaml >> #change the nfs server IP and NFS path
* kubectl apply -f deployment.yaml
* kubectl get pods ##Check for the nfs-client-provisioner pod status
* kubectl get sc
* kubectl apply -f test-claim.yaml ##To test by creating sample pvc.
* kubectl get pvc
