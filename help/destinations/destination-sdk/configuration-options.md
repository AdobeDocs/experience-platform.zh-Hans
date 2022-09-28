---
description: Adobe Experience Platform中的目标服务使用多个组件的配置端点来构建目标功能。 通过这些组件，Experience Platform可以连接到目标合作伙伴、发送自定义消息并在整个数字生态系统中激活用户档案数据。
title: Destination SDK中的配置选项
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---

# Destination SDK中的配置选项

## 概述 {#overview}

Adobe Experience Platform中的目标服务使用多个组件的配置端点来构建目标功能。 通过这些组件，Experience Platform可以连接到目标平台、发送自定义消息、导出自定义文件，以及在整个数字生态系统中激活用户档案数据。 Adobe Experience Platform Destination SDK中使用的配置包括：

* **目标配置**:包含有关目标的基本信息。 此配置包括您的目标可支持的身份类型、所需的导出文件格式（适用于基于文件的目标），以及Adobe Experience Platform用户界面中目标卡的各种UI属性。
* **服务器、文件和模板规范**:将有关服务器规范的信息与Adobe用于将负载传送到目标的模板联系起来。 对于基于文件的目标，此配置还包含目标支持的文件格式和压缩格式。
   * **服务器规范**:配置模板，其中包含有关数据被发送到的存储位置或HTTP端点的信息。”
   * **文件规范**:配置模板，其中包含批处理目标的文件格式和压缩选项。
   * **模板规范**:在此模板中，您可以定义如何在XDM架构和平台支持的格式之间转换配置文件属性字段。 有关支持的模板语言、消息格式以及Adobe设置与平台集成所需的信息的深入信息，请阅读 [消息格式](./message-format.md).
* **身份验证配置**:这些设置定义Adobe Experience Platform用户如何连接到您的目标。
* **受众元数据配置**:此配置端点允许您配置受众/区段在目标中以编程方式创建、更新或删除的方式。 对于批处理目标，允许您在文件成功交付到目标时设置通知。

![显示Destination SDK配置端点以及如何一起使用的图表。](./assets/self-service-configuration.png)

## 相关链接 {#related-links}

以下页面详细介绍了Destination SDK中可用的功能和配置选项，以及可以执行的相应API操作。

| 功能描述（流目标） | 功能描述（批处理目标） | API参考 |
|--- |--- |--- |
| [目标配置选项](./destination-configuration.md) | [基于文件的目标配置选项](/help/destinations/destination-sdk/file-based-destination-configuration.md) | [目标API端点操作](./destination-configuration-api.md) |
| [服务器和模板规范](./server-and-template-configuration.md) | [服务器和文件配置规范](/help/destinations/destination-sdk/server-and-file-configuration.md) | [目标服务器API端点操作](./destination-server-api.md) |
| [身份验证配置](./authentication-configuration.md) | 与流目标相同。 | 您可以通过 `customerAuthenticationConfigurations` 参数 `/destinations` 端点。 有关 [流](/help/destinations/destination-sdk/destination-configuration.md#customer-authentication-configurations) 和 [批次](/help/destinations/destination-sdk/file-based-destination-configuration.md#customer-authentication-configurations) 目标。 |
| [受众元数据管理](./audience-metadata-management.md) | 与流播放相同。 请参阅 [基于文件的示例](/help/destinations/destination-sdk/audience-metadata-management.md#example-file-based) 以了解如何在批处理目标上下文中使用受众元数据。 | [受众元数据端点API操作](./audience-metadata-api.md) |
| [OAuth 2配置](./oauth2-authentication.md) | 与流目标相同 | 使用配置 `customerAuthenticationConfigurations` 参数 [/目标API端点](./destination-configuration-api.md). |
| [消息格式](./message-format.md) | - | - |
| [用于流目标的测试工具](./test-destination.md) | [基于文件的目标测试工具](/help/destinations/destination-sdk/file-based-destination-testing-overview.md) | [目标测试API操作](./destination-testing-api.md) |
| [目标发布](./configure-destination-instructions.md#publish-destination) | 与流目标相同 | [目标发布API操作](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}

## 后续步骤 {#next-steps}

通过阅读本文，您现在可以大致了解Destination SDK提供的功能以及要阅读哪些页面以了解有关特定配置的更多信息。 接下来，您可以阅读指南，其中包含 [配置流](/help/destinations/destination-sdk/configure-destination-instructions.md) 或 [基于文件的目标](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) 使用Destination SDK。
