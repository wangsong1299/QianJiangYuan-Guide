# 3.4: 处理restfulapi等应用

k8s是底层的集群管理服务，在k8s上层有resfulapi、jobmanager、webui等服务。

通过在dev machine上build生成docker镜像，推到docker hub上，再在目标节点从docker hub上拉下来，启停服务。

#### 登录docker

在dev machine上需要登录docker，不然docker image不知道推哪儿。

```
docker login
```

#### service处理

collectd

```
./deploy.py docker push collectd
```

webui

```
./deploy.py webui
./deploy.py docker push webui2
```

restfulapi， jobmanager，两者因为都是flask框架，所以就合在一个docker里了。

```
./deploy.py docker push restfulapi
```

配置nginx:

```
./deploy.py nginx fqdn
./deploy.py nginx config
```

k8s启动服务：

```
./deploy.py kubernetes start mysql jobmanager restfulapi webui2 monitor nginx custommetrics
```

操作后：

kube-system里的pods，会多出collectd，grafana，influxdb，mysql，

![image.png](https://cdn.nlark.com/yuque/0/2019/png/328536/1560832440152-68419101-e659-48c1-96a6-59d6b693f677.png)

default namespace下的pods：

jobmanager，restfulapi，nginx, webui2等

tips：

1. 所有的service镜像都在docker hub上，注意resffulapi和webui2是跟cluster name的，其他的都是公用的。所以比如qjytest这个集群，对应webui2的镜像应该是qjytest_webui2.

2. 因为大部分images都是公用的，即之前编译后已经存在，所以不用去重新push。但是如果看到status是ImagePullBackOff的话，就可以是image缺失，就需要重新编译以下。例如：

   ```
   ./deploy.py docker push grafana
   ./deploy.py docker push influxdb
   ```

   

当所有service都起来后，通过对应的域名应该是可以访问到网页了。包括http和https

但是没法通过微软账号认证。见[下一章](./auth.md)