# 常用命令

| 停止所有容器 | docker stop $(docker ps -aq)       |
| ------------ | ---------------------------------- |
| 删除所有镜像 | docker rmi -f $(docker images -qa) |
| 删除所有容器 | docker rm $(docker ps -a)          |
| 安装镜像     | docker pull tomcat                 |
| 启动Docker   | systemctl start docker.service     |
|              |                                    |
|              |                                    |
|              |                                    |
|              |                                    |
|              |                                    |

```
yum-config-manager \
    --add-repo \
    http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

