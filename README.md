# MinIO Shared Services Deployment 

Make sure you are supervisor Namespace where the shared service cluster is going to be created (in my case namespace1000)

```
k config use-context namespace1000

k get nodes

NAME                               STATUS   ROLES                  AGE   VERSION
4223110e3b11a02b6b177db0551f41ec   Ready    control-plane,master   76d   v1.24.9+vmware.wcp.1
42234f3fd4ee6ad71dde6b4da15622e5   Ready    control-plane,master   76d   v1.24.9+vmware.wcp.1
422398077f99efb5bf4475df395f65f3   Ready    control-plane,master   76d   v1.24.9+vmware.wcp.1

```

Create the cluster

```
kubectl apply -f https://raw.githubusercontent.com/ogelbric/minioSharedServicesCluster/main/miniocluster.yaml

```

Two things to note in the cluster yaml file are 1) a /data mount point and 2) a volume by the name localvolume

```
      - capacity:
            storage: "10Gi"
          mountPath: "/data"
          name: localvolume
```

Checking on our cluster

```
k get clusters
NAME              PHASE         AGE    VERSION
miniocluster      Provisioned   6m9s   v1.23.8+vmware.2
tmclocalcluster   Provisioned   43d    v1.24.9+vmware.1
[root@localhost minio]#

```

![GitHub](miniocluster.png)

Log onto new cluster

```
kubectl vsphere login --server 192.168.2.100 --vsphere-username administrator@vsphere.local --tanzu-kubernetes-cluster-namespace  namespace1000 --tanzu-kubernetes-cluster-name miniocluster --insecure-skip-tls-verify

k get nodes
NAME                                              STATUS   ROLES                  AGE   VERSION
miniocluster-5j55r-mvddn                          Ready    control-plane,master   14m   v1.23.8+vmware.2
miniocluster-node-pool-1-9ljtz-694979f49c-cj4vw   Ready    <none>                 10m   v1.23.8+vmware.2

```






## Inspration Document

https://min.io/docs/minio/kubernetes/upstream/index.html?ref=docs-redirect



