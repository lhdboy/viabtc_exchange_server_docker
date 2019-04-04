# Easy startup viabtc_exchange_server with docker

The contents of this repo repair are only introduced in Chinese version.

## 此repo修复和改进了哪些内容

+ 我在btc-service中新增了nginx用来反向代理accessws，你可以在外部用`ws://<server_ip_address>:18008`来访问

+ 使用3.4的版本来编写docker-compose.yml文件

## 启动它我需要改动哪些地方

+ 将文件`/btc/btc/accessws/config.json`的**auth_url**参数和**sign_url**参数修改为你自己的服务器地址，配置的这两个地址当调用WebSocket的`server.auth`和`server.sign`这两个接口的时候他还请求在这里配置的服务器地址；你需要返回指定格式的json数据

+ 将文件`docker-compose.yml`节点的`service:kafka:environment`其中的**KAFKA_ADVERTISED_HOST_NAME**参数改为你**宿主机**的IP地址；**注意：这个地址不是你docker内的ip地址或hostname；是你外部主机的地址，否则你的应用无法访问kafka**

[中文](README-zh.md)

This is docker config to startup [viabtc_exchange_server](https://github.com/viabtc/viabtc_exchange_server) simply.

This repo do this things automatic:

* Startup a ubuntu docker container
* Prepare requirements environment
* Build viabtc_exchange_server from sourcecode
* Set up requirement service( redis kafka mysql...)
* Startup viabtc_exchange_server service

# Screenshots

![screenshots](imgs/screenshots.jpg)

# Prepare

* docker with compose: https://docs.docker.com/compose/install/
* git: not require, you also can download repo from webpage
* curl: not require, just for test

# Startup

Open a terminal(linux/mac) or cmd(windows)

```bash
git clone git@github.com:gyk001/viabtc_exchange_server_docker.git
cd viabtc_exchange_server_docker
docker-compose up
```

Just wait it startup and then test use curl

```bash
curl  http://127.0.0.1:18080/ -d '{"method": "market.list", "params": [], "id": 1516681174}'
```

All is done, just play it!


Tips: if you don't install git, you can startup it like this

* Download https://codeload.github.com/gyk001/viabtc_exchange_server_docker/zip/master
* Extract viabtc_exchange_server_docker-master.zip
* cd into the target directory
* run `docker-compose up`

you can go here donation the original author: https://github.com/gyk001/viabtc_exchange_server_docker.

# Links

* https://github.com/viabtc/viabtc_exchange_server
* https://github.com/docker-library/mysql
* https://github.com/docker-library/redis
* https://github.com/wurstmeister/kafka-docker
* https://github.com/s7anley/redis-sentinel-docker
* https://github.com/vishnubob/wait-for-it
* https://github.com/yingl/viabtc_exchange_server/blob/master/README.md
