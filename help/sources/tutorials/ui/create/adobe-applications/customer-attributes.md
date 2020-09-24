---
keywords: Experience Platform;home;popular topics;customer attributes
solution: Experience Platform
title: 在UI中创建客户属性源连接器
topic: overview
type: Tutorial
description: 本教程提供了在UI中创建源连接器的步骤，用于收集用户档案到Adobe Experience Platform的客户属性数据。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 8%

---


# 在UI中创建客户属性源连接器

本教程提供了在UI中创建源连接器的步骤，用于收集用户档案到Adobe Experience Platform的客户属性数据。 有关客户属性的更多信息，请参阅 [概述文档](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/customer-attributes/attributes.html)。

## 创建源连接

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择“源”以访问源工作区。 “目 **[!UICONTROL 录]** ”屏幕显示用于创建入站连接的可用源，每个源显示与它们关联的现有连接数。 选择“客户属 **[!UICONTROL 性”选项]** ，然后选择 **[!UICONTROL 添加数据]**。 如果连接成功，您将被重定向。

>[!NOTE]
>
>如果已经为客户属性用户档案数据建立了源连接器，则将禁用与源连接的选项。

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

“源 *活动* ”屏幕列表客户属性用户档案数据的所有以前建立的连接，您可以通过单击“选择数据”来创建 **新连接**。

>[!NOTE]
>
>可以建立与源的多个入站连接以引入不同的数据。

![](../../../../images/tutorials/create/customer-attributes/source_activity.png)

从可用客户属性用户档案数据集的列表中，选择要引入的，然 [!DNL Platform] 后单击下 **一步**。

>[!NOTE]
>
>每个客户属性源连接只能选择一个数据集。

![](../../../../images/tutorials/create/customer-attributes/select_data.png)

此时 *会显示* “审阅”步骤，允许您在创建新入站连接之前查看该连接。 连接的详细信息按类别分组，包括：

* *源详细信息*:显示源连接的类型和所选源数据。
* *目标详细信息*:创建其他源连接器时，此容器显示源数据正被引入的数据集，包括数据集所附加的模式。 客户属性用户档案数据会自动映射并引入实时客户用户档案。

![](../../../../images/tutorials/create/customer-attributes/review.png)

## 后续步骤

创建连接后，将自动创建目标架构和数据集，以包含传入数据。当初始摄取完成时，下游服务（如和）可以使用客户属 [!DNL Platform] 性用户档案 [!DNL Real-time Customer Profile] 数据 [!DNL Segmentation Service]。 有关更多详细信息，请参阅以下文档:

* [[!DNL Real-time Customer Profile] 概述](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概述](../../../../../segmentation/home.md)
