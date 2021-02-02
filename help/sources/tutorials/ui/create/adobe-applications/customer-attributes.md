---
keywords: Experience Platform；主页；热门主题；客户属性
solution: Experience Platform
title: 在UI中创建客户属性源连接器
topic: overview
type: Tutorial
description: 本教程提供了在UI中创建源连接器的步骤，用于收集用户档案到Adobe Experience Platform的客户属性数据。
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 5%

---


# 在UI中创建客户属性源连接器

本教程提供了在UI中创建源连接器的步骤，用于收集用户档案到Adobe Experience Platform的客户属性数据。 有关客户属性的详细信息，请参阅[概述文档](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html)。

## 创建源连接

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问源工作区。 **[!UICONTROL 目录]**&#x200B;屏幕显示可用源，用于创建入站连接，每个源显示与它们关联的现有连接数。 选择&#x200B;**[!UICONTROL 客户属性]**&#x200B;的选项，然后选择&#x200B;**[!UICONTROL 添加数据]**。 如果连接成功，您将被重定向。

>[!NOTE]
>
>如果已经为客户属性用户档案数据建立了源连接器，则将禁用与源连接的选项。

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

**源活动**&#x200B;屏幕列表客户属性用户档案数据的所有先前建立的连接，您可以单击&#x200B;**选择数据**&#x200B;创建新连接。

>[!NOTE]
>
>可以建立与源的多个入站连接以引入不同的数据。

![](../../../../images/tutorials/create/customer-attributes/source_activity.png)

从可用客户属性用户档案数据集的列表中，选择要引入[!DNL Platform]的，然后单击&#x200B;**下一步**。

>[!NOTE]
>
>每个客户属性源连接只能选择一个数据集。

![](../../../../images/tutorials/create/customer-attributes/select_data.png)

出现&#x200B;**检查**&#x200B;步骤，允许您在创建新入站连接之前检查新入站连接。 连接的详细信息按类别分组，包括：

* **源详细信息**:显示源连接的类型和所选源数据。
* **目标详细信息**:创建其他源连接器时，此容器显示源数据正被引入的数据集，包括数据集所附加的模式。客户属性用户档案数据会自动映射并引入实时客户用户档案。

![](../../../../images/tutorials/create/customer-attributes/review.png)

## 后续步骤

创建连接后，将自动创建目标架构和数据集，以包含传入数据。初始摄取完成时，下游[!DNL Platform]服务（如[!DNL Real-time Customer Profile]和[!DNL Segmentation Service]）可以使用客户属性用户档案数据。 有关更多详细信息，请参阅以下文档:

* [[!DNL Real-time Customer Profile] 概述](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概述](../../../../../segmentation/home.md)
