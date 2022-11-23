---
title: AWS扩展概述
description: 了解用于Adobe Experience Platform中事件转发的AWS扩展。
source-git-commit: ac8fe0c0a5d061b34eee26db10883755234d0c1e
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 4%

---

# [!DNL AWS] 扩展概述

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) 是一个云计算平台，可提供多种服务，如分布式计算、数据库存储、内容交付和客户关系管理(CRM)。

的 [!DNL AWS] [事件转发](../../../ui/event-forwarding/overview.md) 扩展利用 [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) 将事件从Adobe Experience Platform边缘网络发送到 [!DNL AWS] 以进一步处理。 本指南介绍如何安装扩展并在事件转发规则中使用其功能。

## 先决条件

您必须具有 [!DNL AWS] 现有帐户 [!DNL Kinesis] 数据流，以便使用此扩展。 如果您没有预先存在的数据流，请参阅 [!DNL AWS] 文档 [使用 [!DNL AWS] 管理控制台](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## 安装扩展 {#install}

安装 [!DNL AWS] 扩展中，导航到数据收集UI或Experience PlatformUI，然后选择 **[!UICONTROL 事件转发]** 的上界。 从此处，选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的资产后，请选择 **[!UICONTROL 扩展]** 在左侧导航中，选择 **[!UICONTROL 目录]** 选项卡。 搜索 [!UICONTROL AWS] 卡片，然后选择 **[!UICONTROL 安装]**.

![的 [!UICONTROL 安装] 按钮 [!UICONTROL AWS] 扩展。](../../../images/extensions/aws/install.png)

在下一个屏幕中，您必须为 [!DNL AWS] 帐户。 具体而言，您必须提供 [!DNL AWS] 访问密钥ID和密钥访问密钥。 如果您不知道这些值，请参阅 [!DNL AWS] 文档 [如何获取您的访问密钥ID和密钥访问密钥](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![扩展配置视图中添加的访问密钥ID和密钥访问密钥。](../../../images/extensions/aws/credentials.png)

>[!IMPORTANT]
>
>访问策略需要附加到 [!DNL AWS] 用于生成访问凭据的帐户。 必须将此策略配置为授予访问权限，以便将数据发送到 [!DNL Kinesis] 数据流。 请参阅 **示例2** 在 [!DNL AWS] 文档 [示例策略 [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) 以了解应如何定义策略。

完成后，选择 **[!UICONTROL 保存]** 并且已安装扩展。

## 配置事件转发规则 {#rule}

安装扩展后，创建新的事件转发 [规则](../../../ui/managing-resources/rules.md) 并根据需要配置其条件。 为规则配置操作时，选择 **[!UICONTROL AWS]** 扩展，然后选择 **[!UICONTROL 将数据发送到Kinesis数据流]** （对于操作类型）。

![的 [!UICONTROL 将数据发送到Kinesis数据流] 在数据收集UI中为规则选择的操作类型。](../../../images/extensions/aws/select-action-type.png)

右侧面板会进行更新，以显示应如何发送数据的配置选项。 具体而言，您必须分配 [数据元素](../../../ui/managing-resources/data-elements.md) 到代表您 [!DNL Event Hub] 配置。

![的配置选项 [!UICONTROL 将数据发送到Kinesis数据流] UI中显示的操作类型。](../../../images/extensions/aws/data-stream-details.png)

**[!UICONTROL Kinesis数据流详细信息]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 流名称] | 此事件转发规则将向其发送数据记录的流名称。 |
| [!UICONTROL AWS地区] | 的 [!DNL AWS] 区域 [!DNL Kinesis] 会创建数据流。 |
| [!UICONTROL 分区键] | 的 [分区键](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) 扩展在向数据流发送数据时将使用的附加内容。<br><br>[!DNL Kinesis Data Streams] 将属于某个流的数据记录分隔为多个分区。 它使用随每个数据记录一起发送的分区键来确定给定数据记录属于哪个共享。<br><br>分发客户的一个好分区键可能是客户编号，因为每个客户的分区键不同。 分区键不好，可能会出现其邮政编码，因为它们都可能位于附近的同一区域。 通常，您应选择具有不同潜在值最高范围的分区键。 请参阅 [!DNL AWS] 文章 [缩放 [!DNL Kinesis] 数据流](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) 以了解有关管理分区键的最佳实践。 |

{style=&quot;table-layout:auto&quot;}

**[!UICONTROL 数据]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 负载] | 此字段包含要转发到 [!DNL Kinesis] 数据流（JSON格式）。<br><br>在 **[!UICONTROL 原始]** 选项，您可以将JSON对象直接粘贴到提供的文本字段中，也可以选择数据元素图标(![“数据集”图标](../../../images/extensions/aws/data-element-icon.png))从现有数据元素列表中选择以表示有效负载。<br><br>您还可以使用 **[!UICONTROL JSON键值对编辑器]** 选项，通过UI编辑器手动添加每个键值对。 每个值都可以由原始输入来表示，也可以改为选择数据元素。 |

{style=&quot;table-layout:auto&quot;}

完成后，选择 **[!UICONTROL 保留更改]** 将操作添加到规则配置。 如果您对规则满意，请选择 **[!UICONTROL 保存到库]**.

最后，发布新的事件转发 [构建](../../../ui/publishing/builds.md) 以启用对库的更改。

## 后续步骤

本指南介绍了如何将数据发送到 [!DNL Kinesis Data Streams] 使用 [!DNL AWS] 事件转发扩展。 有关Experience Platform中事件转发功能的更多信息，请参阅 [事件转发概述](../../../ui/event-forwarding/overview.md).
