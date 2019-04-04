# 此repo修复和改进了哪些内容

+ 我在btc-service中新增了nginx用来反向代理accessws，你可以在外部用`ws://<server_ip_address>:18008`来访问

+ 使用3.4的版本来编写docker-compose.yml文件

# 启动它我需要改动哪些地方

+ 将文件`/btc/btc/accessws/config.json`的**auth_url**参数和**sign_url**参数修改为你自己的服务器地址，配置的这两个地址当调用WebSocket的`server.auth`和`server.sign`这两个接口的时候他还请求在这里配置的服务器地址；你需要返回指定格式的json数据

+ 将文件`docker-compose.yml`节点的`service:kafka:environment`其中的**KAFKA_ADVERTISED_HOST_NAME**参数改为你**宿主机**的IP地址；**注意：这个地址不是你docker内的ip地址或hostname；是你外部主机的地址，否则你的应用无法访问kafka**

# 使用Docker快速运行viabtc_exchange_server

[English](README.md)


本项目提供了一种简单快速启动[viabtc_exchange_server](https://github.com/viabtc/viabtc_exchange_server) 的Docker配置

这些配置会自动配置以下内容：

* 启动一个Ubuntu容器
* 准备好编译及运行环境
* 从源码构建viabtc_exchange_server
* 搭建并启动依赖服务(如redis kafka mysql等)
* 启动viabtc_exchange_server服务

# 屏幕截图

![屏幕截图](imgs/screenshots.jpg)

# 准备工作

* 安装docker包括docker-compose: 详见文档 https://docs.docker.com/compose/install/
* git: 非必须,你也可以下载从页面上下载该仓库
* curl: 非必须，仅测试服务效果使用

# 使用方式

打开终端(linux/mac)或者cmd(windows)

```bash
git clone git@github.com:gyk001/viabtc_exchange_server_docker.git
cd viabtc_exchange_server_docker
docker-compose up
```

等待服务启动完成，然后使用curl命令测试效果

```bash
curl  http://127.0.0.1:18080/ -d '{"method": "market.list", "params": [], "id": 1516681174}'
```

全部搞定了,开始探索吧！


提示: 如果你没有安装git，也可以使用下面的步骤运行

* 手工下载文件 https://codeload.github.com/gyk001/viabtc_exchange_server_docker/zip/master
* 解压下载的压缩包 viabtc_exchange_server_docker-master.zip
* 命令行进入解压后的目录
* 执行`docker-compose up`


可前往此处给原作者捐赠: https://github.com/gyk001/viabtc_exchange_server_docker


# 链接

* https://github.com/viabtc/viabtc_exchange_server
* https://github.com/docker-library/mysql
* https://github.com/docker-library/redis
* https://github.com/wurstmeister/kafka-docker
* https://github.com/s7anley/redis-sentinel-docker
* https://github.com/vishnubob/wait-for-it

