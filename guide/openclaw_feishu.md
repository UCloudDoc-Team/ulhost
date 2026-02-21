# AI应用专区

# 云上OpenClaw(Clawdbot)快速接入飞书指南
## 概述
本文主要介绍在UCloud轻量应用云主机中部署完成OpenClaw后如何配置接入飞书机器人。

## 前置准备工作
在正式开始为OpenClaw(Clawdbot)配置接入飞书机器人之前，请您依次检查如下事项是否准备完成：
1. 您已经拥有一个飞书账号。
2. 是否已经购买预装OpenClaw镜像的UCloud轻量应用云主机。

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

### 通道配置（配置飞书机器人App ID和App Secret）
1. 在应用管理的通道配置输入框中，输入前面步骤中查询到的飞书机器人的App ID和App Secret，并点击确定完成添加。
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
### 添加事件
点击**事件配置**页面中的 **添加事件**，在弹出的列表中，搜索并添加 **接收消息**，点击 **确认添加**，按照指引确认开通权限。
![image](/images/feishu_conf2.png)
（推荐）若您期望将飞书机器人添加进聊天群组中使用，可以参考前述步骤继续添加更多群组相关权限，主要包括“消息已读”、“机器人进群”、“机器人被移出群”。否则，请跳过本步骤。
![image](/images/feishu_conf3.png)
完成添加后，可以在当前页面的列表中查看到已添加的事件。
![image](/images/feishu_conf4.png)
### 回调配置
在“事件与回调-回调配置”页面中，订阅方式选择 “使用长连接接收回调”，点击保存，无需填写其他地址，配置自动生效。
![image](/images/feishu_conf5.png)
### 权限配置
在飞书应用管理页，左侧导航栏找到 “权限管理” ，点击进入页面。点击页面中的 “批量导入权限” 按钮，弹出权限导入窗口。
![image](/images/feishu_conf6.png)
![image](/images/feishu_conf7.png)
复制以下代码，替换前面弹窗中原有的JSON内容，点击下一步，确认新增权限，继续申请开通，确认后等待权限导入完成。
```Plain
{
  "scopes": {
    "tenant": [
      
      "im:message",
      "im:message.p2p_msg:readonly",
      "im:message.group_at_msg:readonly",
      "im:message:send_as_bot",
      "im:resource",

      
      "contact:user.base:readonly",
      "im:message.group_msg",
      "im:message:readonly",
      "im:message:update",
      "im:message:recall",
      "im:message.reactions:read",

   
      "docx:document:readonly",
      "drive:drive:readonly",
      "wiki:wiki:readonly",
      "bitable:app:readonly",
      "task:task:read",

      "contact:contact.base:readonly",
      "docx:document",
      "docx:document.block:convert",
      "drive:drive",
      "wiki:wiki",
      "bitable:app",
      "task:task:write"
    ],
    "user": []
  }
}
```
权限导入完成后，可以在权限列表中查看已成功导入的权限。
![image](/images/feishu_conf8.png)
![image](/images/feishu_conf9.png)
## 创建版本并发布
在飞书应用管理页，左侧导航栏找到 “版本管理与发布” ，点击进入页面。点击右上角的创建版本。
![image](/images/feishu_release1.png)
填写应用版本号（此处以1.0.0为例，您可以自行定义版本号）和更新说明，点击保存并确认发布。
![image](/images/feishu_release2.png)
待飞书管理员通过发布审核。审核发布成功后，可以在“版本管理与发布”页面，查看到已经发布的版本号和状态。
![image](/images/feishu_release3.png)
## 与飞书机器人进行交互
完成前面的步骤之后，您可以与飞书机器人进行单独聊天，或者将飞书机器人添加进群聊。
![image](/images/feishu_bot1.png)
![image](/images/feishu_bot2.png)
更多场景欢迎大家探索和解锁。