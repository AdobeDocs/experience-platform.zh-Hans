---
title: Adobe Experience Platform 发行说明（2024 年 1 月）
description: Adobe Experience Platform 的 2024 年 1 月发行说明。
exl-id: d4b3c5b2-3adb-41fd-91ad-f4c0f21d2325
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: ht
source-wordcount: '1662'
ht-degree: 100%

---

# Adobe Experience Platform 发行说明

**发布日期：2024 年 1 月 30 日**

Adobe Experience Platform 的新功能：

- [用例战术手册](#use-case-playbooks)

Experience Platform 中现有功能的更新：

- [基于属性的访问控制](#abac)
- [数据准备](#data-prep)
- [仪表板](#dashboards)
- [目标](#destinations)
- [身份标识服务](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [实时客户轮廓](#profile)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 用例战术手册 {#use-case-playbooks}

 [!UICONTROL 用例战术手册] 功能现已面向所有 Real-Time CDP 和 Adobe Journey Optimizer 客户开放。[!UICONTROL 用例战术手册] 旨在帮助用户克服使用 Real-Time Customer Data Platform 或 Adobe Journey Optimizer 时遇到的挑战。当您不确定从哪里开始或如何为所需用例创建正确的资产时，用例战术手册可以提供灵感，创建不同的资产供您测试，并在准备就绪时导入到生产环境中。

要开始使用 [!UICONTROL 用例战术手册]，请阅读以下文档页面：

- 阅读[概述页面](/help/use-case-playbooks/playbooks/overview.md)以了解目的、可用性信息，并获得战术手册如何从发现到创建实例，再到将生成的资产导入其他沙盒环境的端到端演示。
- 获取所有[可用战术手册](/help/use-case-playbooks/playbooks/playbooks-list.md)的列表，按产品分组（Real-Time CDP 或 Journey Optimizer）
- 获取有关使用战术手册的所有[所需权限](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions)以及战术手册生成的资产的信息。
- 了解[数据感知功能](/help/use-case-playbooks/playbooks/data-awareness.md)，该功能可让您将生成的资产复制到其他沙盒环境
- 如果您在使用用例战术手册时遇到错误或困难，请获取[故障排除提示](/help/use-case-playbooks/playbooks/troubleshooting.md) 。

## 基于属性的访问控制 {#abac}

基于属性的访问控制是 Adob&#x200B;&#x200B;e Experience Platform 的一项功能，它为注重隐私的品牌在管理用户访问权限方面提供了更大的灵活性。可以将架构字段和区段等单个对象分配给用户角色。此功能允许您授予或撤销组织中特定 Experience Platform 用户对各个对象的访问权限。

通过基于属性的访问控制，您组织的管理员可以控制用户对所有 Experience Platform 工作流和资源中的敏感个人数据（SPD）、个人身份信息（PII）和其他自定义类型数据的访问。管理员可以定义只能访问特定字段以及与这些字段对应的数据的用户角色。

**新增或更新文档**

| 文档更新 | 描述 |
| --- | --- |
| 记录了基于属性的访问控制的新 API 端点 |  [Access Control API 参考文档](https://developer.adobe.com/experience-platform-apis/references/access-control/)现在包括基于属性的访问控制 API 角色、策略和产品端点。这些端点可用于检索指定沙盒中给定资源上用户的相关角色、策略和产品。 |

{style="table-layout:auto"}

有关基于属性的访问控制的详细信息，请参阅[基于属性的访问控制概述](../../access-control/abac/overview.md)。有关基于属性的访问控制工作流的综合指南，请阅读[基于属性的访问控制端到端指南](../../access-control/abac/end-to-end-guide.md)。

## 数据准备 {#data-prep}

通过数据准备，数据工程师可从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 新的映射器函数 | <ul><li>`object_to_map`：使用 `object_to_map` 函数创建映射数据类型。该函数支持几种不同的语法。欲了解更多信息，请阅读[层次结构函数 - 对象](../../data-prep/functions.md#objects)指南。 </li><li>`to_map`：使用 `to_map` 函数使用对象创建具有给定字段名称和值对的映射。欲了解更多信息，请阅读[层次结构函数 - 映射](../../data-prep/functions.md#map)指南。 </li><li>`array_to_map`：使用 `array_to_map` 函数使用对象数组创建具有给定字段名称和值对的映射。欲了解更多信息，请阅读[层次结构函数 - 映射](../../data-prep/functions.md#map)指南。 |

{style="table-layout:auto"}

有关数据准备的详细信息，请参阅[数据准备概述](../../data-prep/home.md)。

## 仪表板 {#dashboards}

Adobe Experience Platform 提供多个仪表板，通过这些仪表板，可查看在每天保存快照期间捕获的关于您组织的数据的重要见解。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 查看 SQL | 您现在可以使用查看 SQL 切换按钮查看轮廓、受众、目标和自定义洞察背后的 SQL，然后通过查询编辑器按需执行查询。访问支持 Real-time Customer Data Platform 洞察的 SQL 有助于您了解数据模型分析背后的逻辑。这种透明度使您的 Adobe Real-time CDP 数据更易于访问、理解，并且对决策更具影响力。<br>从超过 40 个现有洞察的 SQL 中获取灵感，创建新的查询，根据您的业务需求从 Experience Platform 数据中获取独特的洞察。该 SQL 还适用于 Experience League 文档中的[轮廓](../../dashboards/insights/profiles.md)、[受众](../../dashboards/insights/audiences.md)和[目标](../../dashboards/insights/destinations.md)洞察。这些文档重点介绍了可以用标准洞察回答的业务用例。如需了解更多信息，请阅读[查看洞察 SQL](../../dashboards/view-sql.md) 指南。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义小组件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新目标**{#new-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [公共连接](../../destinations/catalog/advertising/pubmatic.md) | 使用此目标将受众数据发送到 [!DNL PubMatic Connect] 平台。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 适用于 Amazon S3 目标的新&#x200B;**承担角色**&#x200B;身份验证类型 | 如果您不想与 Experience Platform 共享帐户密钥和私钥，请在将 Experience Platform 连接到 Amazon S3 存储桶时使用新的承担角色身份验证类型。请参阅 Amazon S3 文档的[身份验证部分](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication)，了解有关新身份验证方法的更多信息。 |

{style="table-layout:auto"}

有关目标的更多一般信息，请参阅[目标概述](../../destinations/home.md)。

## 身份标识服务 {#identity-service}

Adobe Experience Platform 身份标识服务通过跨设备和系统桥接身份标识，使您能够全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。

**新增或更新文档**

| 文档更新 | 描述 |
| --- | --- |
| 文档重组 | 身份标识服务文档已重组，以改善身份标识服务中概念的呈现和清晰度：<ul><li>访问[身份标识服务概述页面](../../identity-service/home.md)，获取详细的术语指南、详细介绍典型客户历程的用例示例、身份标识服务如何将身份标识链接在一起的细分，以及身份标识服务在 Experience Platform 生态系统中所扮演的角色的摘要。</li><li>参阅[了解身份标识服务和实时客户轮廓之间的关系](../../identity-service/identity-and-profile.md)指南，详细了解这两种服务如何协同工作，以及它们的目的、流程、输入和输出之间的差异。</li><li>请参阅[身份标识服务链接逻辑指南](../../identity-service/features/identity-linking-logic.md)，了解身份标识图在不同场景和时间戳下的行为方式的解释和可视化。</li></ul> |

{style="table-layout:auto"}

要了解有关身份标识服务的更多信息，请阅读[身份标识服务概述](../../identity-service/home.md)。

## Real-Time Customer Data Platform {#rtcdp}

建立在 Experience Platform 上的 Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 可以帮助公司汇集已知和未知数据，通过整个客户历程中通过智能决策激活客户轮廓。[!DNL Real-Time CDP] 结合多个企业数据源来实时创建客户轮廓。然后，根据这些轮廓构建的区段可以发送到下游目标，以便跨所有渠道和设备提供一对一的个性化客户体验。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 更新 [Real-Time CDP 主页](https://experience.adobe.com) | <ul><li>**轮廓小组件**：您现在可以使用轮廓小组件导航到轮廓概览页面并查看组织的轮廓指标。</li><li>**轮廓量度卡**：主页仪表板中的轮廓量度卡现在显示您组织中的轮廓总数，具体取决于您各自的合并策略。</li><li>**架构小组件**：您现在可以使用架构小组件导航到 UI 中的架构创建工作流程。</li></ul> |

{style="table-layout:auto"}

**新增或更新文档**

| 文档更新 | 描述 |
| --- | --- |
| 新的 Real-Time CDP 文档主页 | 访问[新的 Real-Time CDP 文档主页](/help/rtcdp/home.md)，了解有关如何开始使用产品、护栏、示例用例等的概览信息。 |
| Real-Time CDP 示例用例概述 | 访问[新示例用例概述页面](/help/rtcdp/use-case-guides/overview.md)，了解您的组织可以使用 Real-Time CDP 实现的一系列示例用例。 |

{style="table-layout:auto"}

要了解有关 Real-Time CDP 的更多信息，请阅读 [Real-Time CDP 概述](../../rtcdp/overview.md)。

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户轮廓，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。轮廓允许您将客户数据整合到一个统一视图中，并为每一次客户交互提供可操作的、有时间戳的描述。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 改进了轮廓查看器的默认仪表板卡的本地化 | 默认的轮廓卡现在将具有动态本地化的名称。自定义轮廓卡可以继续拥有可编辑的自定义名称。 |

{style="table-layout:auto"}

要了解有关实时客户轮廓的更多信息，请阅读[轮廓概述](../../profile/home.md)

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 外部生成的受众上传 | 最大列数已增加至 **25**。 |
| 区段生成器估计 | 估计和合格的轮廓现在显示在受众属性部分中。有关此更改的更多信息，请阅读[区段生成器 UI 指南](../../segmentation/ui/segment-builder.md)。 |

{style="table-layout:auto"}

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Oracle NetSuite] 源 | 使用源目录中的 [!DNL Oracle NetSuite] 集成将 [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) 和 [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) 帐户中的数据带到 Experience Platform。 |
| [!BADGE Beta]{type=Informative} [!DNL Braze Currents] 源 | 使用源目录中的 [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) 集成将 [!DNL Braze] 帐户中的数据带到 Experience Platform。 |
| 支持密钥对身份验证 [!DNL Snowflake] 批次源 | 您现在可以在创建新的 [!DNL Snowflake] 批次数据帐户。欲了解更多信息，请阅读[创建一个 [!DNL Snowflake] 使用API 的帐户](../../sources/tutorials/api/create/databases/snowflake.md)或[创建一个 [!DNL Snowflake] 使用 UI 的帐户](../../sources/tutorials/ui/create/databases/snowflake.md)指南。 |

{style="table-layout:auto"}

若要了解有关源的更多信息，请阅读[源概述](../../sources/home.md)。
