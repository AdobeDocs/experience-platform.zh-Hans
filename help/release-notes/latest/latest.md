---
title: Adobe Experience Platform 发行说明（2025 年 7 月）
description: Adobe Experience Platform 的 2025 年 7 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: ht
source-wordcount: '1574'
ht-degree: 100%

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

**发行日期：2025 年 7 月 29 日**

Adobe Experience Platform 中新功能和现有功能的更新：

- [容量](#capacity)
- [目标](#destinations)
- [数据摄取](#data-ingestion)
- [Real-Time CDP B2B Edition](#b2b)
- [沙盒](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [源](#sources)


## 容量 {#capacity}

>[!AVAILABILITY]
>
>此功能的可用性将因您的所在地区而异。美洲地区的用户可从 8 月 11 日起使用该功能。欧洲地区的用户可从 8 月 25 日起使用该功能。亚洲地区的用户可从 9 月 8 日起使用该功能。

“容量”功能可全面显示您组织的[护栏](../../rtcdp/guardrails/overview.md)，并提供建议，帮助您在沙盒层级分配容量，以解决可能发生的容量超限问题。在此发行版本中，您可以查看流式摄取和流式分段的容量情况。

详细信息请参阅[容量概述](../../landing/license-usage-and-guardrails/capacity.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**更新的目标**

| 目标 | 描述 |
| --- | --- |
| [Google 目标客户匹配功能 + Display &amp; Video 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) 连接的可用性受到限制 | 该集成曾在 6 月暂时提供给所有客户，Adobe 现已将其恢复为限制提供。目前，只有已启用的客户有权访问该目标，Adobe 正与 Google 共同解决相关的实施问题。如果您希望在恢复更大范围的发布后使用此集成，请联系您的 Adobe 代表并表达您的意愿。 |
| [[!DNL The Trade Desk]](../../destinations/catalog/advertising/tradedesk.md) 内部升级 | 从 2025 年 7 月 31 日开始，您可以在目标目录中看到并排的两张 [!DNL The Trade Desk] 卡。这是由于目标服务内部升级造成的。<br><br>现有的 [!DNL The Trade Desk] 目标连接器已更名为&#x200B;**[!UICONTROL （已弃用）The Trade Desk]**，现在提供一个名为 **[!UICONTROL The Trade Desk]** 的新卡片。将目录中新的 **[!UICONTROL The Trade Desk]** 连接用于新的激活数据流。<br><br>如果您有任何连接到&#x200B;**[!UICONTROL （已弃用）The Trade Desk]** 目标的激活数据流，它们将自动更新，您无需执行任何操作。<br><br>如果您通过 [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 创建数据流，则必须将 [!DNL flow spec ID] 和 [!DNL connection spec ID] 更新为以下值：<ul><li>流量规范 ID：`86134ea1-b014-49e8-8bd3-689f4ce70578`</li><li>连接规范 ID：`1029798b-a97f-4c21-81b2-e0301471166e`</li></ul> |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 为目标连接提供帐户名称和描述 | 您现在可以在连接目标时[添加帐户名称和描述](/help/destinations/ui/connect-destination.md)，以便更高效地管理包含多个帐户的目标平台。 |
| 增强边缘目标的数据流信息 | [Adobe Target](/help/destinations/catalog/personalization/adobe-target-v2.md) 和[自定义个性化](/help/destinations/catalog/personalization/custom-personalization.md)目标的右侧信息边栏经过优化，可显示数据流名称，从而能够更清晰地了解相关联的数据流配置，有助于在审查现有数据流时减少混淆。目标配置页面中的&#x200B;**[!UICONTROL 数据流 ID]** 选择器现已更名为&#x200B;**[!UICONTROL 数据流]**，以提升用户界面的清晰度。 |
| 目标选择中的营销操作可见性 | 在目标工作区的&#x200B;**[[!UICONTROL 浏览]](/help/destinations/ui/destinations-workspace.md#browse)**&#x200B;选项卡以及&#x200B;**[[!UICONTROL 数据流运行]](/help/dataflows/ui/monitor-destinations.md)**&#x200B;页面中，营销操作现在显示在右侧信息边栏，您无需跳转至视图页面即可快速查看营销操作的变化。这一改进有助于在设置目标时更轻松地验证营销操作配置，从而提升用户体验。 |
| [!BADGE 限量 beta 版]{type=Informative} 编辑目标的营销操作 | 您现在可以为现有目标[编辑营销操作](/help/destinations/ui/edit-activation.md#edit-marketing-actions)。该功能目前在限量 beta 版中提供。要请求访问权限，请与 Adobe 代表联系。 |
| [!BADGE 限量 beta 版]{type=Informative} 编辑目标 | 您现在可以在目标创建完成后[编辑该目标的配置](/help/destinations/ui/edit-destination.md)。该功能目前在限量 beta 版中提供。要请求访问权限，请与 Adobe 代表联系。 |

**修复**

| 问题 | 描述 |
| --- | --- |
| 类别滚动功能 | 修复了在目标和源目录中的类别侧边菜单在鼠标悬停时无法正常滚动的问题，从而改善了用户在浏览目标类别时的导航体验。 |

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## 数据摄取 {#ingestion}

Experience Platform 提供了一个全面的数据摄取框架，可支持从多个来源进行批量和流式数据摄取。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持监控流式轮廓摄取 | 现在支持实时监测流式轮廓摄取的情况，以便清晰了解吞吐量、延迟和数据质量等量度。该功能支持主动预警和可操作的洞察，以帮助数据工程师识别容量违规和摄取问题。请阅读[流式轮廓摄取监控](../../dataflows/ui/monitor-streaming-profile.md)指南，以获取更多信息。 |

更多详情，请参阅[数据摄取概述](../../ingestion/home.md)。

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B Edition 提供全面的 B2B 客户数据管理能力，支持组织构建统一的客户轮廓、创建复杂的 B2B 受众，并在各种不同的营销渠道中激活数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| B2B 架构升级 | Experience Platform 正在升级至全新的 B2B 架构，为具有 B2B 属性的多实体受众带来显著改进。此次升级统一了合并策略支持、提升了受众计数的准确性，并增强了实体解析能力。请阅读 [Real-Time CDP B2B Edition 架构升级概述](../../rtcdp/b2b-architecture-upgrade.md)，获取完整的更改说明。 |
| 多实体受众的合并策略统一 | 具有 B2B 属性的多实体受众现在仅支持一种合并策略，即默认合并策略，而不再支持多个合并策略。这一变化可确保受众构成的一致性，并简化合并逻辑的管理。如需了解更多信息，请参阅[合并策略概述](../../profile/merge-policies/overview.md)。 |
| 增强了 B2B 实体的受众计数 | 现在，因基于实时分段结果，因此能够准确估算包含 B2B 实体（如帐户和机会）的受众的规模。这一改进提升了涉及复杂 B2B 关系的受众的估算准确性与可靠性。 |
| 受众会员资格的帐户快照 | 账户实体的快照导出现在包含受众会员资格详情，这样可查看帐户级的受众状态、时间戳及会员资格标记。此功能确保了轮廓（个人）与帐户分段模型之间的功能对等性。 |
| 多实体受众的沙盒工具变化 | 不再支持对迁移前导出的包含 B2B 实体和体验事件的多实体受众的导入功能。此类受众将无法通过导入验证，也无法自动转换为新架构。这些受众需在迁移后重新导出，然后才能导入目标沙盒。详情请参阅[沙盒工具支持对象指南](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)。 |
| B2B 实体 API 弃用 | [!DNL Profile Access]对以下 B2B 实体的 API 查找操作现已弃用：帐户-个人关系、机会-个人关系、营销活动、营销活动成员、营销名单及营销名单成员。此外，针对帐户、帐户-个人关系、机会、机会-个人关系、营销活动、营销活动成员、营销名单及其成员等 B2B 实体的[!DNL Profile Access] API 删除操作也已弃用。如需了解详情，请参阅[实体端点 API 指南](../../profile/api/entities.md)。 |
| 更新了实体解析的身份标识命名空间 | 帐户与机会实体现在采用基于时间优先级的合并方式，并使用专属身份标识命名空间（帐户使用 `b2b_account`，机会使用 `b2b_opportunity`）。其他所有实体均通过主身份标识重叠项，以时间优先方式统一合并。如需了解实体解析的更多信息，请参阅[实体端点 API 指南](../../profile/api/entities.md)。 |

有关更多信息，请参阅 [Real-Time CDP B2B Edition 概述](../../rtcdp/b2b-overview.md)。

## 沙盒 {#sandboxes}

Experience Platform 旨在全球范围内扩充数字体验应用。企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 多实体受众导入的变化 | 沙盒工具已更新，以支持新的 B2B 架构升级。包含 B2B 实体与体验事件的多实体受众在架构升级后必须重新导出，才能通过沙盒工具导入至目标沙盒环境。升级前的版本将无法通过导入验证。详情请参阅 [沙盒工具支持对象指南](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)。 |

有关沙盒的更多信息，请阅读[沙盒概述](../../sandboxes/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。受众可以基于记录型数据（如人口统计信息）或时间序列事件（代表客户与品牌的互动行为）进行构建。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 外部受众 API | 您可使用外部受众 API 以编程方式将外部生成的受众导入 Adobe Experience Platform。如需了解详情，请参阅[外部受众端点指南](../../segmentation/api/external-audiences.md)。 |

有关受众分段的更多信息，请参阅[分段服务概述](../../segmentation/home.md)

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新来源**

| 来源 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative} 支持 [!DNL Didomi]（Streaming SDK） | 使用 [!DNL Didomi] 源摄取来自 [!DNL Didomi] 的同意与偏好管理数据，此方法支持符合隐私法规的合规操作和基于同意的营销策略。请阅读[[!DNL Didomi] 来源概述](../../sources/connectors/consent-and-preferences/didomi.md)，了解设置方法。关于创建来源连接的步骤，请参阅[[!DNL Didomi] 来源连接指南](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md)。 |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持使用 [!DNL Flow Service] API 实现部分来源中的变更数据捕获 | 您现在可以通过源连接器创建支持变更数据捕获的数据流，以实现增量摄取。该功能允许客户将变更数据类型用于增量摄取，有助于提升数据实时性并降低处理负载。若要了解更多信息，请阅读[为来源使用变更数据捕获](../../sources/tutorials/api/change-data-capture.md)文档 |
| 支持软删除 [!DNL Salesforce] 中的记录 | [!DNL Salesforce] 源现在支持通过一个可选的 `includeDeletedObjects` 参数包含被软删除的记录。设置为 true 后，客户可以在其 [!DNL Salesforce] 查询中包含被软删除的记录，并将这些记录导入 Experience Platform。有关详细信息，请阅读[[!DNL Salesforce] 源文档](../../sources/connectors/crm/salesforce.md)。 |

有关更多信息，请阅读[来源概述](../../sources/home.md)。
