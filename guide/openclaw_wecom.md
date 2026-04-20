# AI应用专区

# 云上OpenClaw(Clawdbot)快速接入企业微信机器人指南
## 概述
本文主要介绍在UCloud轻量应用云主机中部署完成OpenClaw后如何配置接入企业微信智能机器人。

当前文档仅适配OpenClaw最新版应用镜像，您可以在UCloud控制台轻量应用云主机详情页进行版本确认。
![image](/images/appconf_os.png)


## 前置准备工作
在正式开始为OpenClaw(Clawdbot)配置接入企业微信机器人之前，请您依次检查如下事项是否准备完成：
1. 您已经在本地电脑或者移动终端中安装了最新版企业微信软件。
2. 您已经购买预装OpenClaw最新应用镜像的轻量应用云主机。

## 扫码接入企业微信智能机器人
在**应用管理**页面，找到**通道列表**，点击**添加**按钮，选择需要添加的通道类型，可扫码添加也可手动输入参数添加。
![image](/images/wecome_qrcode.png)


## 手动接入企业微信智能机器人

### 一、创建企业微信智能机器人
1. 打开企业微信客户端，左侧工具栏找到**工作台**，点击-智能机器人-创建机器人，选择API模式创建。
![image](/images/wecomconf1.png)
![image](/images/wecomconf2.png)
选择以「长连接」方式创建，并获取Bot ID 和 Secret，获取后进入轻量应用云主机OpenClaw应用管理页面。
![image](/images/wecomconf3.png)

### 二、为OpenClaw配置模型并接入企业微信智能机器人
选择相应的轻量应用云主机并进入详情页，点击**应用管理**即可对AIAgent进行配置。
![image](/images/appconf.png)

#### 模型配置
为OpenClaw配置模型API Key，[UModelVerse](https://docs.ucloud.cn/modelverse/README) 旨在为客户提供快速搭建 AGI 应用的能力。仅需一个 API Key，即可轻松接入 OpenAI、Gemini 兼容的 API 接口，快速构建您的专属AGI应用。

#### 通道配置（配置企业微信智能机器人BotID 和 Secret）
1. 在应用管理的**通道配置**区域，点击**添加**按钮，选择**企业微信智能机器人**通道。
2. 在弹出的配置框中，输入此前创建企业微信机器人时随机生成的 BotID 和 Secret，点击**确认**完成添加。
![image](/images/wecomconf4.png)
3. 等待几十秒后查看状态，确保你添加的企业微信通道显示**运行中**。

### 完成企业微信机器人配置
1. 此时您需要再回到企业微信机器人创建页面，保存并创建机器人。
2. 添加完成后，即可在企业微信聊天窗中与智能机器人直接进行聊天。如果企业微信智能机器人能够以AI的方式对话，则说明您已经成功完成OpenClaw应用接入企业微信机器人。

