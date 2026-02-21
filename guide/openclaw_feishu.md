# AI应用专区

# 云上OpenClaw(Clawdbot)快速接入飞书指南
## 概述
本文主要介绍在UCloud轻量应用云主机中部署完成OpenClaw后如何配置接入飞书机器人。
当前文档仅适配镜像版本2026.2.2-3及以上版本，您可以在UCloud控制台轻量应用云主机详情页进行版本确认。

## 前置准备工作
在正式开始为OpenClaw(Clawdbot)配置接入飞书机器人之前，请您依次检查如下事项是否准备完成：
1. 您已经拥有一个飞书账号。
2. 您已经购买预装OpenClaw且镜像版本2026.2.2-3及以上版本的UCloud轻量应用云主机。

## 接入飞书

### 创建飞书企业自建应用
1. 使用您的飞书账号登录[飞书开放平台](https://open.feishu.cn/app?lang=zh-CN)，登录成功后，点击**创建企业自建应用**。
![image](/images/feishu1.png)

2. 填写应用名称（如 “OpenClaw助手”）、应用描述，选择应用图标（JPEG/PNG/SVG/BMP 格式，2 MB以内，大于240*240 px，无圆角），点击**创建**按钮，进入应用管理页面。
![image](/images/feishu2.png)

### 添加机器人
1. 在前一步所创建应用的管理页面，左侧导航栏中找到并点击**添加应用能力**。
2. 在弹出的列表中选择**机器人**，点击 **添加**。
![image](/images/feishu3.png)
**提示**：添加机器人之后，可以暂不发布，待其他配置完成后一并发布。

### 查询AppID和AppSecret
1. 在左侧导航栏找到 **“凭据与基础信息”** ，点击进入。
2. 在页面中找到 **“App ID”** 和 **“App Secret”** 两个参数，分别点击右侧 **“复制”** 按钮，将其保存到个人记事本或备忘录中（注意数据安全，勿泄露），后续步骤中需要使用。
![image](/images/feishu4.png)

## 为OpenClaw配置模型和通道
### 应用管理
选择相应的轻量应用云主机并进入详情页，点击**应用管理**即可对AIAgent进行配置。
![image](/images/appconf.png)

### 模型配置
为OpenClaw配置模型API Key，[UModelVerse](https://docs.ucloud.cn/modelverse/README) 旨在为客户提供快速搭建 AGI 应用的能力。仅需一个 API Key，即可轻松接入 OpenAI、Gemini 兼容的 API 接口，快速构建您的专属 AGI 应用，[ModelVerse 控制台](https://console.ucloud.cn/modelverse/experience/api-keys)
![image](/images/UModelVerse.png)

### 通道配置（配置飞书机器人App ID和App Secret）
1. 在应用管理的通道配置输入框中，输入前面步骤中查询到的飞书机器人的App ID和App Secret，并点击确定完成添加。
![image](/images/feishu_ID.png)
2. 点击应用并确认操作，等待几十秒完成配置；
3. 等待几十秒后查看状态，确保你的飞书通道显示**运行中**。
![image](/images/feishu_status.png)


## 飞书机器人相关配置
### 事件配置
回到飞书应用管理页，左侧导航栏点击 **事件与回调** ，点击进入页面。在事件配置页签，选择**长连接接收事件**，点击保存。
![image](/images/feishu_conf1.png)
此时如果事件配置保存成功，可直接前往后续的“添加事件”步骤。

   ⚠️**注意**：如果这一步报错提示**“未建立长连接”**，请检查自己的App ID和App Secret是否已正确配置。如果检查前面步骤中的机器人App ID和App Secret均已经正确配置，但点击保存后仍然报错“应用未建立长连接”，可以返回云主机应用管理页面，找到OpenClaw状态显示，点击“重启”按钮，重启网关服务，再返回飞书开放平台，点击保存事件配置，完成建立长连接。
![image](/images/app_restart.png)
### 回调配置
在“事件与回调-回调配置”页面中，订阅方式选择 “使用长连接接收回调”，点击保存，无需填写其他地址，配置自动生效。
![image](/images/feishu_conf5.png)
### 权限配置
在飞书应用管理页，左侧导航栏找到 “权限管理” ，点击进入页面。
可以按需开启权限，也可点击页面中的 “批量导入权限” 按钮，弹出权限导入窗口。
![image](/images/feishu_conf6.png)  
#### 权限说明
一、基础权限

| 权限范围 (Scope)                          | 权限类型 (Permission) | 功能描述 (Description)       |
|-------------------------------------------|------------------------|------------------------------|
| contact:user.base:readonly                 | User info              | 获取基础用户信息             |
| im:message                                 | Messaging              | 收发消息                     |
| im:message.p2p_msg:read only               | DM                     | 读取机器人的私信消息         |
| im:message.group_at_msg:readonly           | Group                  | 接收群内 @ 机器人的消息      |
| im:message:send_as_bot                     | Send                   | 以机器人身份发送消息         |
| im:resource                                | Media                  | 上传/下载图片/文件           |

二、可选全功能权限

| 权限范围 (Scope)                          | 权限类型 (Permission) | 功能描述 (Description)       |
|-------------------------------------------|------------------------|------------------------------|
| im:message.group_msg                       | Group                  | 读取群内所有消息（敏感）     |
| im:message:readonly                        | Read                   | 获取消息历史记录             |
| im:message:update                          | Edit                   | 编辑/更新已发送的消息        |
| im:message:recall                          | Recall                 | 撤回已发送的消息             |
| im:message.reactions:read                  | Reactions              | 查看消息的互动反馈           |

**提示**：确保消息、机器人、事件订阅等相关权限均已开启。后续使用飞书机器人过程中也可以按需调整权限设置。

## 创建版本并发布
在飞书应用管理页，左侧导航栏找到 “版本管理与发布” ，点击进入页面。点击右上角的创建版本。
填写应用版本号和更新说明，点击保存并确认发布。
![image](/images/feishu_release2.png)
待飞书管理员通过发布审核。审核发布成功后，可以在“版本管理与发布”页面，查看到已经发布的版本号和状态。


## 与飞书机器人进行交互
完成前面的步骤之后，您可以与飞书机器人进行单独聊天，或者将飞书机器人添加进群聊。
![image](/images/feishu_bot1.png)
![image](/images/feishu_bot2.png)
更多场景欢迎大家探索和解锁。
