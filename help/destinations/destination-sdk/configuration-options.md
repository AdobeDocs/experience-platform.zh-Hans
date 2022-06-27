---
description: Adobe Experience Platform中的目标服务对多个组件使用配置模板来构建目标功能。 通过这些组件，Experience Platform可以连接到目标合作伙伴、发送自定义消息并在整个数字生态系统中激活用户档案数据。
title: Destination SDK中的配置选项
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 1%

---

# Destination SDK中的配置选项

## 概述 {#overview}

Adobe Experience Platform中的目标服务对多个组件使用配置模板来构建目标功能。 通过这些组件，Experience Platform可以连接到目标合作伙伴、发送自定义消息并在整个数字生态系统中激活用户档案数据。 Adobe Experience Platform中使用的模板包括：

* **目标配置**:包含有关目标的基本信息。 此配置包括您的目标可支持的身份类型，以及Adobe Experience Platform用户界面中目标卡的各种UI属性。
* **服务器和模板规范**:将有关服务器规范的信息与Adobe用于将负载传送到目标的模板联系起来。
   * **服务器规范**:用于存储端点详细信息的模板。
   * **模板规范**:在此模板中，您可以定义如何在XDM架构和平台支持的格式之间转换配置文件属性字段。 有关支持的模板语言、消息格式以及Adobe设置与平台集成所需的信息的深入信息，请阅读 [消息格式](./message-format.md).
* **身份验证配置**:这些设置定义Adobe Experience Platform用户如何连接到您的目标。
* **受众元数据配置**:利用此模板，可配置受众/区段在目标中以编程方式创建、更新或删除的方式。

![Destination SDK模板和配置](./assets/self-service-configuration.png)

## 相关链接 {#related-links}

以下页面详细介绍了Destination SDK中可用的功能和配置选项，以及可以执行的相应API操作。

| 功能描述 | API参考 |
|--- |--- |
| [目标配置](./destination-configuration.md) | [目标API端点操作](./destination-configuration-api.md) |
| [服务器和模板规范](./server-and-template-configuration.md) | [目标服务器API端点操作](./destination-server-api.md) |
| [身份验证配置](./authentication-configuration.md) | [凭据端点API操作](./credentials-configuration-api.md) |
| [受众元数据管理](./audience-metadata-management.md) | [受众元数据端点API操作](./audience-metadata-api.md) |
| [OAuth 2配置](./oauth2-authentication.md) | 使用配置 `customerAuthenticationConfigurations` 参数 [/目标API端点](./destination-configuration-api.md). |
| [消息格式](./message-format.md) | - |
| [目标测试](./test-destination.md) | [目标测试API操作](./destination-testing-api.md) |
| [目标发布](./configure-destination-instructions.md#publish-destination) | [目标发布API操作](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}
