# 2.2: 看板

登录后，在Home模块下，会展示如下信息：

- 您当前的cluster，目前只有钱江源
- 您的工作目录
- 仪表盘：由grafana可视化工具提供



切换到Cluster Status模块下，会展示整个GPU集群的总览信息：

- Cluster Status ：呈现集群的整体信息，罗列了GPU总数、保留GPU数、已使用GPU数、可用的GPU数，活跃的作业数和总作业数。
- Cluster Usage：可视化展示集群的使用情况。
- Node Status：呈现每个节点的状态，罗列了节点的名字、IP、GPU总数、GPU使用数、GPU空闲数、节点状态、服务和Pods。
- User Status：呈现了用户的使用情况， 罗列了用户和他使用的GPU数目。



tips: 

1. 当你申请了一个job之后，可以在Cluster Status下查看该job对应的pod在哪台物理机上。

