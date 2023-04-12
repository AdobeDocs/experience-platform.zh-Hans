---
title: Microsoft Azure扩展概述
description: 了解用于Adobe Experience Platform中事件转发的Microsoft Azure扩展。
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 3%

---

# [!DNL Microsoft Azure] 扩展概述

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

在 [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) 是一项高度可扩展的实时数据入口服务，它允许您处理和分析连接的设备和应用程序产生的大量数据。 在将数据收集到事件中心后，可以使用任何实时分析提供程序或批量处理/存储适配器来转换和存储数据。

的 [!DNL Microsoft Azure] [事件转发](../../../ui/event-forwarding/overview.md) 扩展利用 [!DNL Event Hubs] 将事件从Adobe Experience Platform边缘网络发送到 [!DNL Azure] 以进一步处理。 本指南介绍如何安装扩展并在事件转发规则中使用其功能。

## 先决条件

要使用此扩展，您必须具有 [!DNL Azure] 有权访问的帐户 [!DNL Event Hubs]. 您还必须 [使用创建事件中心 [!DNL Azure] 门户](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) 执行以下步骤之前，请执行以下操作。

## 安装扩展

安装Microsoft [!DNL Azure] 扩展中，导航到数据收集UI或Experience PlatformUI，然后选择 **[!UICONTROL 事件转发]** 的上界。 从此处，选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的资产后，请选择 **[!UICONTROL 扩展]** 在左侧导航中，选择 **[!UICONTROL 目录]** 选项卡。 搜索 [!UICONTROL Microsoft Azure] 卡片，然后选择 **[!UICONTROL 安装]**.

![的 [!UICONTROL 安装] 按钮 [!UICONTROL Microsoft Azure] 扩展。](../../../images/extensions/server/azure/install.png)

由于扩展没有任何配置属性，因此该扩展会立即添加到已安装扩展的列表。 您现在可以开始使用 [!DNL Event Hub] 操作类型。

## 配置事件转发规则 {#rule}

开始创建新的事件转发规则，并根据需要配置其条件。 为规则选择操作时，选择 **[!UICONTROL Microsoft Azure]** 对于扩展，选择 **[!UICONTROL 将数据发送到事件中心]** ，用于操作类型。

![的 [!UICONTROL 将数据发送到事件中心] 在数据收集UI中为规则选择的操作类型。](../../../images/extensions/server/azure/select-action-type.png)

右侧面板会进行更新，以显示应如何发送数据的配置选项。 具体而言，您必须分配 [数据元素](../../../ui/managing-resources/data-elements.md) 到代表您 [!DNL Event Hub] 配置。

![的配置选项 [!UICONTROL 将数据发送到事件中心] UI中显示的操作类型。](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL 事件中心详细信息]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 命名空间] | 的名称 [!DNL Event Hubs] 您在 [设置事件中心](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL 名称] | 事件中心的名称。 |
| [!UICONTROL SAS授权规则名称] | 整个的共享访问授权规则的名称 [!DNL Event Hubs] 命名空间或要将数据发送到的特定事件中心实例。 请参阅 [获取SAS授权值](#sas) 以了解更多信息。 |
| [!UICONTROL SAS访问密钥] | 整个共享访问授权规则的主密钥 [!DNL Event Hubs] 命名空间或要将数据发送到的特定事件中心实例。 请参阅 [获取SAS授权值](#sas) 以了解更多信息。 |
| [!UICONTROL 分区ID] | [!DNL Event Hubs] 允许您 [将事件直接发送到特定分区](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). 要利用此功能，请提供要接收事件的分区的ID。 |

{style="table-layout:auto"}

**数据**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 负载] | 此字段包含要转发到 [!DNL Event Hubs]. 数据可以是JSON对象、字符串或数据元素。 |

{style="table-layout:auto"}

完成后，选择 **[!UICONTROL 保留更改]** 将操作添加到规则配置。 如果您对规则满意，请选择 **[!UICONTROL 保存到库]**.

最后，发布新的事件转发 [构建](../../../ui/publishing/builds.md) 以启用对库的更改。

## 后续步骤

本指南介绍了如何将数据发送到 [!DNL Event Hubs] 使用 [!DNL Microsoft Azure] 事件转发扩展。 有关Experience Platform中事件转发功能的更多信息，请参阅 [事件转发概述](../../../ui/event-forwarding/overview.md).

## 附录：获取SAS授权值 {#sas}

外部应用程序被授予访问 [!DNL Event Hubs] 至 [共享访问签名(SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). 每个 [!DNL Event Hubs] 命名空间和事件中心实例在创建时自动分配了默认的SAS授权规则，但您也可以根据需要为每个资源创建其他策略。

When [配置事件转发规则](#rule) 使用 [!DNL Azure] 扩展中，您必须为授权规则提供名称和主密钥，以控制要将数据发送到的命名空间或特定事件中心。 有关如何从 [!DNL Azure] 门户，请参阅 [!DNL Azure] 文档：

* [获取的SAS值 [!DNL Event Hubs] 命名空间](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [获取命名空间中特定事件中心的SAS值](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

获得所需值后，可以在配置输入中直接将授权规则名称作为字符串提供，也可以创建一个字符串类型数据元素来引用该名称。 但是，主密钥必须首先包含在事件转发密钥中，然后才能在规则配置中提供，以保护数据安全。

在事件转发UI中， [创建新密码](../../../ui/event-forwarding/secrets.md) 选择 **[!UICONTROL 令牌]** 作为密钥类型。 对于令牌值本身，请提供您之前复制的主密钥。 创建密钥后，创建一个类型为的数据元素 **[!UICONTROL 密码]** ，然后选择 [!DNL Event Hubs] 列表中的秘密。 设置密钥数据元素后，即可在 **[!UICONTROL SAS访问密钥]** 字段。
