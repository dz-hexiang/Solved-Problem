#docker 安装
sudo apt-get install -y docker.io

#引导时启用 docker
systemctl enable docker
/lib/systemd/systemd-sysv-install enable docker

#启动 Docker
systemctl start docker



#其他命令

#查看所有已下载的images
docker images


#停止docker
systemctl stop docker

