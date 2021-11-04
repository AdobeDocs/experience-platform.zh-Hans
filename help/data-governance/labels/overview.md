---
keywords: Experience Platform；主页；热门主题；数据管理；数据使用标签api；策略服务API；数据使用标签概述
solution: Experience Platform
title: 数据使用情况标签概述
topic-legacy: labels
description: Adobe Experience Platform数据管理允许您将数据使用情况标签应用到数据集和字段，并根据相关的数据使用策略对每个数据集和字段进行分类。 本文档概述了Experience Platform中的数据使用标签。
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 数据使用标签概述

Adobe Experience Platform数据管理允许您将数据使用情况标签应用到数据集和字段，并根据相关的数据使用策略对每个数据集和字段进行分类。

本文档概述了 [!DNL Experience Platform]. 在阅读本指南之前，请参阅 [数据管理概述](../home.md) 以更加可靠地介绍数据管理框架。

## 了解数据使用标签

数据使用情况标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 标签可随时应用，从而在您选择如何管理数据方面提供了灵活性。 最佳实践是鼓励在将数据摄取到 [!DNL Experience Platform]，或数据在 [!DNL Platform].

在数据集级别应用的数据使用情况标签将被传播到数据集中的所有字段。 标签也可以直接应用于数据集中的单个字段（列标题），而不会进行传播。

[!DNL Platform] 提供了几个现成的“核心”数据使用标签，其中涵盖了适用于数据管理的各种常见限制。 有关这些标签及其所代表的使用策略的更多信息，请参阅 [核心数据使用标签](reference.md).

除了Adobe提供的标签之外，您还可以为贵组织定义自己的自定义标签。 请参阅 [管理标签](#manage-labels) 以了解更多信息。

## 受众区段的标签继承

由创建的所有受众区段 [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) 继承其相应数据集的使用情况标签。 这允许Experience Platform在将区段激活到目标时自动执行数据使用策略。

除了继承数据集级别标签之外，默认情况下，区段还从其关联的数据集继承所有字段级别标签。 因此，您可以更轻松地识别应从区段中排除的属性，并阻止它们继承排除字段中的标签。

有关自动执行如何在Platform中工作的更多信息，请参阅 [自动策略执行](../enforcement/auto-enforcement.md).

### 从Adobe Audience Manager数据导出控件中继承

[!DNL Experience Platform] 能够与Adobe Audience Manager共享区段。 已应用于Audience Manager区段的任何数据导出控制都会转换为相应的标签和由 [!DNL Experience Platform] 数据管理。

有关特定数据导出控件如何映射到 [!DNL Platform]，请参阅 [Audience Manager文档](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## 在中管理数据使用标签 [!DNL Experience Platform] {#manage-labels}

您可以使用 [!DNL Experience Platform] API或用户界面。 有关每个子部分的详细信息，请参阅下面的子部分。

### 使用UI

的 **[!UICONTROL 策略]** 工作区 [!DNL Experience Platform] UI允许您查看和管理贵组织的核心标签和自定义标签。 的 **[!DNL Datasets]** 工作区允许您将标签应用于数据集和字段。 有关更多信息，请参阅 [标签用户指南](user-guide.md).

### 使用API

的 `/labels` 的端点 [策略服务API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 允许您以编程方式管理数据使用情况标签，包括创建自定义标签。 请参阅 [标签端点指南](../api/labels.md) 以了解更多信息。

的 [数据集服务API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 用于管理数据集和字段的标签。 请参阅 [管理数据集标签](./dataset-api.md) 以了解更多信息。

## 后续步骤

本文档介绍了数据使用标签及其在数据管理框架中的角色。 请参阅本指南中链接的文档，了解有关如何在 [!DNL Experience Platform].
