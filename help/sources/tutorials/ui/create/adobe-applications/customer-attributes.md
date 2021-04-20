---
keywords: Experience Platform；主页；热门主题；客户属性
solution: Experience Platform
title: 在UI中创建客户属性源连接
topic: overview
type: Tutorial
description: 了解如何在UI中创建源连接，以收集用户档案数据到Adobe Experience Platform中的客户属性。
translation-type: tm+mt
source-git-commit: 08a3026e969a8739a8b57226c35a6d1d3150006e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 6%

---


# 在UI中创建客户属性源连接

本教程提供了在UI中创建源连接的步骤，用于将客户属性用户档案数据收集到Adobe Experience Platform中。 有关“客户属性”的详细信息，请参阅[“客户属性”概述](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html)。

>[!IMPORTANT]
>
>客户属性源当前不支持禁用、启用和删除数据流功能。

## 创建源连接

在平台UI中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示可创建连接的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索栏找到要处理的特定源。

在[!UICONTROL Adobe applications]类别下，选择&#x200B;**[!UICONTROL Customer Attributes]**，然后选择&#x200B;**[!UICONTROL Add data]**。

>[!NOTE]
>
>如果您已经为“客户属性”用户档案数据建立了源连接，则与源连接的选项将被禁用。

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

[!UICONTROL Add data]屏幕列表了“客户属性”的所有可用数据源。 要创建新连接，请从列表中选择数据源，然后选择&#x200B;**[!UICONTROL Next]**。

>[!NOTE]
>
>每个“客户属性”源连接只能选择一个数据集。

![](../../../../images/tutorials/create/customer-attributes/add-data.png)

将显示[!UICONTROL Dataflow detail]步骤，允许您命名新数据流并提供简要描述。

在此过程中，您还可以启用[!UICONTROL Partial ingestion]和[!UICONTROL Error diagnostics]。 [!UICONTROL Partial ingestion] 提供收录包含错误的数据的功能，最多可设置某个阈值，同时提 [!UICONTROL Error diagnostics] 供单独分批的任何错误数据的详细信息。有关详细信息，请参阅[部分批摄取概述](../../../../../ingestion/batch-ingestion/partial.md)。

![](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

将显示[!UICONTROL Review]步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

* **[!UICONTROL Connection]**:显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL Assign dataset & map fields]**:显示接收源数据的模式集，包括数据集附带的数据集。

![](../../../../images/tutorials/create/customer-attributes/review.png)

## 后续步骤

创建连接后，将自动创建目标架构和数据集，以包含传入数据。初始摄取完成时，下游平台服务（如[!DNL Real-time Customer Profile]和[!DNL Segmentation Service]）可以使用客户属性用户档案数据。 有关更多详细信息，请参阅以下文档:

* [[!DNL Real-time Customer Profile] 概述](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概述](../../../../../segmentation/home.md)
