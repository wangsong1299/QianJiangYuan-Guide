# 3.1: 准备

需要准备以下资源，搭建过程中dev-machine，master node 和 proxy node，public ip，使用过程中需要挂载gpu node。

#### 1. dev-machine

开发服务器，本次用zjlab-storage，几乎所有的操作都在这边执行。



#### 2. master node

k8s的主node，进行相应调度。

本次搭建节点为qjy-test01, 下面出现的qjy-test01为master node.



#### 3. proxy node

proxy 节点，起webui等服务。

本次搭建节点为qjy-proxy02, 下面出现的qjy-proxy02为proxy node.



#### 4. gpu-machine

挂载上去的gpu资源。



#### 5.公网ip

用来申请https证书，和微软登录认证相关。



#### 6. 拉取代码

确定开发目录，拉去代码

```
git clone https://github.com/zhejianglab/QianJiangYuan.git
```

项目开源，拉取没有权限问题。

部署脚本为：/src/ClusterBootstrap/deploy.py



由于开发目录较深，每次一直cd比价麻烦，所以设置快捷键。

​    在根目录的.bashrc文件中，添加

```
alias cddev='cd code/server/china/qjy-dev/QianJiangYuan/src/ClusterBootstrap'
```

​    退出再进入。



#### 7.DNS解析相关

确保master和proxy节点的hostname正确.

确保内网的长域名的dns解析：信息中心做

确保proxy外网的dns解析：信息中心做

确保内网的短域名的dns解析：修改hosts



完整链路：

二级域名 DNS解析到 申请的公网ip， 公网ip 映射到某一个内网ip（proxy那一台）



修改hostname:

```
vim /etc/hostname
vim /etc/hosts
reboot
```



修改hosts：

```
vim /etc/hosts
./deploy.py copytoall /etc/hosts /etc/hosts
```

