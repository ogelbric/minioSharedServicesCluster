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


## Inspration Document

https://min.io/docs/minio/kubernetes/upstream/index.html?ref=docs-redirect



