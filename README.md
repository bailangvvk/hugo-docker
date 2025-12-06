### **1.创建项目目录并挂载到容器** 强制指定 Hugo 将站点生成到挂载的 `/arc`目录 创建一个新的 Hugo 站点(GitHub.io镜像)

```
HUGO_PATH=/data/hugo

mkdir -p $HUGO_PATH/site
cd $HUGO_PATH/site
chmod 777 $HUGO_PATH/site

docker run --rm -it \
-p 1313:1313 \
-v $HUGO_PATH/site:/src \
-w /src \
bailangvvking/hugo \
new site .
```

### 2.新建某篇文章(以hello.md举例)

```
HUGO_PATH=/data/hugo
docker run --rm -it \
-v $HUGO_PATH/site:/src \
-w /src \
bailangvvking/hugo \
new content/posts/hello.md
```

## 3.启动 Hugo 服务器(主机网络模式 监听V4 V6 端口以1313举例)可以添加-d后台运行

```
HUGO_PATH=/data/hugo
docker run -it -d \
--name hugo \
-v $HUGO_PATH/site:/src \
-w /src \
--network=host \
--restart always \
bailangvvking/hugo \
server --bind=0.0.0.0 --bind=:: --port=1313 \
--renderToMemory --templateMetrics --buildDrafts --noBuildLock --watch \
--baseURL=http://ipv6.lovelyy.eu.org:1313/
```

#### (构建站点）写入文件(默认 server运行的是内存版本 没有写入到文件中)

```
HUGO_PATH=/data/hugo

docker run --rm -it -d \
--name hugo \
-v $HUGO_PATH/site:/src \
-w /src \
--network=host \
bailangvvking/hugo \
--bind=0.0.0.0 --bind=:: \
--port=1313 \
--buildDrafts \
--baseURL=http://ipv6.lovelyy.eu.org:1313/
```

#### # 创建首页

```
HUGO_PATH=/data/hugo

docker run --rm -it \
-v $HUGO_PATH/site:/src \
-w /src \
bailangvvking/hugo \
new content/_index.md
```

### # 在主机上查看 Hugo 自动构建的页面 URL 以及可以访问的网址

```
HUGO_PATH=/data/hugo

docker run --rm -it \
-v $HUGO_PATH/site:/src \
-w /src \
bailangvvking/hugo \
list all
```

