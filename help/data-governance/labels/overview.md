---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据使用标签概述
topic: labels
translation-type: tm+mt
source-git-commit: f4b3148db3b4a17d071c1c8ad2aff8dd64ddd0b7
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---


# 数据使用标签概述

Adobe Experience Platform使用标签和执行(DULE)是数据管理的核心机制。 DULE功能允许您将数据使用标签应用到数据集和字段，并根据相关的数据使用策略对每个标签进行分类。

此文档概述中的数据使用标签（也称为DULE标签） [!DNL Experience Platform]。 在阅读本指南之前，请参 [阅数据管理概述](../home.md) ，以获得DULE框架的更强健的介绍。

## 了解数据使用标签

数据使用标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 可随时应用标签，在数据管理方式上提供灵活性。 最佳实践是，在数据被引入或 [!DNL Experience Platform]数据可供使用时，立即添加标签 [!DNL Platform]。

在数据集级别应用的数据使用标签将传播到数据集中的所有字段。 标签还可以直接应用于数据集中的各个字段（列标题），而不会传播。

[!DNL Platform] 提供了几个“核心”数据使用标签，它们涵盖适用于数据治理的各种常见限制。 有关这些标签及其所代表的使用策略的详细信息，请参阅核心数据使 [用标签指南](reference.md)。

除了Adobe提供的标签外，您还可以定义自己的自定义标签。 有关如何在UI中执行此操作的步骤，请参阅数 [据使用标签用户指南](./user-guide.md)。 有关如何使用API调用执行此操作的步骤，请参阅数 [据使用标签API指南](./api.md)。

## 受众段的标签继承

由受众分段服务创 [建的所有Adobe Experience Platform段](../../segmentation/home.md) ，都会继承其相应数据集的使用标签。 这样，在将区段激活到目标 [!DNL Experience Platform] 时，构建在( [!DNL Real-time Customer Data Platform]如)之上的应用程序可以自动执行数据使用策略。

除了继承数据集级别标签外，默认情况下，区段还会继承其关联数据集中的所有字段级别标签。 根据您的基于应 [!DNL Platform]用程序对段的使用情况，您可以潜在地指定使用哪些字段，从而阻止该段从被排除的字段继承标签。

有关自动执行如何在实时CDP中工作的更多信息，请参 [阅Adobe实时CDP数据管理概述](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)。

### 从Adobe Audience Manager数据导出控件继承

Experience Platform能够与Adobe Audience Manager共享细分。 已应用于Audience Manager细分的任何数据导出控制均转换为Experience Platform数据管理所确认的对等标签和营销操作。

有关特定数据导出控件如何映射到平台中数据使用标签的参考，请参阅 [Audience Manager文档](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)。


## 后续步骤

既然您已经引入了数据使用标签，您可以继续阅读 [用户指南](user-guide.md) ，学习如何在UI中管理 [!DNL Experience Platform] 标签。 有关如何使用API管理标签的步骤，请参阅使 [用标签API指南](./api.md)。