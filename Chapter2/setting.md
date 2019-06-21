# 2.4: 配置项说明

#### 1. Base Options

- Interative job： 是否是交互式

- Enable TensorBoard:  启用tensor board

- Launch container as root user: 登录账户拥有root权限

  

#### 2. Advanced Options

##### Mount Directories 

容器和物理机路径映射相关，展开后可以看到列表共有四列信息。

- Path inside container ：容器内path
- Path on host machine (or storage server) ：物理机path
- Enable ：是否开启
- Description：描述

tips 

1. 如我们常用的pod内的公共资源路径/dlwsdata3/public，其实对应的是物理机上的/dlwsdata/dlwsdata3/public目录上，而在gpu物理机上，/dlwsdata/dlwsdata3的路径其实挂载的是qjy-stors1上的某一个目录，存储节点都是单独的。
2. 除非有特殊需求，一般不用改动。

##### HyperParameter Turning 

超参调优相关，待补充。

##### Environmet variables 

添加环境变量。

##### GPU Topology 

是否打开GPU拓扑。

##### Priviledged Docker

是否使用特权的docker。

- use host network in container： 容器内使用物理机ip
- user host IPC in container： 与infiniband network有关
- container DNS policy：dns策略
- CPU request
- Memory request

tips:

1. 容器内use host network，可以实现不同物理机上的pod之间的通信。



#### 3. Job Template Operations

可以切换Template Location的选项。



#### 4. Database operation

可以download和upload json。