# Setup Servers

This directory contains Ansible playbooks to help set up servers in patch **in China, thanks to GFW**.

- `setup_mirror.yml` Ubuntu apt 换源为镜像站
- `setup_mihomo.yml` 安装 mihomo 并注册到 systemd，配置文件在 `templates`:
  - `templates/config.yaml` mihomo 配置文件，**启用了 TUN 模式**
  - `templates/mihomo.service` systemd 配置文件
  - `templates/provider.yaml` 将订阅的 provider 放在这里