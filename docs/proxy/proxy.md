# 搭建代理

国内访问国外网站的速度很慢

可以使用TinyProxy搭建一个IP代理服务器

TinyProxy安装非常简单

```shell
sudo apt-get update
sudo apt-get install tinyproxy
```

然后修改配置

```shell
sudo vim /etc/tinyproxy/tinyproxy.conf
```

修改下面两个部分
```shell
Port 8888 #改成你的端口
Allow 127.0.0.1 #改成你自己的IP，只有这个IP才能连接，前面打#注释掉则所有人都可以连接
```

TinyProxy打开与关闭

```shell
sudo service tinyproxy start # 运行 
sudo service tinyproxy restart #重启
sudo service tinyproxy stop # 停止
```

代理服务器已经搭建好了

接下来到连接就行了。

但是用国外的代理服务器访问国内的网站速度会变慢

所以我推荐使用Hubstudio

可以创建隔离环境，把代理和日常隔离成两个环境。

链接是http://suo.im/aT2os
