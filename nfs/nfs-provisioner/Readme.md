# Kubernetes NFS-Client Provisioner
**nfs-client** is an automatic provisioner that use your *existing and already configured* NFS server to support dynamic provisioning of Kubernetes Persistent Volumes via Persistent Volume Claims.

This repo can used to dynamically provision NFS persistent volumes in your Kubernetes cluster. After we have provisioned NFS-Provisioner Pod,  Persistent volumes will get created dyanmically whenever we create persistent volume claim.
Dynamic Provisioning is not avaliable on OnPremise K8S but it is avalible on Cloud K8S as Service like  AWS EKS, GCP etc.
We donot have to create PV , We just create PVC and based of it needs/configuration PV is provisioned.

For this we must have NFS Server configured for our Kubernetes Nodes(Add K8S Nodes IP Range in /etc/exports) & we as using /srv/nfs/kubedata as NFS shared Directory.

For NFS Client Provisioner - 
Create ServiceAccount, Role, RoleBinding, ClusterRole, ClusterRoleBinding, StorageClass, Deployment 
In [nfs-provisioner-deployment.yaml](https://github.com/hrsikesa/kubernetes/blob/master/nfs/nfs-provisioner/nfs-provisioner-deployment.yaml) we have to specify our NFS Server Location(IP/Hostname) & NFS shared directory path . NFS shared directory will be mounted to NFS Client Provisioner Pod 

On K8s Woker Nodes we can run below commands to verify whether NFS is working with K8S Worker Nodes or not 
```sh
   1. #showmount -e <Ip of NFS Server>
   2. Mount NFS Shared Directory to Worker Node
      # mount -t nfs <Ip of NFS Server>:/srv/nfs/kubedata /mnt  
   3. After it is successfully mounted unmount it 
      # umount /mnt 
```
 
After creating all required objects, if we create PVC it will dynamically provisions a new PV & on NFS Server under /srv/nfs/kubedata a new directory is created for every PVC/PV we create.

For more information refer to [this GitHub Link](https://github.com/kubernetes-incubator/external-storage/blob/master/nfs-client/README.md)
