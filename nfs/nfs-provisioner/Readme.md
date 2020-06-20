This repo can used to dynamically provision NFS persistent volumes in your Kubernetes cluster. After we have provisioned NFS-Provisioner Pod Persistent volumes will get created dyanmically whenever there is a persistent volume claim.
Dynamic Provisioning is not avaliable on OnPremise but it is avalible on Cloud K8S as Service like in AWS EKS, GCP etc.
We donot have to create PV , We just create PVC and based of it needs/configuration PV is provisioned.

For this we must have NFS Server configured for our Kubernetes Nodes(Nodes IP Range in /etc/exports) & we as using /srv/nfs/kubedata NFS-mount Directory.

For NFS Client Provisioner - Create ServiceAccount, Role, RoleBinding, ClusterRole, ClusterRoleBinding, StorageClass, Deployment 

On K8s Nodes we can run below commands to verify whether NFS is working with K8S Worker Nodes or not 
   1. #showmount -e <Ip of NFS Server>
   2. Mount NFS Shared Directory to Worker Node
      #mount -t nfs <Ip of NFS Server>:/srv/nfs/kubedata /mnt  
   3. After it is successfully mounted unmount it 
      #umount /mnt 

After deploying NFS Client Provisioner Pod, if we create PVC  it dynamically provisions PV & on NFS Server under /srv/nfs/kubedata a new directory is created & 
