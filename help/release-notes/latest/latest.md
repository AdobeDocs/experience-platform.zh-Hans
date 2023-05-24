---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform 2023年5月版发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 85401e3abfd7d5d1d84e082d20a1a064760c4e19
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 4%

---

# Adobe Experience Platform 发行说明

>[!IMPORTANT]
>
>为了准备Audience Portal功能的正式发布，Adobe Experience Platform正在更新系统和文档中“受众”和“区段”的使用情况。
>
>- **Audience**：一组人员、帐户、家庭或具有共同特征和行为的其他实体。
>
>- **区段定义**：在Adobe Experience Platform中，用于描述目标受众关键特征或行为的规则。 此术语以前称为“区段”。
>
>- **区段**：将用户档案划分为受众的操作。 术语“区段”现在只用作动词。
>
>- **分段**：识别和阐明将分组在一起以生成一组结果（如受众）的用户档案特征的行为。
>
>因此，在Adobe Experience Platform UI中，您将看到“区段”被“受众”取代，以反映这种创建和管理受众的新途径。

**发布日期：2023 年 5 月 24 日**

Adobe Experience Platform 现有功能的更新包括：

- [数据收集](#data-collection)
- [数据治理](#data-governance)
- [数据引入](#data-ingestion)
- [查询服务](#query-service)
- [源](#sources)

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，可让您收集客户端客户体验数据并将该数据发送到Adobe Experience Platform Edge Network，可在其中扩充和转换数据，并将其分发到Adobe或非Adobe目标。

**新增或更新功能**

| 功能 | 描述 |
| --- | --- |
| [!DNL Twitter] 转化API扩展 | 此 [[!DNL Twitter] 转化API](../../tags/extensions/server/twitter/overview.md) 事件转发扩展允许您使用实时在服务器端转发事件数据，以进行事件转换。 [!DNL Twitter] 转化API。 |
| 数据元素路径帮助 | 确定数据元素在 [核心扩展](../../tags/extensions/client/core/overview.md) 现在比以往任何时候都更容易。 此增强功能会提供一个引导式表单，帮助您选择和设置正确的数据元素路径的格式。 |

{style="table-layout:auto"}

要了解有关数据集合的更多信息，请阅读 [数据集合概述](../../tags/home.md).

## 数据治理 {#data-governance}

Adobe Experience Platform数据管理是用于管理客户数据并确保遵守适用于数据使用的法规、限制和策略的一系列策略和技术。 它在各个级别的Experience Platform中发挥着关键作用，包括编目、数据谱系、数据使用标签、数据访问策略和对营销活动数据的访问控制。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 数据集字段级别标签弃用 | 将标签应用于单个字段的功能已从数据集移至架构。 这允许您集中管理上游用于数据治理、同意和访问控制的字段标签。 先前应用的数据集字段标签将通过Experience PlatformUI暂时受支持。 您需要在2024年5月31日之前手动将任何现有数据集字段标签迁移到架构字段标签。 请阅读 [数据治理端到端指南](../../data-governance/e2e.md) 以了解有关标签迁移的更多信息。 |

{style="table-layout:auto"}

要了解有关数据管理的更多信息，请参阅 [数据治理概述](../../data-governance/home.md).

## 数据引入 {#data-ingestion}

Adobe Experience Platform提供了一组丰富的功能，可用于摄取任何类型和任何延迟的数据。 您可以使用Adobe构建的源、数据集成合作伙伴或Adobe Experience Platform UI，使用批处理或流API进行摄取。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 数据摄取模板的Beta版可用性 | 数据摄取模板为数据架构师和工程师提供了标准模板和自动化工具，可加快数据摄取过程，包括架构和数据集创建以及映射规则配置。 数据摄取模板当前可用于 [[!DNL Marketo Engage]](../../sources/connectors/adobe-applications/marketo/marketo.md)， [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) 和 [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) 源。 有关详细信息，请阅读以下指南： [在UI中使用模板](../../sources/tutorials/ui/templates.md). |

要了解有关数据摄取的更多信息，请参阅 [数据摄取概述](../../ingestion/home.md).

## 查询服务 {#query-service}

查询服务允许您使用标准SQL在Adobe Experience Platform中查询数据 [!DNL data lake]. 您可以加入数据湖中的任何数据集，并将查询结果捕获为新数据集，以用于报表、数据科学工作区或将其摄取到实时客户档案中。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 计算ADLS数据集的列级统计信息 | 此 `ANALYZE TABLE` 命令已扩展 `COMPUTE STATISTICS` 和 `SHOW STATISTICS` sql命令。 您现在可以计算ADLS数据集子集或该数据集内某些列的统计信息。 有关详细信息，请阅读 [数据集统计信息计算指南](../../query-service/essential-concepts/dataset-statistics.md). |

{style="table-layout:auto"}

要了解有关查询服务的更多信息，请阅读 [查询服务概述](../../query-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Platform服务来构建、标记和增强这些数据。 您可以从多种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 扩展了对草稿模式的API支持 | 现在，在使用时，您可以在源工作流中暂停并保存进度 [!DNL Flow Service] API的任何时间。 使用 `mode=draft` 将基础、源和目标连接另存为草稿的状态。 可稍后重新访问所有草绘图元，以便完成。 阅读以下内容中的指南： [设置您的 [!DNL Flow Service] 图元到草稿状态](../../sources/tutorials/api/draft.md) 了解更多信息。 |
| 正式发布 [!DNL Salesforce Marketing Cloud] 源 | 此 [[!DNL Salesforce Marketing Cloud source] 现在为GA版](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md). 使用此源将您的 [!DNL Salesforce Marketing Cloud] Experience Platform数据。 |
| [!DNL Google Ads] 身份验证更新 | 现在，您可以在验证您的帐户时，提供登录客户ID。 [!DNL Google Ads] 从特定操作客户获取报表数据的源帐户。 阅读 [[!DNL Google Ads] 源文档](../../sources/connectors/advertising/ads.md) 了解更多信息。 |
| [!DNL Google PubSub] 身份验证更新 | 您现在可以定义访问权限 [!DNL Google PubSub] 源。 使用基于项目的身份验证允许根级别访问，或使用基于主题和订阅的身份验证限制对特定主题和订阅流的访问。 阅读 [[!DNL Google PubSub] 源文档](../../sources/connectors/cloud-storage/google-pubsub.md) 了解更多信息。 |
| 的新分页字段参数 `type=PAGE` 在自助式源(Batch SDK)中 | 您现在可以使用 `initialPageIndex` 和 `endPageIndex` 将源与集成时 `type=PAGE` 通过Batch SDK. <ul><li>`initialPageIndex`：利用此参数可定义分页开始的页码。 </li><li>`endPageIndex`：利用此参数可建立结束条件并停止分页。</li></ul> 有关这些新参数的详细信息，请参阅 [自助式源批处理SDK文档](../../sources/sources-sdk/config/sourcespec.md#page). |
| 草稿模式的UI支持 | 现在，您可以在源工作流期间通过用户界面暂停并保存进度。 您可以选择 **[!UICONTROL 另存为草稿]** 在工作流执行数据流详细信息、映射和计划步骤期间，将数据流另存为草稿以供日后完成。 阅读以下内容中的指南： [在UI中将数据流另存为草稿](../../sources/tutorials/ui/draft.md) 了解更多信息。 |

{style="table-layout:auto"}

要了解有关来源的更多信息，请阅读 [源概述](../../sources/home.md).

<!-- | API support for streaming data from a [!DNL Snowflake] database | You can now stream data from a [[!DNL Snowflake] source](../../sources/connectors/databases/snowflake.md) using the [!DNL Flow Service] API. | -->