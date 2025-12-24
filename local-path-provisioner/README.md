# Local Path Provisioner by Rancher

Install [rancher/local-path-provisioner:v0.0.32](https://github.com/rancher/local-path-provisioner/tree/v0.0.32) and use it as default StorageClass:

```shell
kubectl apply -f manifests
```

The default path to create local storage is `/opt/local-path-provisioner`, you can modify this at `./manifests/ConfigMap.yml`, it can even be RAM Disk if you have sufficient RAM and do not really need persistence.