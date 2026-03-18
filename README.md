# 用于快速初始化一个 k8s 集群的脚本

目前仅适用于节点全部为刚装好的 ubuntu 裸机。确保执行本脚本的机器可以 ssh 到全部节点，并安装好 ansible。

## 0. 中国大陆需要的额外配置

参考 `china` 目录。

## 1. 配置ssh

编辑 `ssh/hosts.txt` 列出所有节点（可被 ssh 连接）的 hostname/ip。

```shell
cd ssh
./keys.sh
```

## 2. 分配 controller 和 worker

复制 `inventory.yml.example` 创建一份 `inventory.yml`，编辑该文件分配 controller 和 worker。

## 3. 执行 playbook

准备环境、安装依赖：

```shell
# 若需要修改 k8s 集群版本可以修改该 playbook 的变量
ansible-playbook -i inventory.yml setup_common.yml
```

初始化一个新集群：

```shell
ansible-playbook -i inventory.yml setup_cluster.yml
```

删除已有的集群：

```shell
ansible-playbook -i inventory.yml setup_rm_cluster.yml
```

将一个新机器加入集群（作为 worker），先在 `inventory.yml` 中增加 `new_workers` 的节点，然后：

```shell
ansible-playbook -i inventory.yml setup_common.yml --limit new_workers
ansible-playbook -i inventory.yml setup_new_worker.yml
```

注意新的 worker k8s 版本不能高于控制平面！(即使是小版本)

##  4. 自定义插件

创建的集群使用 Flannel 作为 CNI 插件。

若需要 CSI 插件，请参考 `./csi/` 目录。

若需要负载均衡器，请参考 `./metallb/` 目录。