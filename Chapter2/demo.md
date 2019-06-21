# 2.5: 实际使用场景

当你创建完job之后，等于给你分配了一个容器，可以理解为预装好跑深度学习的环境的虚拟主机，然后你可以登录上传和运行自己的代码。

通过该平台，你不仅可以省去自己配置环境的很多烦恼，还可以利用云端的GPU资源进行深度学习。



#### 运行pytorch的官方example中的mnist为例

以mnist为例，这是一个手写数字的识别，github地址：<https://github.com/pytorch/examples/tree/master/mnist>。



通过ssh或者web login登录到pod中，在自己的工作目录下（~目录），新建代码文件夹（如mnist），然后上传对应的代码在文件夹下。

按照github上的readme说明，执行 pip install -r requirements.txt，如下，会发现一些依赖都已经安装好了，这也正是我们平台的遍历之处。

![img](https://cdn.nlark.com/yuque/0/2019/png/328536/1558603251338-75454af1-d8af-49f1-b83b-d7bf492fbbab.png)

然后执行主代码，python main.py， 会看到先下了数据集，然后一共跑了10轮Epoch，每轮都会进行一次训练，然后进行一次测试。

![img](https://cdn.nlark.com/yuque/0/2019/png/328536/1558603319510-a01064dc-2e91-4a35-b22f-abf10cfabe66.png)

![image.png](https://cdn.nlark.com/yuque/0/2019/png/328536/1558603200343-f7a5e6a5-c72f-4a8f-bbc0-b09bd2c740ff.png)



tips:

1. ssh登录建议使用mobaXterm，该客户端可以直接拖拽上传文件，一定程度上带来方便。
2. 数据集可以放在根目录的几个公共文件夹下，作为共享数据集。
3. 如上我们就跑了mnist的例子，进行了训练和测试，可以通过相应的参数进行不同的配置和操作。比如，加上--save-model，会发现训练的模型（mnist_cnn.pt）保存在本地同目录下。下次就可以直接拿这个模型去测试新的测试集了。