# AI应用专区

# 快速部署云上OpenClaw
## 概述
本文档介绍了如何在UCloud轻量应用云主机上配置使用开源AI助手OpenClaw的完整流程。 

部署过程主要包括：
1. 在UCloud控制台创建使用最新版OpenClaw镜像的轻量应用云主机
2. 使用控制台整合的模型配置功能，结合[UModelVerse](https://docs.ucloud.cn/modelverse/README) 服务，仅需一个 API Key，轻松接入Qwen、DeepSeek、 OpenAI、Gemini 等主流大模型，快速构建您的专属 AGI 应用。
3. 使用控制台整合的通道配置功能快速完成接入飞书、QQ、钉钉、企业微信机器人、企业微信应用。
4. 使用控制台整合的skills配置功能快速安装[ClawHub](https://clawhub.ai/)已发布的skills。

当前轻量应用云主机控制台整合的模型配置、通道配置、Skills配置功能仅适配镜像版本2026.2.17及以上版本，。若您的镜像版本不支持，可以通过重装系统更新到最新版本。

**注意**重装系统会清空原有实例数据且不可恢复，请您备份数据后再谨慎操作。


## 部署OpenClaw轻量应用云主机

## 模型配置
选择相应的轻量应用云主机并进入详情页，点击**应用管理**即可对AIAgent进行配置。
![image](/images/appconf.png)

在**应用管理**页面，找到**模型配置**，当前控制台仅支持接入[UModelVerse](https://docs.ucloud.cn/modelverse/README) 服务提供的各大主流大模型API能力。如您第一次使用请点击**立即创建**，到[ModelVerse 控制台](https://console.ucloud.cn/modelverse/experience/api-keys)创建API Key。
![image](/images/appconf_model.png)
![image](/images/appconf_model1.png)

如您已有UModelVerse 的API Key，则直接选择API Key并选择需要接入OpenClaw的大模型。
![image](/images/appconf_model2.png)

更多关于UModelVerse的介绍请见[UModelVerse产品文档](https://docs.ucloud.cn/modelverse/README)

## 通道配置
在**应用管理**页面，找到**通道配置**，当前控制台仅支持接入飞书、QQ、钉钉、企业微信机器人、企业微信应用。点击**添加**按钮，选择需要添加的通道，填写该通道需要配置的参数并点击完成确认。
![image](/images/appconf_channel.png)
![image](/images/appconf_channel1.png)

等待几十秒后查看状态，确保你添加的通道显示**运行中**。
![image](/images/feishu_status.png)

## Skills配置
在**应用管理**页面，找到**Skills配置**，当前控制台仅支持添加已发布到[ClawHub](https://clawhub.ai/)的skills。点击**添加**按钮，输入Skills的名称并点击确认，即可在控制台完成Skills添加。
![image](/images/appconf_skills1.png)
也可以通过对话的方式，安装新的Skills或查看已安装的Skills列表。
![image](/images/appconf_skills2.png)
2026.2.17版本OpenClaw镜像默认预装的Skills如下：
![image](/images/appconf_skills3.png)

## OpenClaw WebUI
若您想要在OpenClaw官网网站（Web UI）与OpenClaw聊天，您可以在**应用管理**页面**基础信息**中找到**WebUI**信息，点击地址跳转至OpenClaw官网网站。
**注意**：访问OpenClaw官网网站需要访问18789端口，需要在防火墙放行18789端口。
⚠️ 警告：请勿泄露该网站地址！该链接包含您的身份验证凭据，任何持有此链接的人都能直接绕过登录验证，获得您OpenClaw控制台的管理员权限。
