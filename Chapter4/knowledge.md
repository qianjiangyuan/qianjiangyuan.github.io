# 4.2: 集群原理

webui2

resffulapi

jobmanager

![图片](https://uploader.shimo.im/f/7VfvPktyVNIFvo2R.png!thumbnail)

<center>钱江源系统组件</center>

钱江源平台系统层面大致由4个模块组成

1. MVC模块
   - 与用户交互的前端UI
   - 提供服务接口的RestfulAPI
2. 保存集群及各种状态信息的SQL server模块
3. 任务调度模块
   - 对用户的计算任务进行调度管理的Job Manager
   - kubernetes暴露出来方便用户自定义扩展kuberneters功能的k8s Master Api
4. 集群本身

下面依次介绍各个子组件所负责的详细功能

### 1. 前端

- 认证授权
- 账户管理
- 获取用户job请求的参数并转交给RestfulAPI处理
- 浏览和管理现有的Job,查看集群状态

### 2. Restful Api

提供的主要Api有以下这些

- 处理前端请求
- 创建Job
- 获得Job列表
- 删除Job
- 获得某个Job的详情
- 获得集群的状态
- 批准Job...

### 3. SQL Server

这里列出一些SQL Server中Job表的字段信息

- jobId
- jobName
- userName
- jobStatus
- jobStatusDetail
- jobType
- jobDescription
- jobTime
- endpoints
- errorMsg
- jobParams
- jobMeta
- jobLog...

### 4. Job manager 

Job Manager通过轮询Sql Server，查看并获取提交的job请求的详细内容，查看用户想生成什么类型的job（pytorch、tensorflow...），调取相应的Pod描述模板文件，填入用户自定义配置，产生kubernetes的Pod描述文件，将他们交给kuernetes的master节点上的Api server组件，由Api server通知kubernetes其他组件生成对应的Job Pod，调度到资源合适的节点上运行。

### 5. K8s Master API

​		K8s提供了一系列的API对象，可以通过它们开发、部署容器化的计算任务。
![图片](https://uploader.shimo.im/f/doFYRoaB0icjwk1h.png!thumbnail)

<center>K8s架构图</center>

[一些k8s常用资源的介绍](https://www.yuque.com/wangsong1299/tqarhh/zoq456)

集群部署的主要逻辑是：
通过src/ClusterBootstrap/deploy.py填充集群配置，使用python的jinja2模板引擎将配置内容渲染进模板(dockerfile)，最后通过模板生成各种docker image，通过这些docker image提供了各种容器化的服务，包括创建、查看、结束计算job，集群状态查看等















  

