---
keywords: Experience Platform;home;popular topics;namespace;Namespace;Namespaces;namespaces;identity namespace;Identity namespace;identity;Identity;Identity service;identity service
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
description: '身份命名空间是 Identity Service 的组件，充当与身份相关的上下文指示器。例如，它们将值“name@email.com”区分为电子邮件地址或数字CRM ID“443522”。 '
translation-type: tm+mt
source-git-commit: dfb16c1808ac61e6c4f4d97c08ac3d1dcc8499a8
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 4%

---


# 身份命名空间概述

Identity namespaces are a component of [[!DNL Identity Service]](./home.md) that serve as indicators of the context to which an identity relates. 例如，它们将“name<span>@email.com”的值区分为电子邮件地址或“443522”作为数字CRM ID。

## 入门指南

与身份命名空间合作需要了解所涉的Adobe Experience Platform各项服务。 在开始与命名空间合作之前，请查看以下服务的相关文档：

- [[!DNL实时客户用户档案]](../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
- [[!DNL标识服务]](./home.md):通过跨设备和系统桥接身份，更好地视图个别客户及其行为。
- [[!DNLPrivacy Service]](../privacy-service/home.md):身份命名空间用于遵守一般数据保护规定(GDPR)，在该规定中，GDPR请求可以与命名空间相关。

## 了解身份命名空间

完全限定的标识包括ID值和命名空间。 在用户档案片段之间匹配记录数据时(如 [!DNL Real-time Customer Profile] 合并用户档案数据时)，标识值和命名空间必须匹配。

例如，两个用户档案片段可能包含不同的主ID，但它们对“电子邮件”命名空间具有相同的值，因此平台能够看到这些片段实际上是同一个人，并将数据整合到个人的标识图中。

![](images/identity-service-stitching.png)

### 身份类型

数据可以由多种不同的标识类型进行标识。 标识类型在创建标识命名空间时指定，并控制数据是否会保留到标识图以及如何处理该数据的任何特殊说明。

以下身份类型在中可用 [!DNL Platform]:

| 身份类型 | 描述 |
| --- | --- |
| Cookie | 这些身份对于扩展是至关重要的，并且构成了身份图的大部分。 然而，从本质上讲，它们会迅速衰退，并随着时间的推移而失去价值。 删除Cookie是在身份图中特别处理的。 |
| 跨设备 | 这表明应 [!DNL Identity Service] 将此视为强人物标识符，因此应永久保留它。 例如，登录ID、CRM ID、忠诚度ID等。 |
| 设备 | 包括IDFA、GAID和其他IOT ID。 这些可以由家庭中的人分享。 |
| 电子邮件 | 此类型的身份包括个人身份信息(PII)。 这是一个灵敏 [!DNL Identity Service] 地处理该值的指示。 |
| 移动设备 | 此类型的身份包括PII。 这是一个灵敏 [!DNL Identity Service] 地处理该值的指示。 |
| 非人 | 用于存储需要命名空间但未绑定到人群集的标识符。 然后从标识图中过滤这些标识符。 可能的使用案例包括与产品、组织、商店等相关的数据。 （例如，产品SKU。） |
| Phone | 此类型的身份包括PII。 这说明该 [!DNL Identity Service] 值处理灵敏。 |

### 标准命名空间 {#standard}

Adobe Experience Platform为所有组织提供多种身份命名空间。 这些命名空间称为标准，可通过API [!DNL Identity Service] 或通过UI [!DNL Platform] 查看。

要在UI中视图标准命名空间 **[!UICONTROL ，请单击左边栏中的“标]** 识 **[!UICONTROL ”，然后单击“浏览”]** 选项卡。 您的组织可访问的所有身份命名空间都将显示，但“标[!UICONTROL 准]”为“所有者”的命名空间是Adobe提供的标准。

然后，您可以单击列出的命名空间之一以了解视图详细信息。

![](./images/standard-namespace-detail.png)

## 为组织管理命名空间

根据组织数据和使用案例，您可能需要自定义命名空间。

这些命名空间在UI中可见，如“自[!UICONTROL 定义]”为“[!UICONTROL 所有者]”。 可以使用API或通过 [!DNL Identity Service] 用户界面创建自定义命名空间。

要使用UI创建自定义命名空间，请单 **[!UICONTROL 击创建标识命名空间]**，然后完成对话框并单 **[!UICONTROL 击创建]**。

您定义的命名空间对您的组织是私有的，并且需要唯一的“[!UICONTROL Identity]Symbol”（如果您使用的是API，则为“code”）才能成功创建。

![](./images/create-identity-namespace.png)

与标准命名空间类似，您可以单击“浏览”选项卡中的“自定义命名空间 **** ”来视图其详细信息，但使用“自定义命名空间”，您也可以从详细信息区域编辑其“显示名称”和“说明”。

>[!NOTE]
>
>创建命名空间后，无法删除它，并且其“Identity Symbol”（或API中的“代码”）和“Type”不能更改。

## 命名空间身份数据

为身份提供命名空间取决于您提供身份数据的方法。 有关提供数据标识数据的详细信息，请参阅概 [述中有关提供](./home.md#supplying-identity-data-to-identity-service) 标识数据 [!DNL Identity Service] 的部分。
