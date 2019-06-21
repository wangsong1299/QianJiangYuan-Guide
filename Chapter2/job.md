# 2.3: job创建和使用

#### 创建

进入submit new job的页面，进行job的创建。

- job template，可以理解为您要使用的深度学习的框架，可选caffe training example、pytorch-bert、tensorflow training example、tensorflow-IPython-GPU、tutorial-dl共五种，对应着caffe、pytorch、tensorflow等主流的深度学习框架。

- job name， job的名称，可自定义。
- job type，可以分为regular job和distributed job。
- number of GPUs，申请的gpu使用数目。
- docker Image, 和job template是一一对应的，比如选择pytorch-bert，会选择qianjiangyuan/algorithm-bert:1.7的镜像，里面会安装pytorch所需的依赖，使用docker可以省去配置开发环境的麻烦。
- command， 模块选择后会填入默认的start script，可以做一些修改。
- 其他参数设置在配置项说明的做详细阐述。



#### 查看

##### job 列表

创建完job之后，会跳转到view and manage jobs的模块。

可以在running jobs中看到刚创建的job，以及看到相应的ID、名字、状态、占用的GPU数目、使用者、提交时间、开始时间以及操作项。

可以看到job的status会依次经历approved、queued、scheduling、running等状态。

点击job的id可以进入job的详情。

##### job详情

job详情页可以分为以下六个子模块。

- base info：展示了这个job的基本信息
- Job Folder
- Mapped Endpoints：登录job工作环境的三种方式，ssh以及两个web界面
- Job Console Output
- Run Command
- Job analytics and monitoring



#### 管理

目前只有kill的操作



#### 使用

通过Mapped Endpoints中的登录方式，就可以登录到pod容器中，等于分配了一个带GPU、预装了一些环境的虚拟环境，可以进行相应的深度学习，实际使用代码参考[2.5章节](./demo.md)。