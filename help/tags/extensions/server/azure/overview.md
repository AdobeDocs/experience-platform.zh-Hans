---
title: Microsoft Azure扩展概述
description: 了解Adobe Experience Platform中用于事件转发的Microsoft Azure扩展。
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# [!DNL Microsoft Azure]扩展概述

在[!DNL Microsoft Azure]中，[[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview)是一种高度可扩展的实时数据输入服务，允许您处理和分析连接设备和应用程序生成的大量数据。 将数据收集到事件中心后，可以使用任何实时Analytics提供程序或批处理/存储适配器转换和存储数据。

[!DNL Microsoft Azure] [事件转发](../../../ui/event-forwarding/overview.md)扩展利用[!DNL Event Hubs]将事件从Adobe Experience Platform Edge Network发送到[!DNL Azure]以供进一步处理。 本指南介绍如何安装扩展并在事件转发规则中部署其功能。

## 先决条件

若要使用此扩展，您必须拥有有效的[!DNL Azure]帐户，且有权访问[!DNL Event Hubs]。 在执行以下步骤之前，您还必须[使用 [!DNL Azure] 门户](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create)创建事件中心。

## 安装扩展

要安装Microsoft [!DNL Azure]扩展，请导航到数据收集UI或Experience Platform UI，然后从左侧导航中选择&#x200B;**[!UICONTROL Event Forwarding]**。 在此处，选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的属性后，在左侧导航中选择&#x200B;**[!UICONTROL Extensions]**，然后选择&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡。 搜索[!UICONTROL Microsoft Azure]卡，然后选择&#x200B;**[!UICONTROL Install]**。

![正在为数据收集UI中的[!UICONTROL Install]扩展选择[!UICONTROL Microsoft Azure]按钮。](../../../images/extensions/server/azure/install.png)

由于扩展没有任何配置属性，因此会立即将其添加到已安装的扩展列表中。 在配置事件转发规则时，您现在可以开始使用[!DNL Event Hub]操作类型。

## 配置事件转发规则 {#rule}

开始创建新的事件转发规则，并根据需要配置其条件。 为规则选择操作时，请为扩展选择&#x200B;**[!UICONTROL Microsoft Azure]**，然后选择操作类型的&#x200B;**[!UICONTROL Send Data to Event Hubs]**。

![为数据收集UI中的规则选择的[!UICONTROL Send Data to Event Hubs]操作类型。](../../../images/extensions/server/azure/select-action-type.png)

右侧面板将更新，以显示应如何发送数据的配置选项。 具体而言，必须将[数据元素](../../../ui/managing-resources/data-elements.md)分配给表示[!DNL Event Hub]配置的各种属性。

![用户界面中显示的[!UICONTROL Send Data to Event Hubs]操作类型的配置选项。](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Event Hub Details]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL Namespace] | [!DNL Event Hubs]设置事件中心[时创建的](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)命名空间的名称。 |
| [!UICONTROL Name] | 事件中心的名称。 |
| [!UICONTROL SAS Authorization Rule Name] | 整个[!DNL Event Hubs]命名空间或要向其发送数据的特定事件中心实例的共享访问授权规则的名称。 有关详细信息，请参阅附录中有关[获取SAS授权值](#sas)的部分。 |
| [!UICONTROL SAS Access Key] | 您整个[!DNL Event Hubs]命名空间或要向其发送数据的特定事件中心实例的共享访问授权规则的主键。 有关详细信息，请参阅附录中有关[获取SAS授权值](#sas)的部分。 |
| [!UICONTROL Partition ID] | [!DNL Event Hubs]允许您[将事件直接发送到特定分区](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka)。 要利用此功能，请提供要接收事件的分区的ID。 |

{style="table-layout:auto"}

**数据**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL Payload] | 此字段包含将转发到[!DNL Event Hubs]的数据。 数据可以是JSON对象、字符串或数据元素。 |

{style="table-layout:auto"}

完成后，选择&#x200B;**[!UICONTROL Keep Changes]**&#x200B;以将该操作添加到规则配置。 如果对规则满意，请选择&#x200B;**[!UICONTROL Save to Library]**。

最后，发布新的事件转发[生成](../../../ui/publishing/builds.md)以启用对库的更改。

## 后续步骤

本指南介绍了如何使用[!DNL Event Hubs]事件转发扩展将数据发送到[!DNL Microsoft Azure]。 有关Experience Platform中事件转发功能的更多信息，请参阅[事件转发概述](../../../ui/event-forwarding/overview.md)。

## 附录：获取SAS授权值 {#sas}

通过[!DNL Event Hubs]共享访问签名(SAS) [授予外部应用程序对](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature)的访问权限。 每个[!DNL Event Hubs]命名空间和事件中心实例都有一个在创建时自动分配的默认SAS授权规则，但您也可以根据需要为每个资源创建其他策略。

使用[扩展配置](#rule)事件转发规则[!DNL Azure]时，必须提供管理要向其发送数据的命名空间或特定事件中心的授权规则的名称和主密钥。 有关如何从[!DNL Azure]门户获取这些值的详细信息，请参阅[!DNL Azure]文档中的以下部分：

* [获取 [!DNL Event Hubs] 命名空间的SAS值](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [获取命名空间中特定事件中心的SAS值](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

获得所需的值后，授权规则名称可以直接作为配置输入中的字符串提供，或者您可以创建字符串类型数据元素来引用它。 但是，主密钥必须首先包含在事件转发密码中，然后才能在规则配置中提供，以保护您的数据安全。

在事件转发UI中，[创建新密钥](../../../ui/event-forwarding/secrets.md)并选择&#x200B;**[!UICONTROL Token]**&#x200B;作为密钥类型。 对于令牌值本身，提供您之前复制的主键。 创建密钥后，创建类型为&#x200B;**[!UICONTROL Secret]**&#x200B;的数据元素并从列表中选择[!DNL Event Hubs]密钥。 设置机密数据元素后，您可以在&#x200B;**[!UICONTROL SAS Access Key]**&#x200B;字段中引用该数据元素。
