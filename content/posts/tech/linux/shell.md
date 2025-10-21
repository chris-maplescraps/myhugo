+++
title = 'Linux Shell 核心命令速查'
date = 2025-10-21T00:00:00+08:00
draft = false
slug = "linux-shell"
description = "运维与 DevOps 工程师必备的核心命令，用最简单的解释与例子"
summary = "文件/进程/网络/日志/磁盘/包管理/权限/压缩/SSH/Docker/K8s 速查"
tags = [ "技术", "运维", "DevOps" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

# Linux Shell 核心命令速查（运维/DevOps）

这份速查把“日常必用”命令按场景分组，配最短解释与最小例子，一屏掌握、拿来即用。

## 1. 文件与目录
- 查看与导航：
```bash
pwd                 # 显示当前目录
ls -la              # 列出详细文件（含隐藏）
cd /var/log         # 切换目录
```
- 查找：
```bash
find /var/log -name "*.log"     # 按文件名查找
grep -R "ERROR" /var/log        # 递归搜索文本
```
- 创建与移动：
```bash
mkdir -p /data/app/logs         # 递归创建目录
cp app.conf /etc/app/           # 复制文件
mv old.log logs/                # 移动/重命名
rm -rf tmp/                     # 删除目录（危险！确认路径）
```

## 2. 文本查看与处理
- 快速查看：
```bash
cat file.log            # 显示全文（小文件）
less file.log           # 分页查看（q退出）
head -n 50 file.log     # 前 50 行
tail -n 100 file.log    # 后 100 行
tail -f app.log         # 实时追踪日志
```
- 查找筛选：
```bash
grep -n "ERROR" app.log         # 搜索并显示行号
grep -R "timeout" .             # 递归搜索当前目录
```
- 统计与去重：
```bash
wc -l app.log                    # 行数
sort app.log | uniq -c | sort -nr  # 频次统计
```
- awk/sed（最常用场景）：
```bash
awk -F',' '{print $1,$3}' data.csv    # 选取列
sed -n '100,120p' app.log             # 打印指定行范围
sed -i 's/DEBUG/INFO/g' app.conf      # 就地替换（谨慎）
```

## 3. 进程与服务
- 进程查看：
```bash
ps aux | grep app         # 查进程
top                      # 实时监控（htop更好用）
pgrep -f "gunicorn"      # 找到进程ID
```
- 终止与优先级：
```bash
kill -9 <pid>            # 强制杀进程（优先尝试不带 -9）
renice 10 -p <pid>       # 调整优先级
```
- systemd（常见）：
```bash
sudo systemctl status app.service  # 查看状态
sudo systemctl restart app.service # 重启服务
journalctl -u app.service -f       # 实时查看 Unit 日志
```

## 4. 网络与连通性
- 基本连通：
```bash
ping 8.8.8.8             # 测试网络
curl -I https://example.com   # 查看响应头
wget https://example.com/file # 下载文件
```
- 端口与连接：
```bash
ss -tulpn                # 查看监听端口
lsof -i :8080            # 查看占用端口的进程
nc -vz host 80           # 测试端口（TCP）
```
- DNS 与路由：
```bash
dig example.com +short   # 查询 DNS
traceroute example.com   # 路由追踪
```

## 5. 磁盘与文件系统
- 使用情况：
```bash
df -h                # 磁盘占用（人类可读）
du -sh /var/log      # 目录大小汇总
du -h --max-depth=1 /data  # 一级目录大小
```
- 分区与设备：
```bash
lsblk                 # 查看块设备
```

## 6. 压缩与打包
```bash
tar -czf logs.tar.gz logs/   # 打包压缩目录
tar -xzf logs.tar.gz         # 解压
zip -r site.zip public/      # zip 压缩
unzip site.zip               # 解压
```

## 7. 权限与所有者
```bash
chmod 644 file.conf          # 读写权限（所有者可写，其他只读）
chmod -R 755 /usr/local/bin  # 递归设置可执行
chown root:root /etc/app.conf # 变更所有者和组
```

## 8. 包管理（按发行版）
- Debian/Ubuntu：
```bash
sudo apt update && sudo apt install htop
apt list --installed | grep nginx
```
- CentOS/RHEL（Dnf/Yum）：
```bash
sudo dnf install htop   # 或 yum
sudo dnf list installed | grep nginx
```

## 9. 日志与系统信息
```bash
journalctl -xe                 # 最近错误详情
journalctl --since "-2h"       # 最近2小时日志
dmesg | tail                   # 内核消息（启动/设备）
uname -a                       # 内核与系统信息
cat /etc/os-release            # 发行版信息
```

## 10. SSH 与文件传输
```bash
ssh user@host                  # 远程登录
ssh -i ~/.ssh/id_rsa user@host # 指定密钥
scp file user@host:/path/      # 传文件
rsync -avz dir/ user@host:/path/ # 同步目录
ssh-keygen -t ed25519          # 生成密钥
ssh-copy-id user@host          # 上传公钥
```

## 11. Docker 核心
```bash
docker ps                     # 列出容器
docker logs -f <container>    # 跟踪日志
docker exec -it <container> sh # 进入容器
docker inspect <container>    # 查看细节
docker run -d -p 8080:80 nginx # 快速启动
docker stop <container>; docker rm <container> # 停止并删除
```

## 12. Kubernetes（kubectl）核心
```bash
kubectl get pods -n prod                  # 查看Pod
kubectl describe pod <name> -n prod       # 详情
kubectl logs -f <pod> -n prod             # 日志
kubectl exec -it <pod> -- sh -n prod      # 进入容器
kubectl rollout restart deploy/<name> -n prod  # 重启部署
kubectl scale deploy/<name> --replicas=3 -n prod # 扩容
kubectl port-forward svc/<name> 8080:80 -n prod # 本地转发
kubectl apply -f manifest.yaml            # 应用配置
kubectl delete -f manifest.yaml           # 删除资源
```

## 13. 定时与监控（简单版）
```bash
crontab -e                     # 编辑定时任务
crontab -l                     # 查看定时任务
free -h                        # 内存
vmstat 1 5                     # 虚拟内存/上下文切换
sar -n DEV 1 5                 # 网络设备统计（需 sysstat）
```

## 14. 容易踩雷（务必注意）
- `rm -rf` 路径确认三遍，慎用变量拼接；可先用 `echo` 打印再执行。
- `sed -i` 就地修改前先备份；生产环境建议走配置模板+回滚机制。
- `kill -9` 是最后手段，优先尝试普通 `kill` 给程序机会清理资源。
- `journalctl` 带时间窗口（如 `--since`/`--until`）更高效，避免一次性吐出海量日志。
- `ss`/`lsof` 权限不足时用 `sudo`；避免误判端口占用。
- Docker 与宿主机时区/时钟差异会影响日志和定时，统一时区配置。
- Kubernetes 资源改动优先 `kubectl apply` + GitOps/CI 管控，避免直接编辑线上对象。

## 15. 一屏速查关键词
- 文件：`ls` `cd` `pwd` `find` `grep -R` `mkdir` `cp` `mv` `rm -rf`
- 文本：`head` `tail -f` `less` `awk` `sed` `wc` `sort | uniq -c`
- 进程：`ps` `top` `pgrep` `kill` `renice` `systemctl` `journalctl`
- 网络：`ping` `curl -I` `ss -tulpn` `lsof -i :PORT` `nc -vz` `dig`
- 磁盘：`df -h` `du -sh` `lsblk`
- 压缩：`tar -czf` `tar -xzf` `zip` `unzip`
- 权限：`chmod` `chown`
- 包：`apt` `dnf`
- 传输：`ssh` `scp` `rsync` `ssh-keygen` `ssh-copy-id`
- 容器：`docker ps` `logs -f` `exec -it` `run -d -p` `stop` `rm`
- K8s：`kubectl get/describe/logs/exec/rollout/scale/port-forward/apply/delete`

如果你希望我再加：
- 高级 `awk/sed` 模板、正则技巧
- `systemd` 定时器与健康检查（service + timer）
- `docker compose` 与镜像构建 cache/多阶段
- `kubectl` 上下文/多集群管理与 `k9s`
告诉我我就补上。