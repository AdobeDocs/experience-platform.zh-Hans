---
title: 数据流概述
description: 将客户端 Experience Platform SDK 集成与 Adobe 产品和第三方目标连接起来。
keywords: 配置；数据流；datastreamId；Edge；数据流ID；环境设置；edgeConfigId；身份；ID同步已启用；ID同步容器ID；沙盒；流式入口；事件数据集；目标；客户端代码；属性令牌；目标环境ID；Cookie目标；URL目标；Analytics设置阻止报表包ID；数据收集的数据准备；数据准备；映射器；XDM映射器；Edge上的映射器；
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 4%

---


# 数据流概述

数据流表示实施 Adobe Experience Platform Web 和移动 SDK 时的服务器端配置。而 [configure命令](../edge/fundamentals/configuring-the-sdk.md) SDK中控制必须在客户端上处理的内容(例如 `edgeDomain`)，数据流处理SDK的所有其他配置。 向Adobe Experience Platform Edge Network发送请求时， `edgeConfigId` 用于引用数据流。 这样，您就可以更新服务器端配置，而无需在网站上更改代码。

您可以通过选择来创建和管理数据流 **[!UICONTROL 数据流]** 在Adobe Experience Platform UI或数据收集UI的左侧导航中。

![UI中的“数据流”选项卡](assets/overview/datastreams-tab.png)

有关如何在UI中配置数据流的更多信息，请参阅 [配置指南](./configure.md).

## 处理数据流中的敏感数据 {#sensitive}

>[!IMPORTANT]
>
>本文档的内容不是法律建议，也不会代替法律建议。 请咨询贵公司的法律部门，以获取有关处理敏感数据的建议。

公司数据管理政策和法规要求日益增加了对如何收集、处理和使用敏感客户数据的限制。 这包括受健康保险流通与责任法案(HIPAA)等法规约束的受保护健康数据(PHI)的收集、处理和使用。

数据流提供了三种方法来帮助您安全地处理敏感数据：

* [增强加密](#encryption)
* [数据治理](#governance)
* [审核日志](#audit-logs)

### 增强加密 {#encryption}

所有通过Edge Network传输的数据都通过安全的加密连接进行，使用 [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). 如果数据流将数据引入Experience Platform，则数据在Experience Platform数据湖中静态加密。 查看文档 [Experience Platform中的数据加密](../landing/governance-privacy-security/encryption.md) 了解更多信息。

### 数据治理 {#governance}

数据流利用Experience Platform的内置数据治理功能，防止将敏感数据发送到不符合HIPAA要求的服务。 通过标记数据流架构中包含敏感数据的特定字段，您可以精细地控制哪些数据字段可用于特定目的。

以下视频简要概述如何在UI中为数据流配置和强制执行数据使用限制：

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

在Experience Platform中，您可以应用 [敏感数据使用标签](../data-governance/labels/reference.md#sensitive) 到包含贵组织视为敏感的数据的架构和字段。 例如， `RHD` 标签用于表示受保护的健康信息(PHI)，以及 `S1` 标签表示地理位置数据。

>[!NOTE]
>
>有关如何在 [!UICONTROL 架构] 选项卡，请参阅Experience PlatformUI或数据收集UI中的 [架构标签设置教程](../xdm/tutorials/labels.md).

创建新数据流时，如果所选架构包含敏感数据使用标签，则只能将该数据流配置为将该数据发送到支持HIPAA的目标。 目前，数据流支持的唯一支持HIPAA的目标是Adobe Experience Platform。 对于包含敏感数据使用标签的数据流，将禁用其他目标服务，包括Adobe Target、Adobe Analytics、Adobe Audience Manager、事件转发和边缘目标。

如果架构正在具有非HIPAA就绪服务的现有数据流中使用，则尝试将敏感数据使用标签添加到架构会导致策略违规消息，并阻止该操作。 该消息指定哪个数据流触发了冲突，并建议从数据流中删除任何非HIPAA就绪的服务以解决该问题。

### 审核日志

在Experience Platform中，可以通过审核日志的形式监控数据流活动。 审核日志可告知 **谁** 已执行 **什么** 操作，以及 **时间**，以及其他可帮助您排查与数据流相关问题的上下文数据，以帮助您的企业遵守公司数据管理政策和法规要求。

每当用户创建、更新或删除数据流时，都会创建一个审核日志来记录该操作。 当用户通过创建、更新或删除映射时，也会发生这种情况 [为数据收集准备数据](./data-prep.md). 无论更新的是数据流还是映射，生成的审核日志都分类在 [!UICONTROL 数据流] 资源类型。

请参阅相关文档 [审核日志](../landing/governance-privacy-security/audit-logs/overview.md) 有关如何解释数据流和其他受支持服务的日志的更多信息。

## 后续步骤

本指南提供了有关数据流及其在数据收集和处理敏感数据中的使用的高级概述。 有关如何设置新数据流的步骤，请参见 [数据流配置指南](./configure.md).
