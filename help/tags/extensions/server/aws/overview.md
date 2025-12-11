---
title: AWS扩展概述
description: 了解Adobe Experience Platform中用于事件转发的AWS扩展。
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# [!DNL AWS]扩展概述

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/)是一个云计算平台，它提供了多种服务，如分布式计算、数据库存储、内容交付，以及用于客户关系管理(CRM)和企业资源规划(ERP)的软件即服务(SaaS)集成服务。

[!DNL AWS] [事件转发](../../../ui/event-forwarding/overview.md)扩展利用[[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)将事件从Adobe Experience Platform Edge Network发送到[!DNL AWS]以供进一步处理。 本指南介绍如何安装扩展并在事件转发规则中部署其功能。

## 先决条件

您必须具有包含现有[!DNL AWS]数据流的[!DNL Kinesis]帐户才能使用此扩展。 如果您没有预先存在的数据流，请参阅有关[!DNL AWS]使用[管理控制台 [!DNL AWS] 创建新数据流的](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html)文档。

## 安装扩展 {#install}

要安装[!DNL AWS]扩展，请导航到数据收集UI或Experience Platform UI，然后从左侧导航中选择&#x200B;**[!UICONTROL Event Forwarding]**。 在此处，选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的属性后，在左侧导航中选择&#x200B;**[!UICONTROL Extensions]**，然后选择&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡。 搜索[!UICONTROL AWS]卡，然后选择&#x200B;**[!UICONTROL Install]**。

![正在为数据收集UI中的[!UICONTROL Install]扩展选择[!UICONTROL AWS]按钮。](../../../images/extensions/server/aws/install.png)

在下一个屏幕上，必须提供[!DNL AWS]帐户的连接凭据。 具体而言，您必须提供您的[!DNL AWS]访问密钥ID和访问密钥。 如果您不知道这些值，请参阅[!DNL AWS]上的[文档，了解如何获取访问密钥ID和访问密钥](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html)。

![访问密钥ID和访问密钥已添加到扩展配置视图中。](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>访问策略需要附加到用于生成访问凭据的[!DNL AWS]帐户。 必须将此策略配置为授予将数据发送到[!DNL Kinesis]数据流的访问权限。 请参阅&#x200B;**策略示例（适用于**[!DNL AWS]）中的[示例2 [!DNL Kinesis Data Streams]（在](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples)文档中），了解应如何定义该策略。

完成后，选择&#x200B;**[!UICONTROL Save]**&#x200B;并安装扩展。

## 配置事件转发规则 {#rule}

安装扩展后，创建新的事件转发[规则](../../../ui/managing-resources/rules.md)并根据需要配置其条件。 配置规则的操作时，请选择&#x200B;**[!UICONTROL AWS]**&#x200B;扩展，然后选择操作类型的&#x200B;**[!UICONTROL Send Data to Kinesis Data Stream]**。

![为数据收集UI中的规则选择的[!UICONTROL Send Data to Kinesis Data Stream]操作类型。](../../../images/extensions/server/aws/select-action-type.png)

右侧面板将更新，以显示应如何发送数据的配置选项。 具体而言，必须将[数据元素](../../../ui/managing-resources/data-elements.md)分配给表示[!DNL Event Hub]配置的各种属性。

![用户界面中显示的[!UICONTROL Send Data to Kinesis Data Stream]操作类型的配置选项。](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis Data Stream Details]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL Stream Name] | 此事件转发规则将数据记录发送到的流的名称。 |
| [!UICONTROL AWS Region] | 创建[!DNL AWS]数据流的[!DNL Kinesis]区域。 |
| [!UICONTROL Partition Key] | 扩展在将数据发送到数据流时将使用的[分区键](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key)。<br><br>[!DNL Kinesis Data Streams]将属于某个流的数据记录分离为多个分片。 它使用随每个数据记录一起发送的分区键来确定给定数据记录属于哪个分片。<br><br>分发客户的正确分区密钥可能是客户编号，因为每个客户的编号不同。 分区键值不佳可能导致他们的邮政编码，因为他们可能都住在附近的同一区域。 通常，您应该选择具有不同潜在值的最大范围的分区键。 请参阅有关[!DNL AWS]缩放[数据流 [!DNL Kinesis] 的](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/)文章以了解管理分区键的最佳实践。 |

{style="table-layout:auto"}

**[!UICONTROL Data]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL Payload] | 此字段包含将以JSON格式转发到[!DNL Kinesis]数据流的数据。<br><br>在&#x200B;**[!UICONTROL Raw]**&#x200B;选项下，您可以将JSON对象直接粘贴到提供的文本字段中，也可以选择数据元素图标（![数据集图标](/help/images/icons/database.png)）以从现有数据元素列表中进行选择以表示有效负载。<br><br>您还可以使用&#x200B;**[!UICONTROL JSON Key-Value Pairs Editor]**&#x200B;选项通过UI编辑器手动添加每个键值对。 每个值都可以用原始输入表示，也可以改为选择数据元素。 |

{style="table-layout:auto"}

完成后，选择&#x200B;**[!UICONTROL Keep Changes]**&#x200B;以将该操作添加到规则配置。 如果对规则满意，请选择&#x200B;**[!UICONTROL Save to Library]**。

最后，发布新的事件转发[生成](../../../ui/publishing/builds.md)以启用对库的更改。

## 后续步骤

本指南介绍了如何使用[!DNL Kinesis Data Streams]事件转发扩展将数据发送到[!DNL AWS]。 有关Experience Platform中事件转发功能的更多信息，请参阅[事件转发概述](../../../ui/event-forwarding/overview.md)。
