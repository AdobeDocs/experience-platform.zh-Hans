---
title: Adobe Experience Platform 发行说明（2025 年 7 月）
description: Adobe Experience Platform 的 2025 年 7 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 22%

---

# Adobe Experience Platform 发行说明

>[!TIP]
>
>有关其他 Adobe Experience Platform 应用程序的发行说明，请参阅以下文档：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/releases/pre-release-notes)
>- [联合受众构成](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hans/docs/real-time-cdp-collaboration/using/latest)

**发行日期： 2025年7月29日**

Adobe Experience Platform 中新功能和现有功能的更新：

- [容量](#capacity)
- [目标](#destinations)
- [数据引入](#data-ingestion)
- [Real-Time CDP B2B 版](#b2b)
- [沙盒](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [源](#sources)


## 容量 {#capacity}

>[!AVAILABILITY]
>
>根据您所在的区域，此功能将可供使用。 对于美洲用户，此功能将从8月11日起提供。 对于欧洲的用户，此功能将从8月25日开始提供。 对于亚洲的用户，此功能将从9月8日开始提供。

容量提供组织[护栏](../../rtcdp/guardrails/overview.md)的全面视图，并提供有关如何通过在沙盒级别分配容量来解决潜在容量违规的建议。 在此版本中，您可以查看流摄取和流分段的容量。

有关详细信息，请阅读[容量概述](../../landing/license-usage-and-guardrails/capacity.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**已更新目标**

| 目标 | 描述 |
| --- | --- |
| [Google Customer Match + Display &amp; Video 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md)连接的可用性有限 | 在6月份向所有客户简要推出后，Adobe已将此集成恢复为有限可用。 目前，此目标的访问仅限于已启用的客户，而Adobe和Google正在努力解决实施问题。 如果您希望在更广泛的推出恢复后使用此集成，请联系您的Adobe代表来表达您的意图。 |
| [[!DNL The Trade Desk]](../../destinations/catalog/advertising/tradedesk.md)内部升级 | 从2025年7月31日开始，您可以在目标目录中并排看到两张[!DNL The Trade Desk]信息卡。 这是由于目标服务内部升级造成的。<br><br>现有[!DNL The Trade Desk]目标连接器已重命名为&#x200B;**[!UICONTROL （已弃用）交易台]**&#x200B;和名称为&#x200B;**[!UICONTROL 交易台]**&#x200B;的新卡现在可用。 使用目录中的新&#x200B;**[!UICONTROL 交易台]**&#x200B;连接获取新的激活数据流。 <br><br>如果您有任何到&#x200B;**[!UICONTROL （已弃用）交易台]**&#x200B;目标的活动数据流，它们会自动更新，因此您无需执行任何操作。 <br><br>如果您是通过[流服务API](https://developer.adobe.com/experience-platform-apis/references/destinations/)创建数据流，则必须将[!DNL flow spec ID]和[!DNL connection spec ID]更新为以下值：<ul><li>流量规范 ID：`86134ea1-b014-49e8-8bd3-689f4ce70578`</li><li>连接规范 ID：`1029798b-a97f-4c21-81b2-e0301471166e`</li></ul> |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 目标连接的帐户名称和描述 | 现在，在连接到目标时，您可以[添加帐户名称和描述](/help/destinations/ui/connect-destination.md)，从而更好地管理具有多个帐户的目标。 |
| 边缘目标的增强数据流信息 | [Adobe Target](/help/destinations/catalog/personalization/adobe-target-v2.md)和[自定义Personalization](/help/destinations/catalog/personalization/custom-personalization.md)目标的右边栏信息已得到改进，可以显示数据流名称，从而可以更清楚地了解关联的数据流配置，并有助于在查看现有数据流时减少混淆。 目标配置屏幕中的&#x200B;**[!UICONTROL 数据流ID]**&#x200B;选择器已更新为&#x200B;**[!UICONTROL 数据流]**，以提高用户界面中的清晰度。 |
| 目标选择中的营销活动可见性 | 营销操作现在显示在目标工作区中&#x200B;**[[!UICONTROL 浏览]](/help/destinations/ui/destinations-workspace.md#browse)**&#x200B;选项卡的右边栏和&#x200B;**[[!UICONTROL 数据流运行]](/help/dataflows/ui/monitor-destinations.md)**&#x200B;页面上，无需导航到视图页面即可即时查看营销操作更改。 此增强功能使得在目标设置期间验证营销操作配置变得更加容易，从而改善了用户体验。 |
| [!BADGE 有限测试版]{type=Informative}编辑目标的营销操作 | 您现在可以[编辑现有目标的营销操作](/help/destinations/ui/edit-activation.md#edit-marketing-actions)。 此功能当前为有限测试版。 要请求访问权限，请与 Adobe 代表联系。 |
| [!BADGE 有限测试版]{type=Informative}编辑目标 | 创建目标配置[后，您现在可以](/help/destinations/ui/edit-destination.md)编辑该配置。 此功能当前为有限测试版。 要请求访问权限，请与 Adobe 代表联系。 |

**修复**

| 问题 | 描述 |
| --- | --- |
| 类别滚动功能 | 修复了目标和源目录中的类别侧菜单未在鼠标悬停时正确滚动的问题，从而提高用户浏览目标类别的导航可用性。 |

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## 数据引入 {#ingestion}

Experience Platform提供了一个全面的数据摄取框架，该框架支持从各种来源进行批量摄取和流式摄取。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持监控流配置文件摄取 | 现在提供了对流式配置文件摄取的实时监控，从而透明地显示吞吐量、延迟和数据质量指标。 这支持主动警报和可操作的洞察，以帮助数据工程师识别容量违规和摄取问题。 有关详细信息，请阅读有关[监视流式配置文件摄取](../../dataflows/ui/monitor-streaming-profile.md)的指南。 |

有关详细信息，请阅读[数据引入概述](../../ingestion/home.md)。

## Real-Time CDP B2B 版 {#b2b}

Real-Time CDP B2B edition提供全面的B2B客户数据管理功能，使组织能够构建统一的客户档案、创建复杂的B2B受众并在各种营销渠道中激活数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| B2B架构升级 | Experience Platform正在升级到新的B2B架构，该架构对具有B2B属性的多实体受众引入了重大改进。 此升级整合了合并策略支持，提高了受众计数的准确性，并改进了实体解析功能。 阅读[Real-Time CDP B2B edition架构升级概述](../../rtcdp/b2b-architecture-upgrade.md)，全面了解更改情况。 |
| 多实体受众的合并策略合并 | 具有B2B属性的多实体受众现在仅支持单个合并策略（默认合并策略），不支持多个合并策略。 此更改可确保一致的受众构成并简化合并逻辑管理。 有关详细信息，请阅读[合并策略概述](../../profile/merge-policies/overview.md)。 |
| 增强了B2B实体的受众计数 | 现在，根据实时分段结果，可以准确地估计具有B2B实体（如客户和机会）的受众规模。 这种改进为涉及复杂B2B关系的受众提供了更准确和可靠的估计。 |
| 适用于受众成员资格的帐户快照 | 现在，快照导出中包含了“帐户”实体的受众成员资格详细信息，从而可以访问帐户级别的受众状态、时间戳和成员资格指标。 这使得用户档案（人员）和帐户分段模型之间存在功能对等性。 |
| 多实体受众的沙盒工具更改 | 不再支持在迁移之前通过导出的B2B实体和体验事件导入多实体受众。 这些受众将无法通过导入验证，且无法自动转换为新架构。 迁移后，必须先重新导出受众，然后才能将其导入目标沙盒中。 有关详细信息，请阅读有关沙盒工具[支持的对象的](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)指南。 |
| B2B实体API弃用 | 现已弃用B2B实体（帐户 — 人员关系、机会人员关系、营销活动、营销活动成员、营销列表和营销列表成员）的[!DNL Profile Access] API查找操作。 此外，还弃用了B2B实体（帐户、帐户 — 人员关系、机会、机会人员关系、营销活动、营销活动成员、营销列表和营销列表成员）的[!DNL Profile Access] API删除操作。 有关详细信息，请阅读[实体端点API指南](../../profile/api/entities.md)。 |
| 更新了用于实体解析的身份命名空间 | Account和Opportunity实体现在使用基于时间优先级的与特定身份命名空间合并（`b2b_account`用于帐户，`b2b_opportunity`用于机会）。 所有其它实体通过基于时间优先的合并合并与主标识重叠合并。 有关实体解析的详细信息，请阅读[实体端点API指南](../../profile/api/entities.md)。 |

有关详细信息，请阅读[Real-Time CDP B2B edition概述](../../rtcdp/b2b-overview.md)。

## 沙盒 {#sandboxes}

Experience Platform旨在丰富全球范围内的数字体验应用程序。 企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 对多实体受众导入的更改 | 沙盒工具已更新，以支持新的B2B架构升级。 在架构升级后，必须重新导出包含B2B实体和体验事件的多实体受众，然后才能通过沙盒工具导入目标沙盒中。 导入升级前版本将导致验证失败。 有关详细信息，请阅读有关沙盒工具[支持的对象的](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)指南。 |

有关沙盒的更多信息，请阅读[沙盒概述](../../sandboxes/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。受众可以基于记录型数据（如人口统计信息）或时间序列事件（代表客户与品牌的互动行为）进行构建。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 外部受众API | 您可以使用外部受众API以编程方式将外部生成的受众导入Adobe Experience Platform。 有关详细信息，请阅读[外部受众端点指南](../../segmentation/api/external-audiences.md)。 |

有关分段的详细信息，请阅读[分段服务概述](../../segmentation/home.md)

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新来源**

| 来源 | 描述 |
| --- | --- |
| 对[!BADGE 的]{type=Informative}Beta[!DNL Didomi]支持(流式SDK) | 使用[!DNL Didomi]源从[!DNL Didomi]中摄取同意和偏好设置管理数据，支持遵守隐私法规和基于同意的营销策略。 有关如何获取设置的信息，请阅读[[!DNL Didomi] 源概述](../../sources/connectors/consent-and-preferences/didomi.md)。 有关创建源连接的步骤，请阅读[[!DNL Didomi] 源连接指南](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md)。 |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持使用[!DNL Flow Service] API在选定源中捕获变更数据 | 您现在可以创建数据流，以便使用源连接器为增量摄取启用变更数据捕获。 此功能允许客户为增量摄取引入更改数据类型，从而提高数据新鲜度并减少处理开销。 有关详细信息，请阅读有关[对源使用更改数据捕获](../../sources/tutorials/api/change-data-capture.md)的文档 |
| 支持软删除[!DNL Salesforce]中的记录 | [!DNL Salesforce]源现在支持通过可选的`includeDeletedObjects`参数包含软删除记录。 如果设置为true，客户可以在其[!DNL Salesforce]查询中包含软删除记录，并将这些记录导入Experience Platform。 有关详细信息，请阅读[[!DNL Salesforce] 源文档](../../sources/connectors/crm/salesforce.md)。 |

有关更多信息，请阅读[数据源概述](../../sources/home.md)。
