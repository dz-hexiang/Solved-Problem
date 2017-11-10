#安装docker
#启动 Docker
systemctl start docker
# 使用镜像
docker pull piasy/apprtc-server

git clone https://github.com/Piasy/WebRTC-Docker.git

#运行镜像
docker run --rm \
   -p 8080:8080 -p 8089:8089 -p 3478:3478 -p 3033:3033 \
  --expose=59000-65000 \
  -e PUBLIC_IP=192.168.8.129 \
  -v /home/hexiang/Downloads/WebRTC-Docker/apprtc-server:/apprtc_configs \
  -t -i piasy/apprtc-server
  
  
  
  docker run --rm \
   -p 6080:6080 -p 6089:6089 -p 3478:3478 -p 3033:3033 \
  --expose=59000-65000 \
  -e PUBLIC_IP=192.168.8.129 \
  -v /home/hexiang/Downloads/WebRTC-Docker/apprtc-server:/apprtc_configs \
  -t -i piasy/apprtc-server
  

  docker stop  piasy/apprtc-server
  

#修改constants.py, 中的 ICE_SERVER_BASE_URL, ICE_SERVER_URL_TEMPLATE and WSS_INSTANCES 改成自己的ip(<server public IP> 改成服务器ip)
#websocket连接不上很有可能是配置没改
#chrome浏览器getting user media : Only secure origins are allowed 获取不到视频 是因为google需要https才能获取，改用firefox六拿起


http://192.168.8.129:8080/
  
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
iptables -A INPUT -p tcp --dport 8089 -j ACCEPT 
iptables -A INPUT -p tcp --dport 3478 -j ACCEPT
iptables -A INPUT -p tcp --dport 3033 -j ACCEPT



sudo ufw allow 8080
sudo ufw allow 8089
sudo ufw allow 3478
sudo ufw allow 3033



docker run --rm \
   -p 8080:8080 -p 8089:8089 -p 3478:3478 -p 3033:3033 \
  --expose=59000-65000 \
  -e PUBLIC_IP=192.168.8.129 \
  -v /home/hexiang/Downloads/WebRTC-Docker/apprtc-server:/apprtc_configs \
  -t -i docker.io/piasy/apprtc-server
