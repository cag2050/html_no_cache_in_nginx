# html_no_cache_in_nginx

### 问题：Nginx 配置不缓存单页面应用的 index.html 文件===并没有生效。
* 现在配置：
1. nginx 配置文件（nginx/default.conf）已经配置了：
```
    location = /index.html {
        add_header Cache-Control "no-cache, no-store";
    }
```
2. 进入docker容器（`docker exec -it <容器名或容器id> bash`）后，修改`/usr/share/nginx/dist/index.html`文件，点击切换前端页面路由，index.html 并没有更新。
* 疑问：修改 index.html 文件后，为什么没有更新？请告知原因。

### 将 Vue 单页面应用项目，运行在docker的nginx容器中，步骤：
1.安装docker mac版
2.下载nginx镜像（1.15.8：是具体的nignx版本；默认从 https://hub.docker.com/ 下载镜像）：
```
docker pull nginx:1.15.8
```
3.运行命令打包项目：`npm run build`
4.编写nginx的配置文件（文件在本项目中位置：`nginx/default.conf`）
5.在项目目录下运行 docker 命令：
```
docker run -p 9081:80 -v $PWD/dist/:/usr/share/nginx/dist/ -v $PWD/nginx/default.conf:/etc/nginx/conf.d/default.conf -d nginx:1.15.8
```
6.宿主机（就是本机）访问项目网址：[http://localhost:9081/](http://localhost:9081/)

### 基于 debian 操作系统的 docker 镜像，安装 vim，步骤：
1. `apt-get update`
2. `apt-get install vim`
* 说明：这个 nginx docker 镜像需要安装下 vim。

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
