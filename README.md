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