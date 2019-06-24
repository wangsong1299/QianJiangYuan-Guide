# 3.6: GPU服务器挂载

#### 总结一下

如果是新的gpu机器，

那么修改config.yaml，增加node

那么执行 sshkey install， 从dev-machine上把一些key拷进去

再执行 updateworker 就可以了 。

注意两个问题：

1.  可能会有host问题，那么就把dev-machine上的hosts拷过去
2. 如果gpu之前的开发machine不是这台，就要把镜像mount过来



#### 挂载

在config.yaml中加上配置

```
machines:
	……
	qjy-ai02:
		role:worker
		type:gpu
```

type是gpu是default选项，可以不填。

注入这个cluster的key

```
./deploy.py --node qjy-ai02 sshkey install
```

再执行updateworker

```
./deploy.py --node qjy-ai02 -y updateworker
```

更新完worker之后，理论上可以在节点列表中找到这台机器。但是没有仍和services。执行label操作。

```
./deploy.py --node qjy-ai02 kubernetes labels
```

#### 挂载目录重定向处理

每个GPU节点只做运算和临时存储（有cache空间），但是实际数据存储都是挂载到另外的存储节点，如果这个GPU在上个集群使用，且两个集群的存储节点不同，则会导致创建job的时候出错，所以需要改gpu节点的mount路径。

进入ai-03节点：

```
cd /dlwsdata/
sudo rm dlwsdata2 dlwsdata3 jobfiles namenodeshare storage work
```

回dev-machine，执行：

```
./deploy.py --node qjy-ai03 mount
```

#### 下线GPU节点：

```
./deploy.py kubectl drain qjy-ai02 --ignore-daemonsets
./deploy.py kubectl delete node qjy-ai02
```

