---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api;data usage labels overview
solution: Experience Platform
title: 数据使用标签概述
topic: labels
description: 数据使用标签和执行(DULE)是Adobe Experience Platform数据治理的核心机制。 DULE功能允许您将数据使用标签应用到数据集和字段，并根据相关的数据使用策略对每个标签进行分类。 此文档概述Experience Platform中的数据使用标签（也称为DULE标签）。
translation-type: tm+mt
source-git-commit: cddc559dfb65ada888bb367d6265863091a9b2a1
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# 数据使用标签概述

Adobe Experience Platform [!DNL Data Governance] 允许您将数据使用标签应用于数据集和字段，并根据相关的数据使用策略对每个标签进行分类。

此文档概述中的数据使用标签 [!DNL Experience Platform]。 在阅读本指南之前，请参 [阅数据治理概述](../home.md) ，以获得有关数据治理框架的更可靠介绍。

## 了解数据使用标签

数据使用标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 可随时应用标签，在数据管理方式上提供灵活性。 最佳实践是，在数据被引入或 [!DNL Experience Platform]数据可供使用时，立即添加标签 [!DNL Platform]。

在数据集级别应用的数据使用标签将传播到数据集中的所有字段。 标签还可以直接应用于数据集中的各个字段（列标题），而不会传播。

[!DNL Platform] 提供了几个“核心”数据使用标签，它们涵盖适用于数据治理的各种常见限制。 有关这些标签及其所代表的使用策略的详细信息，请参阅核心数据使 [用标签指南](reference.md)。

除了Adobe提供的标签外，您还可以为组织定义自己的自定义标签。 有关详细信息，请 [参阅](#manage-labels) “管理标签”一节。

## 受众段的标签继承

由Adobe Experience Platform分段服务创 [建的所有受众段](../../segmentation/home.md) ，都会继承其相应数据集的使用标签。 这样，在将区段激活到目标 [!DNL Experience Platform] 时，构建在( [!DNL Real-time Customer Data Platform]如)之上的应用程序可以自动执行数据使用策略。

除了继承数据集级别标签外，默认情况下，区段还会继承其关联数据集中的所有字段级别标签。 根据您的基于应 [!DNL Platform]用程序对段的使用情况，您可以潜在地指定使用哪些字段，从而阻止该段从被排除的字段继承标签。

有关自动执行如何在实时CDP中工作的更多信息，请参 [阅有关实时CDP中数据管理的概述](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)。

### Adobe Audience Manager数据导出控制的继承

[!DNL Experience Platform] 能够与Adobe Audience Manager分享细分。 已应用于Audience Manager段的任何数据导出控制均转换为公认的等效标签和营销操 [!DNL Experience Platform][!DNL Data Governance]作。

有关特定数据导出控件如何映射到中的数据使用标签的 [!DNL Platform]参考，请参阅 [Audience Manager文档](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)。

## 管理 [!DNL Experience Platform] {#manage-labels}

您可以使用API或用户界面 [!DNL Experience Platform] 管理数据使用标签。 有关每个子部分的详细信息，请参阅以下子部分。

### 使用UI

UI **[!UICONTROL 中的]** “策略”工 [!DNL Experience Platform] 作区允许您视图和管理组织的核心标签和自定义标签。 工作 **[!DNL Datasets]** 区允许您将标签应用于数据集和字段。 有关详细信息，请参阅标 [签用户指南](user-guide.md)。

### 使用API

策略 `/labels` 服务API中 [的端点允许您以编程方式](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) 管理数据使用标签，包括创建自定义标签。 有关详细信 [息，请参阅](../api/labels.md) “labels endpoint guide”。

数 [据集服务](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) API用于管理数据集和字段的标签。 有关详细信息，请 [参阅管理数据集](./dataset-api.md) 标签指南。

## 后续步骤

本文档介绍了数据使用标签及其在数据管理框架中的作用。 请参阅本指南中链接的文档，进一步了解如何管理中的标签 [!DNL Experience Platform]。