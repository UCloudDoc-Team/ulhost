# 跨境电商专区

# Socks5配置信息查询
## CentOS/Debian
**当使用系统镜像或自制镜像时，需要自行查看Socks5配置信息并完成代理配置**

登录主机后输入命令，查看Socks5配置信息：  
```Plain
curl http://100.80.80.80/user-data
```
![image](/images/PROXY_IP_centos.png)

**使用官方应用镜像时会为您预设好相应的Redsocks配置**
配置地址：
```Plain
cat /etc/redsocks/redsocks.conf 
```
![image](/images/2.png)


## Windows
**当使用系统镜像或自制镜像时，需要自行查看Socks5配置信息并完成代理配置**
登录主机后打开浏览器访问如下地址，查看Socks5配置信息：
```Plain
http://100.80.80.80/user-data
```
![image](/images/PROXY_IP_windows.png)
**使用官方应用镜像时会为您预设好相应的Redsocks配置**
配置地址：
```Plain
C: /Program Files/v2ray/config.json
```
![image](/images/3.png)
