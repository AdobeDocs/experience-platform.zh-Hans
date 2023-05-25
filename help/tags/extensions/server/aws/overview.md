---
title: AWS扩展概述
description: 了解Adobe Experience Platform中用于事件转发的AWS扩展。
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 3%

---

# [!DNL AWS] 扩展概述

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) 是一个云计算平台，提供多种服务，例如分布式计算、数据库存储、内容交付，以及用于客户关系管理(CRM)和企业资源规划(ERP)的软件即服务(SaaS)集成服务。

此 [!DNL AWS] [事件转发](../../../ui/event-forwarding/overview.md) 扩展利用 [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) 将事件从Adobe Experience Platform Edge Network发送到 [!DNL AWS] 以进行进一步处理。 本指南介绍如何安装扩展并将其功能用于事件转发规则。

## 先决条件

您必须拥有 [!DNL AWS] 具有现有帐户的帐户 [!DNL Kinesis] 数据流以便使用此扩展。 如果您没有预先存在的数据流，请参阅 [!DNL AWS] 相关文档 [使用创建新数据流 [!DNL AWS] 管理控制台](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## 安装扩展 {#install}

安装 [!DNL AWS] 扩展上，导航到数据收集UI或Experience PlatformUI并选择 **[!UICONTROL 事件转发]** 从左侧导航栏中。 在此处，选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的属性后，选择 **[!UICONTROL 扩展]** 在左侧导航中，然后选择 **[!UICONTROL 目录]** 选项卡。 搜索 [!UICONTROL AWS] 信息卡，然后选择 **[!UICONTROL 安装]**.

![此 [!UICONTROL 安装] 已为选择按钮 [!UICONTROL AWS] 数据收集UI中的扩展。](../../../images/extensions/server/aws/install.png)

在下一个屏幕上，您必须提供连接凭据 [!DNL AWS] 帐户。 具体而言，您必须提供 [!DNL AWS] 访问密钥ID和访问密钥。 如果您不知道这些值，请参见 [!DNL AWS] 相关文档 [如何获取访问密钥ID和访问密钥](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![在扩展配置视图中添加了访问密钥ID和秘密访问密钥。](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>访问策略需要附加到 [!DNL AWS] 用于生成访问凭据的帐户。 必须将此策略配置为授予将数据发送到 [!DNL Kinesis] 数据流。 请参阅 **示例2** 在 [!DNL AWS] 文档 [的策略示例 [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) 了解应如何定义策略。

完成后，选择 **[!UICONTROL 保存]** 并安装了扩展。

## 配置事件转发规则 {#rule}

安装该扩展后，创建新的事件转发 [规则](../../../ui/managing-resources/rules.md) 并根据需要配置其条件。 配置规则的操作时，选择 **[!UICONTROL AWS]** 扩展，然后选择 **[!UICONTROL 将数据发送到Kinesis数据流]** 操作类型对应的。

![此 [!UICONTROL 将数据发送到Kinesis数据流] 为数据收集UI中的规则选择的操作类型。](../../../images/extensions/server/aws/select-action-type.png)

右侧面板将更新，以显示应如何发送数据的配置选项。 具体而言，您必须指定 [数据元素](../../../ui/managing-resources/data-elements.md) 到各种属性，这些属性表示 [!DNL Event Hub] 配置。

![的配置选项 [!UICONTROL 将数据发送到Kinesis数据流] UI中显示的操作类型。](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis数据流详细信息]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 流名称] | 此事件转发规则将数据记录发送到的流的名称。 |
| [!UICONTROL AWS地区] | 此 [!DNL AWS] 区域 [!DNL Kinesis] 数据流被创建。 |
| [!UICONTROL 分区键] | 此 [分区键](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) 在将数据发送到数据流时，扩展将使用的标识符。<br><br>[!DNL Kinesis Data Streams] 将属于一个流的数据记录划分为多个分片。 它使用随每个数据记录一起发送的分区键来确定给定数据记录属于哪个分片。<br><br>分发客户的良好分区键可能是客户编号，因为每个客户的编号不同。 分区密钥不正确，可能是因为所有分区密钥都可能位于附近的同一区域。 通常，您应该选择具有不同潜在值的最大范围的分区键。 请参阅 [!DNL AWS] 文章： [缩放 [!DNL Kinesis] 数据流](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) 以了解管理分区键的最佳实践。 |

{style="table-layout:auto"}

**[!UICONTROL 数据]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 有效负荷] | 此字段包含将转发到的数据 [!DNL Kinesis] JSON格式的数据流。<br><br>在 **[!UICONTROL 原始]** 选项，您可以将JSON对象直接粘贴到提供的文本字段中，也可以选择数据元素图标(![数据集图标](../../../images/extensions/server/aws/data-element-icon.png))以从现有数据元素列表中进行选择以表示有效负载。<br><br>您还可以使用 **[!UICONTROL JSON键值对编辑器]** 选项，用于通过UI编辑器手动添加每个键值对。 每个值都可以通过原始输入来表示，也可以改为选择数据元素。 |

{style="table-layout:auto"}

完成后，选择 **[!UICONTROL 保留更改]** 以将操作添加到规则配置。 如果对规则满意，请选择 **[!UICONTROL 保存到库]**.

最后，发布新的事件转发 [生成](../../../ui/publishing/builds.md) 以启用对库的更改。

## 后续步骤

本指南介绍了如何将数据发送到 [!DNL Kinesis Data Streams] 使用 [!DNL AWS] 事件转发扩展。 有关Experience Platform中事件转发功能的详细信息，请参阅 [事件转发概述](../../../ui/event-forwarding/overview.md).
