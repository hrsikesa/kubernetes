# NFS as storage backend for K8S Cluster
This repo can be used for using NFS as PV 

For this we must have NFS Server configured for our Kubernetes Nodes(Add K8S Nodes IP Range in /etc/exports) & we as using /srv/nfs/kubedata as NFS shared Directory.

On K8s Nodes we can run below commands to verify whether NFS is working with K8S Worker Nodes or not 
  ```sh
  1. # showmount -e <Ip of NFS Server>
   2. Mount NFS Shared Directory to Worker Node
      # mount -t nfs <Ip of NFS Server>:/srv/nfs/kubedata /mnt  
   3. After it is successfully mounted unmount it 
      # umount /mnt
```

To configure NFS Shared Directory as Persistence Volume add server: <nfs server ip> in [pv-nfs.yaml](https://github.com/hrsikesa/kubernetes/blob/master/nfs/nfs-pv/nfs-pv.yaml) and use it to create Persistent Volume
To create Persistent Volume Claim use [pvc-nfs.yaml](https://github.com/hrsikesa/kubernetes/blob/master/nfs/nfs-pv/nfs-pvc.yaml)
To create sample nginx deployment which uses PV use [nfs-nginx.yaml](https://github.com/hrsikesa/kubernetes/blob/master/nfs/nfs-pv/nfs-nginx.yaml)

After creating Sample Nginx Deployment 
 ```sh
1. Create index.html on NFS Server in this location /srv/nfs/kubedata
    & add any content in index.html 
2. Create NodePort Service for Nginx Deployment, so we can access index.html via Browser.
   # kubectl expose deployment nginx-deploy --port=80 --type=NodePort
3. Now any change we make in index.html on NFS Server same will be reflected in Nginx Pod. 
   Again access it via browser
```


