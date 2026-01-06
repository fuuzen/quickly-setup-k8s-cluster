# MetalLB

[安装 MetalLB](https://metallb.universe.tf/installation/) 并启用 L2 模式，作为集群的负载均衡器。

```shell
# IPVS 模式 kube-proxy 需要启用 strictARP
kubectl get configmap kube-proxy -n kube-system -o yaml | \
sed -e "s/strictARP: false/strictARP: true/" | \
kubectl apply -f - -n kube-system
# 安装 MetalLB
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.15.3/config/manifests/metallb-native.yaml
```

`./manifests/IPAddressPool.yml` 定义了可被分配的 IP 池，这里的 IP 网段需要是节点(最好包括开发机)所在内网(确保可被路由)的一段空闲、不会冲突的 ip。当然也可以用一段随便的 ip 然后在开发机静态路由这一段 ip 到集群的节点上。