---
keywords: Experience Platform；主页；热门主题；数据管理；数据使用标签api；策略服务api；数据使用标签概述
solution: Experience Platform
title: 数据使用标签概述
description: 了解如何使用数据使用标签来帮助在Adobe Experience Platform中实施数据管理合规性。
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 5d34781e06c0fa8bfd2e52f73e336d92d16192f6
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 15%

---

# 数据使用标签概述 {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="控制访问敏感和受保护的数据"
>abstract="<h2>描述</h2><p>通过控制访问特定的数据属性和/或区段，可为操作 Experience Platform 用例的各种角色和团队设计灵活的工作流。</p>"

Adobe Experience Platform允许您将数据使用标签应用于数据集和字段，并根据相关对每个数据集和字段进行分类 [数据治理策略](../policies/overview.md) 和 [访问控制策略](../../access-control/abac/ui/policies.md).

本文档概述了中的数据使用标签 [!DNL Experience Platform].

## 了解数据使用标签

使用数据使用标签，可根据适用于数据集和字段的治理策略对数据集和字段进行分类。 您可以随时应用标签，灵活地选择管理数据的方式。 最佳实践鼓励在将数据摄取到其中后立即为其设置标签 [!DNL Experience Platform]，或当数据可用于以下项目时 [!DNL Platform].

在数据集级别应用的数据使用标签会传播到数据集中的所有字段。 标签也可以直接应用于数据集中的单个字段（列标题），而无需传播。

[!DNL Platform] 提供了多个现成的“核心”数据使用标签，涵盖了适用于数据治理的各种常见限制。 有关这些标签及其代表的治理政策的更多信息，请参阅以下内容中的指南： [核心数据使用标签](reference.md).

除了Adobe提供的标签之外，您还可以为组织定义自己的自定义标签。 请参阅以下部分 [管理标签](#manage-labels) 以了解更多信息。

## 受众区段的标签继承

创建的所有受众区段 [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) 继承其相应数据集的使用标签。 这允许Experience Platform在将区段激活到目标时提供自动策略实施。

除了继承数据集级别的标签之外，默认情况下，区段还从关联的数据集中继承所有字段级别的标签。 因此，您可以更轻松地识别应从区段中排除的属性，并阻止这些属性从排除的字段中继承标签。

有关自动实施如何在Platform中工作的更多信息，请参阅的概述 [自动策略执行](../enforcement/auto-enforcement.md).

### 从Adobe Audience Manager数据导出控件的继承

[!DNL Experience Platform] 能够与Adobe Audience Manager共享区段。 已应用于Audience Manager区段的任何数据导出控件将转换为由识别的等效标签和营销操作 [!DNL Experience Platform] 数据管理。

有关特定数据导出控件如何映射到中的数据使用标签的参考 [!DNL Platform]，请参阅 [Audience Manager文档](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## 管理 [!DNL Experience Platform] 中的数据使用标签 {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="说明"
>abstract="<ul><li>为 XDM 字段和区段加标签以划分要限制访问其的字段和/或区段。</li><li>为角色加标签，通过将标签添加到角色，可定义此角色的成员应在其上具有限制的标签。</li><li>创建策略，策略在加了标签的对象（如 XDM 字段和区段）上的标签与角色上的标签之间建立关系。如果标签匹配，则可以定义允许或限制访问。</li></ul>"

您可以使用以下工具管理数据使用标签 [!DNL Experience Platform] API或用户界面。 有关每个报表包的详细信息，请参阅下面的子部分。

### 使用UI

此 **[!UICONTROL 策略]** 中的工作区 [!DNL Experience Platform] UI允许您查看和管理组织的核心标签和自定义标签。 您可以使用 **[!UICONTROL 架构]** 工作区至 [将标签应用于您的体验数据模型(XDM)架构](../../xdm/tutorials/labels.md)，或了解如何 [在**中创建和管理自定义标签[!UICONTROL 策略] UI](./user-guide.md) 而是通过阅读数据使用标签用户指南。

>[!IMPORTANT]
>
>标签无法再应用于数据集级别的字段。 此工作流已弃用，支持在架构级别应用标签。 在2024年5月31日之前，之前在数据集对象级别应用的任何标签仍将通过Platform UI受到支持。 要确保您的标签在所有架构中保持一致，在未来一年中，必须将之前附加到数据集级别字段的任何标签迁移到架构级别。 请参阅以下部分 [迁移以前应用的标签](../e2e.md#migrate-labels) 以获取有关如何执行此操作的说明。

### 使用API

此 `/labels` 中的端点 [策略服务API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 允许您以编程方式管理数据使用标签，包括创建自定义标签。 请参阅 [标签端点指南](../api/labels.md) 以了解更多信息。

此 [数据集服务API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 用于管理数据集和字段的标签。 请参阅指南，网址为 [管理数据集标签](./dataset-api.md) 以了解更多信息。

## 后续步骤

本文档介绍了数据使用标签及其在数据管理框架中的角色。 请参阅本指南中链接的文档，了解更多有关如何在中管理标签的信息 [!DNL Experience Platform].
