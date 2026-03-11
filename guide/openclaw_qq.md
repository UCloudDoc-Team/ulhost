# AI应用专区

# 云上OpenClaw(Clawdbot)快速接入QQ指南
## 概述
本文主要介绍在UCloud轻量应用云主机中部署完成OpenClaw后如何配置接入QQ 机器人。

当前文档仅适配预装OpenClaw-2026.2.17及以上版本的应用镜像，您可以在UCloud控制台轻量应用云主机详情页进行版本确认。
![image](/images/appconf_os.png)

## 前置准备工作
在正式开始为OpenClaw(Clawdbot)配置接入QQ之前，请您依次检查如下事项是否准备完成：
1. 您已经拥有一个完成实名认证的腾讯 QQ 账号。
2. 您已经购买预装OpenClaw且镜像版本2026.2.17及以上版本的UCloud轻量应用云主机。

## 接入QQ

### 创建 QQBot 机器人 
1. 前往[QQ 开放平台](https://q.qq.com/qqbot/openclaw/login.html)，需使用QQ扫码登陆并完成注册。
![image](/images/tencentqq1.png)
2. 完成注册后，进入QQ机器人配置页，创建一个QQBot机器人，获取AppID 和 AppSecret。
![image](/images/tencentqq2.png)
回到QQ软件，可以看到新建的QQ机器人已经被添加至您的消息列表中，并将会发送第一条消息。
![image](/images/tencentqq3.png)
接下来就是位QQbot机器人做OpenClaw相关的模型配置和通道配置

## 为OpenClaw配置模型和通道
### 应用管理
选择相应的轻量应用云主机并进入详情页，点击**应用管理**即可对AIAgent进行配置。
![image](/images/appconf.png)

### 模型配置
为OpenClaw配置模型API Key，[UModelVerse](https://docs.ucloud.cn/modelverse/README) 旨在为客户提供快速搭建 AGI 应用的能力。仅需一个 API Key，即可轻松接入 OpenAI、Gemini 兼容的 API 接口，快速构建您的专属 AGI 应用，[ModelVerse 控制台](https://console.ucloud.cn/modelverse/experience/api-keys)

### 通道配置（配置 QQ 机器人 AppID 和 AppSecret）
1. 在应用管理的通道配置输入框中，输入此前在 QQ 开放平台获取的QQBot机器人 AppID和AppSecret；
2. 点击应用并确认操作，等待几十秒完成配置；
3. 等待几十秒后查看状态，确保你的QQ通道显示**运行中**。


## 与 QQ 机器人进行交互
模型配置和通道配置完成后，即可在 QQ 端与接入 OpenClaw 的 QQBot 机器人进行互动。
![image](/images/tencentqq4.png)

