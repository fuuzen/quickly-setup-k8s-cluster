# Container Storage Interface Plugin

## Local Path Provisioner by Rancher

Install [rancher/local-path-provisioner:v0.0.32](https://github.com/rancher/local-path-provisioner/tree/v0.0.32) and use it as default StorageClass, which is also provided in k3s/rke2:

```shell
kubectl apply -f local-path-provisioner
```

The default path to create local storage is `/opt/local-path-provisioner`, you can modify this at `./local-path-provisioner/ConfigMap.yml`, it can even be RAM Disk if you have sufficient RAM and do not really need persistence.

## Other Local Storage Options

- [OpenEBS](https://github.com/openebs/openebs)
- [Sig-Storage Local **Static** Provisioner](https://github.com/kubernetes-sigs/sig-storage-local-static-provisioner)