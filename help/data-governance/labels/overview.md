---
keywords: Experience Platform；主页；热门主题；数据管理；数据使用标签api；策略服务api；数据使用标签概述
solution: Experience Platform
title: 数据使用标签概述
topic-legacy: labels
description: Adobe Experience Platform Data Governance允许您将数据使用标签应用到数据集和字段，并根据相关的数据使用策略对每个标签进行分类。 本文档概述Experience Platform中的数据使用标签。
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# 数据使用标签概述

Adobe Experience Platform [!DNL Data Governance]允许您将数据使用标签应用到数据集和字段，并根据相关的数据使用策略对每个标签进行分类。

本文档概述[!DNL Experience Platform]中的数据使用标签。 在阅读本指南之前，请参阅[数据治理概述](../home.md)，以了解有关数据治理框架的更可靠介绍。

## 了解数据使用标签

数据使用标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 可随时应用标签，在您选择如何管理数据方面提供灵活性。 最佳做法鼓励在将数据引入[!DNL Experience Platform]或数据可用于[!DNL Platform]时立即标记数据。

在数据集级别应用的数据使用标签将传播到数据集中的所有字段。 标签还可以直接应用于数据集中的各个字段（列标题），而不会进行传播。

[!DNL Platform] 提供了几个“核心”数据使用标签，它们涵盖适用于数据治理的各种常见限制。有关这些标签及其所代表的使用策略的详细信息，请参阅[核心数据使用标签](reference.md)指南。

除了Adobe提供的标签外，您还可以为组织定义自己的自定义标签。 有关详细信息，请参阅[管理标签](#manage-labels)一节。

## 受众段的标签继承

由[Adobe Experience Platform Segmentation Service](../../segmentation/home.md)创建的所有受众区段将继承其相应数据集的使用标签。 这允许Experience Platform在将区段激活到目标时提供自动数据使用策略强制。

默认情况下，除了继承数据集级别标签外，区段还会继承其关联数据集中的所有字段级别标签。 因此，您可以更轻松地识别应从区段中排除的属性，并防止它们从被排除的字段继承标签。

有关自动强制执行在平台中的工作原理的详细信息，请参阅[自动策略强制执行](../enforcement/auto-enforcement.md)的概述。

### 从Adobe Audience Manager数据导出控件继承

[!DNL Experience Platform] 能够与Adobe Audience Manager共享细分。已应用于Audience Manager段的任何数据导出控件均转换为由[!DNL Experience Platform] [!DNL Data Governance]识别的等效标签和营销操作。

有关具体的Audience Manager导出控件如何映射到[!DNL Platform]中的数据使用标签的参考，请参阅[数据文档](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)。

## 管理[!DNL Experience Platform] {#manage-labels}中的数据使用标签

您可以使用[!DNL Experience Platform] API或用户界面管理数据使用标签。 有关每个子部分的详细信息，请参阅下面的子部分。

### 使用UI

[!DNL Experience Platform] UI中的&#x200B;**[!UICONTROL Policies]**&#x200B;工作区允许您视图和管理组织的核心标签和自定义标签。 **[!DNL Datasets]**&#x200B;工作区允许您将标签应用于数据集和字段。 有关详细信息，请参阅[标签用户指南](user-guide.md)。

### 使用API

[策略服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)中的`/labels`端点允许您以编程方式管理数据使用标签，包括创建自定义标签。 有关详细信息，请参阅[labels endpoint guide](../api/labels.md)。

[数据集服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml)用于管理数据集和字段的标签。 有关详细信息，请参阅[管理数据集标签](./dataset-api.md)指南。

## 后续步骤

本文档介绍了数据使用标签及其在数据治理框架中的作用。 请参阅本指南中链接的文档，进一步了解如何管理[!DNL Experience Platform]中的标签。
