## 同步DockerHub上的镜像仓库到阿里云容器镜像仓库

Docker 的一些服务所在域名被封杀，无法直接访问和拉取镜像。国内的镜像源又宣布停止服务，所以需要一个工具将DockerHub上的镜像同步到阿里云容器镜像仓库。

阿里云容器镜像仓库提供了个人实例服务，支持最多创建300个仓库，而且免费。个人使用完全够满足需求。

阿里云容器镜像仓库地址： [https://cr.console.aliyun.com/](https://cr.console.aliyun.com/)

支持用命令行触发workflow运行，[点此查看方法](#使用命令行直接同步镜像)

## copy-fix.yml 运行介绍

这个工具主要是将 DockerHub (也支持其他仓库，修改source即可) 上某个仓库下的某个标签同步到阿里云容器镜像仓库。

1. 使用阿里云开通个人实例服务，并获取 [登录用户名和固定密码](https://cr.console.aliyun.com/cn-hangzhou/instance/credentials)

2. 克隆本仓库，在仓库设置中配置阿里云镜像仓库账号和密码
    
    其中注意 *Name* 必须为 `DESTINATION_USERNAME` 和 `DESTINATION_USERNAME` 。

![配置密码页面](assets/settings-actions-secrets.png)

3. 在 *Actions* 页面上选择 *copy-fix.yml* 点击 *Run workflow* 填写内容即可运行。

![Run Copy workflow](assets/copy.png)

> 填写说明：
>
> 如同步 DockerHub 上的 nginx:1.13 到 阿里云容器镜像仓库 registry.cn-hangzhou.aliyuncs.com/vantoo/nginx:1.13，则填写如下：
>
> ```yaml
> # 镜像源 (Registry)
> source: docker.io
> # 目标源 (Registry)
> destination: registry.cn-hangzhou.aliyuncs.com
> # 仓库及标签 (格式 repo:tag)
> source_repo: nginx:1.13
> # 目标仓库及标签 (格式 repo:tag)
> destination_repo: vantoo/nginx:1.13
> ```
> 必须要填写仓库及标签
