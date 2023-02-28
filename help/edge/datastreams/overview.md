---
title: 数据流概述
description: 将客户端 Experience Platform SDK 集成与 Adobe 产品和第三方目标连接起来。
keywords: 配置；数据流；数据流ID；边缘；数据流ID；环境设置；边缘配置ID；标识；启用ID同步；ID同步容器ID；沙盒；流入口；事件数据集；目标；客户端代码；资产令牌；目标环境ID;Cookie目标；URL目标；Analytics设置阻止报表包ID；数据收集的数据准备；数据准备；映射器；XDM；边缘上的XDM；映射器
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 2cec87d3f45b1b774925a9b669b53a958e65e57a
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 4%

---

# 数据流概述

数据流表示实施 Adobe Experience Platform Web 和移动 SDK 时的服务器端配置。而 [配置命令](../fundamentals/configuring-the-sdk.md) 中的控件控制必须在客户端上处理的事项(例如 `edgeDomain`)，数据流将处理SDK的所有其他配置。 请求发送至Adobe Experience Platform边缘网络时， `edgeConfigId` 用于引用数据流。 这样，您就无需在网站上进行代码更改即可更新服务器端配置。

您可以通过选择 **[!UICONTROL 数据流]** 在Adobe Experience Platform UI或数据收集UI的左侧导航中。

![UI中的“数据流”选项卡](../assets/datastreams/overview/datastreams-tab.png)

有关如何在UI中配置数据流的更多信息，请参阅 [配置指南](./configure.md).

## 处理数据流中的敏感数据 {#sensitive}

>[!IMPORTANT]
>
>本文档的内容不是法律建议，也不会代替法律建议。 请咨询贵公司的法律部门，以获取有关处理敏感数据的建议。

企业数据管理政策和法规要求对如何收集、处理和使用敏感客户数据提出了越来越多的限制。 这包括受保护健康数据(PHI)的收集、处理和使用，这些数据受诸如健康保险便携性和责任法案(HIPAA)等法规的约束。

数据流提供了三种方法来帮助您安全地处理敏感数据：

* [增强加密](#encryption)
* [数据管理](#governance)
* [审核日志](#audit-logs)

### 增强加密 {#encryption}

通过边缘网络传输的所有数据均使用安全、加密的连接进行 [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). 如果数据流将数据引入Experience Platform，则数据随后会在Experience Platform数据湖中的静态位置进行加密。 请参阅 [Experience Platform中的数据加密](../../landing/governance-privacy-security/encryption.md) 以了解更多信息。

### 数据管理 {#governance}

数据流利用Experience Platform内置的数据管理功能，防止敏感数据被发送到非HIPAA就绪型服务。 通过为数据流架构中包含敏感数据的特定字段设置标签，您可以精确控制哪些数据字段可用于特定目的。

以下视频简要概述了如何在UI中为数据流配置和强制执行数据使用限制：

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

在Experience Platform中，您可以应用 [敏感数据使用标签](../../data-governance/labels/reference.md#sensitive) 到架构和字段，其中包含贵组织认为敏感的数据。 例如， `RHD` 标签用于表示受保护的健康信息(PHI)，并且 `S1` 标签表示地理位置数据。

>[!NOTE]
>
>有关如何在 [!UICONTROL 模式] 选项卡，请参阅 [架构标签教程](../../xdm/tutorials/labels.md).

创建新数据流时，如果选定的架构包含敏感数据使用标签，则数据流只能配置为将该数据发送到HIPAA就绪目标。 目前，数据流支持的唯一HIPAA就绪目标是Adobe Experience Platform。 对于包含敏感数据使用标签的数据流，其他目标服务(包括Adobe Target、Adobe Analytics、Adobe Audience Manager、事件转发和边缘目标)将被禁用。

如果某个架构正在现有数据流中使用，且该数据流中没有HIPAA就绪服务，则尝试向该架构添加敏感数据使用标签将导致策略违规消息，并且阻止该操作。 该消息指定触发违规的数据流，并建议从数据流中删除任何非HIPAA就绪服务以解决此问题。

### 审核日志

在Experience Platform中，可以以审核日志的形式监控数据流活动。 审核日志告知 **who** 执行 **什么** 操作和 **when**，以及其他上下文数据，可帮助您排查与数据流相关的问题，以帮助您的企业遵守公司数据管理策略和法规要求。

每当用户创建、更新或删除数据流时，都会创建审核日志以记录操作。 每当用户创建、更新或删除映射时，都会发生这种情况 [为数据收集准备数据](./data-prep.md). 无论是数据流还是更新的映射，生成的审核日志都会分类到 [!UICONTROL 数据流] 资源类型。

请参阅 [审核日志](../../landing/governance-privacy-security/audit-logs/overview.md) 有关如何从数据流和其他受支持的服务中解释日志的更多信息。

## 后续步骤

本指南概要介绍了数据流及其在数据收集和敏感数据处理中的用途。 有关如何设置新数据流的步骤，请参阅 [datastream配置指南](./configure.md).
