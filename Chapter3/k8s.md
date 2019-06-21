# 3.3: 搭建kubernetes

#### sudo免密码

因为需要在dev machine上频繁操作几台节点服务器，所以需要开启sudo免密码模式。

登录对应服务器，执行

```
sudo vim /etc/sudoers
```

在末尾加上

```
 %sudo ALL=(ALL) NOPASSWD:ALL
```



如何验证，执行

```
./deploy.py execonall sudo ls -al
```

可以通过日志看到，可以在dev machine上执行几台服务器上sudo操作。



#### 修改config.yaml

config.yaml为核心配置文件，需要修改的地方有：

- cluster_name: 节点的名称，每个集群都该不同
- machines：配置本地的节点信息
- DeployAuthentications：可以修改超管信息等
- Authentications：登录认证的key信息，见[认证章节](./auth.md)
- proxy相关：全局替换yaml文件中原先proxy相关为新的proxy节点。



machines写法：

```
machines:

 qjy-test01:

   role: infrastructure

 qjy-proxy02:

   role: worker

   type: cpu
```



#### build

执行

```
./deploy.py -y build
```

编译源码，会生成需要key文件和deploy目录下的中间文件（这些文件都会在deploy操作中搬运到目标节点上）



#### insert key

首先在节点服务器上实现了sudo免密码操作./

然后在./deploy/sshkey/rootpasswd中加入节点的password，如果没有rootpasswd文件，则手动创建写入。

接着，把dev Machine上生成的key安装到节点上，然后确保可以通信。

执行

```
./deploy.py sshkey install
```



#### backup

key信息做备份。

```
 ./deploy.py backup ~/qjytest
```



#### reslov文件处理

等于dns解析，可以加快一些文件的下载。

其实就是加上了 nameserver：8.8.8.8

执行：

```
/deploy.py copytoall ./deploy/etc/resolvconf/resolv.conf.d/base /etc/resolvconf/resolv.conf.d/base

sudo resolvconf -u
```



#### 节点安装ubuntu环境

在前面的操作中，都在dev-machine上build或者操作，差不多仍都是准备工作。

接下来就开始在节点上进行相应的安装，进行集群的搭建。

先remove掉libappstream3包，[原因](https://askubuntu.com/questions/942895/e-problem-executing-scripts-aptupdatepost-invoke-success)

```
./deploy.py execonall sudo apt-get remove libappstream3
```

给节点安装ubuntu镜像：

```
./deploy.py runscriptonall ./scripts/prepare_ubuntu.sh
```

再做一步：

```
./deploy.py execonall sudo usermod -aG docker core
```

tips：

1. prepare_ubuntu这一步会比较耗时。



#### Setup kubernetes

拉取镜像

```
./deploy.py execonall docker pull dlws/pause-amd64:3.0
./deploy.py execonall docker tag  dlws/pause-amd64:3.0 gcr.io/google_containers/pause-amd64:3.0
```

执行deploy:

```
./deploy.py -y deploy
```

更新k8s的workder：

```
./deploy.py -y updateworker
```

再进行labels操作

```
./deploy.py -y kubernetes labels
```



如上操作执行，k8s已经搭建上。

可以通过k8s的执行进行查看。

```
/deploy.py kubectl get pods -n kube-system
```

