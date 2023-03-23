---
keywords: Experience Platform；主页；热门主题；身份；XDM图形；身份服务；Identity服务
solution: Experience Platform
title: Identity Service概述
description: Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而帮助您更好地了解客户及其行为。
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 7%

---

# [!DNL Identity Service] 概述

提供相关的数字体验需要全面了解您的客户。 当客户数据在不同的系统中分散，导致每个客户似乎都具有多个“身份”时，这会使操作愈发困难。

Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而全面了解客户及其行为。

使用 [!DNL Identity Service]，您可以：

- 确保客户通过每次互动获得一致、个性化且相关的体验。
- 将来自不同来源的多个不同身份拼合在一起，并全面了解您的客户。
- 利用身份图映射不同的身份命名空间，以直观的方式展示客户如何跨不同渠道与您的品牌进行交互。

## 快速入门

在深入研究 [!DNL Identity Service]，以下是关键术语的简要摘要：

| 搜索词 | 定义 |
| --- | --- |
| 标识 | 身份是实体（通常是个人）特有的数据。 身份（如登录ID、ECID或忠诚度ID）也称为“已知身份”。 |
| ECID | Experience CloudID(ECID)是跨Experience Platform和Adobe Experience Cloud应用程序使用的共享身份命名空间。 ECID为客户身份提供了基础，可用作设备的主ID，用作身份图的基节点。 请参阅 [ECID概述](./ecid.md) 以了解更多信息。 |
| 身份命名空间 | 标识命名空间用于区分标识的上下文或类型。例如，标识将“name<span>@email.com”识别为电子邮件地址，将“443522”识别为数字 CRM ID。身份命名空间用于查找个人身份并提供身份值的上下文。 这允许您确定这两个 [!DNL Profile] 包含不同主ID但共享相同值的片段 `email` 身份命名空间实际上是同一个人。 请参阅 [身份命名空间概述](./namespaces.md) 以了解更多信息。 |
| 身份图 | 身份图是不同身份之间关系的映射，使您能够可视化并更好地了解哪些客户身份被拼合在一起，以及如何拼合。 请参阅 [使用身份图查看器](./ui/identity-graph-viewer.md) 以了解更多信息。 |
| 个人身份信息(PII) | PII是可以直接识别客户的信息，如电子邮件地址或电话号码。 PII值通常用于匹配。 客户在不同系统中的多个身份。 |
| 未知或匿名身份 | 未知或匿名身份是指在不识别使用设备的实际人员的情况下隔离设备的指示器。 未知和匿名身份包括访客的IP地址和Cookie ID等信息。 尽管未知和匿名身份可以提供行为数据，但在客户提供其PII之前，这些身份数据会受到限制。 |

## 什么是 [!DNL Identity Service]？

客户每天都与您的业务互动，并与您的品牌建立持续不断的关系。 典型客户可能在贵组织数据基础架构中的任意数量的系统中处于活动状态，例如您的电子商务、忠诚度和服务台系统。 同一客户也可以在任意数量的设备上匿名接触。 [!DNL Identity Service] 允许您整合客户的完整图片，聚合相关数据，否则这些数据可能会分散到不同的系统中。

以消费者与您的品牌关系的日常示例为例：

- Mary在您的电子商务网站上有一个帐户，她过去在该帐户中完成了一些订单。 她通常使用自己的个人笔记本电脑进行购物，每次都会登录。 但是，在她的一次访问中，她使用平板电脑购买凉鞋，但没有下订单，也没有登录。
- 此时，Mary的活动将显示为两个单独的用户档案：
   - 她的电子商务登录
   - 她的平板电脑设备，可能由设备ID识别
- Mary稍后恢复平板电脑会话，并在订阅您的新闻稿时提供其电子邮件地址。 在执行此操作后，流摄取会添加新身份作为其配置文件中的记录数据。 因此， [!DNL Identity Service] 现在，Mary的平板电脑设备活动与她的电子商务帐户历史记录相关联。
- 在下次点击她的平板电脑时，您的目标内容可能会反映Mary的完整资料和历史，而不是只反映未知购物者使用的平板电脑。

![Platform上的身份拼合](./images/identity-service-stitching.png)

基本上， [!DNL Identity Service] 允许您整合客户的完整图片，聚合可能分散在不同系统中的相关数据。 与 [!DNL Identity Service] 实时客户资料利用定义和维护功能，以构建客户及其与您品牌的交互的完整图片。 有关更多信息，请参阅 [实时客户资料概述](../profile/home.md).

### 用例

示例 [!DNL Identity Service] 实施包括：

- 电信公司可能依赖“电话号码”值，其中电话号码是指线下和线上数据集中的同一关注个人。
- 由于匿名访客的高百分比，零售公司可能会在离线数据集中使用“电子邮件地址”，并在在线数据集中使用ECID。
- 银行可能倾向于在离线数据集中使用“帐号”，例如分行交易。 它们可能依赖于在线数据集中的“登录ID”，因为大多数访客在访问期间都将进行身份验证。
- 您的客户还可能具有唯一的专有ID，如GUID或其他通用唯一标识符。

## 身份命名空间 {#identity-namespace}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="标识命名空间"
>abstract="标识命名空间用于区分标识的上下文或类型。例如，标识将“name<span>@email.com”识别为电子邮件地址，将“443522”识别为数字 CRM ID。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="标识值"
>abstract="标识值是代表唯一个人、组织或资产的标识符。该值表示的标识的上下文或类型由相应的标识命名空间定义。当跨配置文件片段匹配记录数据时，命名空间和标识值必须匹配。"
>text="Learn more in documentation"

如果你问某人“你的ID是什么？” 如果没有进一步的背景，他们将很难提供有用的答案。 按照相同的逻辑，表示标识值的字符串值（无论是系统生成的ID还是电子邮件地址）只有在提供给字符串值上下文的限定符时才能完成：身份命名空间。

您的客户可能会通过线上和线下渠道的组合与您的品牌进行交互，这就给如何将这些分散的交互协调到单个客户身份带来了挑战。

通过识别每个渠道中的客户，开始跨多个设备和渠道了解客户。 Platform使用身份命名空间来实现此目的。 标识命名空间是用于为客户标识提供其他上下文的标识符，例如电子邮件或电话。 身份命名空间用于查找或链接个人身份，并提供身份值的上下文。 请参阅 [身份命名空间概述](./namespaces.md) 以了解更多信息。

## 身份图

身份图是不同身份命名空间之间关系的映射，允许您可视化并更好地了解哪些客户身份拼合在一起，以及如何拼合。 请参阅 [使用身份图查看器](./ui/identity-graph-viewer.md) 以了解更多信息。

以下视频旨在支持您对身份和身份图形的了解。

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## 向提供身份数据 [!DNL Identity Service]

本节介绍在使用之前处理提供给Adobe Experience Platform的数据的方式 [!DNL Identity Service] 为每个客户构建身份图。

### 确定身份字段

根据您的企业数据收集策略，您标记为身份的数据字段将决定哪些数据包含在您的身份映射中。 为了最大限度地利用Adobe Experience Platform以及尽可能全面的客户身份，您应当上传在线和离线数据。

- 在线数据是描述在线状态和行为（如用户名和电子邮件地址）的数据。

- 离线数据是指与在线存在无直接关系的数据，例如来自CRM系统的ID。 此类数据可让您的身份更加强健，并支持跨不同系统的数据凝聚力。

### 创建其他身份命名空间

虽然Experience Platform提供了多种标准命名空间，但您可能需要创建其他命名空间以对您的身份正确分类。 有关更多信息，请参阅 [查看和创建贵组织的命名空间](./namespaces.md) 在身份命名空间概述中。

>[!NOTE]
>
>身份命名空间是身份的限定符。 因此，在创建命名空间后，将无法删除该命名空间。

### 将身份数据包含在 [!DNL Experience Data Model] (XDM)

作为标准化框架， [!DNL Platform] 整理客户数据， [!DNL Experience Data Model] (XDM)允许在与之交互的Experience Platform和其他服务之间共享和理解数据 [!DNL Platform]. 有关详细信息，请参阅 [XDM系统概述](../xdm/home.md).

记录架构和时序架构都提供了包含身份数据的方法。 在摄取数据时，如果发现来自不同命名空间的数据片段共享通用身份数据，则该身份图将在它们之间创建新关系。

### 将XDM字段标记为标识

任何类型的字段 `string` 在实施记录类或时间序列XDM类的架构中，可以标记为标识字段。 因此，摄取到该字段的所有数据都将被视为身份数据。

>[!NOTE]
>
>数组和映射类型字段不受支持，无法标记和标记为标识字段。

如果标识字段共享通用PII数据，则还允许关联标识。
例如，通过将电话号码字段标记为身份字段， [!DNL Identity Service] 会自动绘制与使用相同电话号码的其他个人的关系的图表。

>[!NOTE]
>
>在标记字段时，将提供所生成标识的命名空间。

### 为配置数据集 [!DNL Identity Service]

在流式引入过程中， [!DNL Identity Service ]自动从记录数据和时间序列数据中提取身份数据。 但是，在摄取数据之前，必须在 [!DNL Identity Service]. 请参阅  [使用API为实时客户配置文件和Identity服务配置数据集](../profile/tutorials/dataset-configuration.md) 以了解更多信息。

### 将数据摄取到 [!DNL Identity Service]

[!DNL Identity Service] 使用由发送到Experience Platform的符合XDM的数据 [批量摄取](../ingestion/batch-ingestion/overview.md) 或 [流式引入](../ingestion/streaming-ingestion/overview.md).

以下视频旨在支持您对Identity Service的了解。 此视频向您展示了如何为数据字段设置标签以作为标识，引入标识数据，然后验证该数据是否已发送到Adobe Experience Platform Identity Service专用图。

>[!WARNING]
>
>的 [!DNL Platform] 以下视频中显示的UI已过期。 有关最新的UI屏幕截图和功能，请参阅相关文档。

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 数据管理

Adobe Experience Platform构建时考虑了隐私，并包含一个数据管理框架来保护客户PII数据。 默认情况下，“电子邮件”或“电话”命名空间下的身份数据会进行加密，但为确保在保留敏感数据之前对其进行加密，可以在数据被摄取或到达时对数据应用数据使用标签 [!DNL Platform]. 欲知更多信息，请阅读 [数据管理概述](../data-governance/home.md).

## 后续步骤

现在，您已了解 [!DNL Identity Service] 及其在Experience Platform中的角色，您可以开始了解如何使用身份图 [[!DNL Identity Service API]](./api/getting-started.md).
