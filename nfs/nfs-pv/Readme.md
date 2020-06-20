Here we are use using NFS as a storage backend for our Kubernetes Cluster.

For this we must have NFS Server configured for our Kubernetes Nodes(Nodes IP Range in /etc/exports) & we as using /srv/nfs/kubedata NFS-mount Directory.

pv-nfs.yaml - to use NFS Shared Directory as Persistence Volume 
server: <nfs server ip>  Insert NFS Server IP

pvc-nfs.yaml - to create PVC 

nfs-nginx.yaml - sample nginx deployment 

 On K8s Nodes we can run below commands to verify whether NFS is working with K8S Worker Nodes or not 
   1. # showmount -e <Ip of NFS Server>
   2. Mount NFS Shared Directory to Worker Node
      # mount -t nfs <Ip of NFS Server>:/srv/nfs/kubedata /mnt  
   3. After it is successfully mounted unmount it 
      # umount /mnt 

1. Create index.html on NFS Server in this location /srv/nfs/kubedata
 & add content to it 

2. Create NodePort Service for Nginx Deployment, so we can access index.html via Browser.
 # kubectl expose deployment nginx-deploy --port=80 --type=NodePort

3. Now any change we make in index.html on NFS Server same will be reflected in Nginx Pod 



