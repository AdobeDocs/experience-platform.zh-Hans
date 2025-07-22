---
title: Experience Platform预发行说明
description: Adobe Experience Platform最新发行说明预览。
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: d30778ef3152b779157206ce0d416c0e61ba98c3
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 21%

---

# Adobe Experience Platform预发行说明

>[!IMPORTANT]
>
>本文档旨在作为当月发行说明的&#x200B;**预览**。 版本项目可能会发生更改，并且可能会在最终版本中添加或删除。

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

- [目标](#destinations)
- [数据引入](#ingestion)
- [查询服务](#query-service)
- [Real-Time CDP B2B 版](#b2b)
- [沙盒](#sandboxes)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**已更新目标**

| 目标 | 描述 |
| --- | --- |
| Marketo目标卡整合 | Marketo V2和Marketo Engage人员同步目标卡已合并到单个统一目标卡中。 此整合简化了目标选择过程，并为Marketo集成提供了更简化的体验。 |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 数据登录区(DLZ)目标加密支持 | 为数据登陆区目标添加了加密支持。 您现在可以附加RSA格式公钥以向导出的文件添加加密，从而为敏感数据导出提供增强的安全性。 |
| 边缘目标的增强数据流信息 | 改进了Adobe Target和自定义Personalization目标的右边栏信息现在同时显示数据流名称和数据流ID字段，从而更清楚地了解关联的数据流配置并减少查看现有数据流时的混淆。 目标配置屏幕中的&#x200B;**[!UICONTROL 数据流ID]**&#x200B;选择器已更新为&#x200B;**[!UICONTROL 数据流]**，以提高用户界面中的清晰度。 |
| 目标选择中的营销活动可见性 | 现在，在配置数据流时，营销操作显示在[!UICONTROL 选择目标]步骤的右边栏中，无需导航到视图页面即可立即看到营销操作更改。 这项改进增强了用户体验，因为它使得在目标设置期间验证营销行动配置变得更加容易。 |
| 编辑目标的营销操作 | 您现在可以编辑现有目标的营销操作。 |
| 目标连接的帐户名称和描述 | 现在，您可以在连接到目标时添加帐户名称和描述，从而更好地管理具有多个帐户的目标。 |

**修复**

| 问题 | 描述 |
| --- | --- |
| 类别滚动功能 | 修复了目标和源目录中的类别侧菜单未在鼠标悬停时正确滚动的问题，从而提高用户浏览目标类别的导航可用性。 |

有关更多信息，请阅读[目标概述](../destinations/home.md)。

## 数据引入 {#ingestion}

Experience Platform提供了一个全面的数据摄取框架，该框架支持从各种来源进行批量摄取和流式摄取。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持监控流配置文件摄取 | 现在提供了对流式配置文件摄取的实时监控，从而透明地显示吞吐量、延迟和数据质量指标。 这支持主动警报和可操作的洞察，以帮助数据工程师识别容量违规和摄取问题。 |

有关详细信息，请阅读[数据引入概述](../ingestion/home.md)。

## 查询服务 {#query-service}

Adobe Experience Platform查询服务提供了一个强大的SQL接口，可用于跨平台进行数据分析和探索。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 增强的会话管理 | Data Distiller现在包括增强的会话管理功能，更好地控制用户会话并改进跨开发和生产环境的性能监控。 |
| 支持不过期凭据密码字符限制 | Data Distiller现在支持具有特定字符限制的非过期凭据。 虽然密码至少需要一个数字、一个小写字母、一个大写字母和一个特殊字符，但美元符号($)不受支持。 推荐的特殊字符包括`!, @, #, ^, or &`。 |
| 提高了跨环境的性能一致性 | 数据Distiller性能现在在开发沙盒和生产沙盒之间保持一致，在两个环境中都提供了相似的后端资源。 使用的计算小时数可能因处理时的数据量和可用的后端计算资源而异。 |

有关详细信息，请阅读[查询服务概述](../query-service/home.md)。

## Real-Time CDP B2B 版 {#b2b}

Real-Time CDP B2B edition提供全面的B2B客户数据管理功能，使组织能够构建统一的客户档案、创建复杂的B2B受众并在各种营销渠道中激活数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| B2B架构升级 | Experience Platform正在升级到新的B2B架构，该架构对具有B2B属性的多实体受众引入了重大改进。 此升级整合了合并策略支持，提高了受众计数的准确性，并改进了实体解析功能。 |
| 多实体受众的合并策略合并 | 具有B2B属性的多实体受众现在仅支持单个合并策略（默认合并策略），不支持多个合并策略。 此更改可确保一致的受众构成并简化合并逻辑管理。 |
| 更新了帐户受众限制 | 帐户受众不再具有以前对体验事件的30天回溯时间范围的限制、自定义实体限制或使用`inSegment`事件的限制。 这些更新在创建复杂的B2B受众定义方面提供了更大的灵活性。 |
| 增强了B2B实体的受众计数 | 现在，根据实时分段结果，可以准确地估计具有B2B实体（如客户和机会）的受众规模。 这种改进为涉及复杂B2B关系的受众提供了更准确和可靠的估计。 |
| 适用于受众成员资格的帐户快照 | 现在，快照导出中包含了“帐户”实体的受众成员资格详细信息，从而可以访问帐户级别的受众状态、时间戳和成员资格指标。 这使得用户档案（人员）和帐户分段模型之间存在功能对等性。 |
| 多实体受众的沙盒工具更改 | 不再支持在迁移之前通过导出的B2B实体和体验事件导入多实体受众。 这些受众将无法通过导入验证，且无法自动转换为新架构。 迁移后，必须先重新导出受众，然后才能将其导入目标沙盒中。 |
| B2B实体API弃用 | 现已弃用通过API为B2B实体（帐户、机会、帐户 — 人员关系、机会 — 人员关系、营销活动、营销活动成员、营销列表和营销列表成员）创建受众。 此外，也不建议对这些B2B实体执行配置文件访问API查找和删除操作。 |
| 更新了实体解析的身份命名空间 | Account和Opportunity实体现在使用基于时间优先级的与特定身份命名空间合并（`b2b_account`用于帐户，`b2b_opportunity`用于机会）。 所有其它实体通过基于时间优先的合并合并与主标识重叠合并。 |

有关详细信息，请阅读[Real-Time CDP B2B edition概述](../rtcdp/b2b-overview.md)。

## 沙盒 {#sandboxes}

Experience Platform旨在丰富全球范围内的数字体验应用程序。 企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 对多实体受众导入的更改 | 沙盒工具已更新，以支持新的B2B架构升级。 在架构升级后，必须重新导出包含B2B实体和体验事件的多实体受众，然后才能通过沙盒工具导入目标沙盒中。 导入升级前版本将导致验证失败。 |

有关沙盒的更多信息，请阅读[沙盒概述](../sandboxes/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。受众可以基于记录型数据（如人口统计信息）或时间序列事件（代表客户与品牌的互动行为）进行构建。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 外部受众API | 您可以使用外部受众API以编程方式将外部生成的受众导入Adobe Experience Platform。 |

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新来源**

| 来源 | 描述 |
| --- | --- |
| 支持[!DNL Didomi] (流式SDK) | [!DNL Didomi]源连接器允许您从[!DNL Didomi]的平台中摄取同意管理数据，支持遵守隐私法规和基于同意的营销策略。 |

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持选定源中的变更数据捕获 | 您现在可以创建数据流，以便使用源连接器为增量摄取启用变更数据捕获。 此功能允许客户为增量摄取引入更改数据类型，从而提高数据新鲜度并减少处理开销。 |
| 支持软删除[!DNL Salesforce]中的记录 | [!DNL Salesforce]源现在支持通过可选的`includeDeletedObjects`参数包含软删除记录。 如果设置为true，客户可以在其[!DNL Salesforce]查询中包含软删除记录，并将这些记录导入Experience Platform。 |

有关更多信息，请阅读[数据源概述](../sources/home.md)。
