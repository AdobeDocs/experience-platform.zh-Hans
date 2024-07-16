---
title: Adobe Experience Platform 发行说明（2024 年 1 月）
description: Adobe Experience Platform 的 2024 年 1 月发行说明。
exl-id: d4b3c5b2-3adb-41fd-91ad-f4c0f21d2325
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 39%

---

# Adobe Experience Platform 发行说明

**发行日期： 2024年1月30日**

Adobe Experience Platform中的新增功能：

- [用例战术手册](#use-case-playbooks)

对Experience Platform中现有功能的更新：

- [基于属性的访问控制](#abac)
- [数据准备](#data-prep)
- [仪表板](#dashboards)
- [目标](#destinations)
- [身份服务](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [实时客户配置文件](#profile)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 用例战术手册 {#use-case-playbooks}

[!UICONTROL 用例行动手册]功能现在普遍适用于所有Real-Time CDP和Adobe Journey Optimizer客户。 [!UICONTROL 用例行动手册]旨在帮助用户在开始使用Real-time Customer Data Platform或Adobe Journey Optimizer时克服挑战。 当您不确定从何处开始或如何为所需的用例创建正确的资产时，用例行动手册会提供灵感并创建不同的资产，以供您在准备就绪时测试并导入生产环境。

要开始使用[!UICONTROL 用例行动手册]，请阅读以下文档页面：

- 阅读[概述页面](/help/use-case-playbooks/playbooks/overview.md)以了解用途、可用性信息，并获取行动手册如何工作的端到端演示，从发现到创建实例，再到将生成的资源导入其他沙盒环境。
- 获取按产品(Real-Time CDP或Journey Optimizer)分组的所有[可用行动手册](/help/use-case-playbooks/playbooks/playbooks-list.md)的列表
- 获取有关使用行动手册和行动手册生成的资产的所有[所需权限](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions)的信息。
- 了解[数据感知功能](/help/use-case-playbooks/playbooks/data-awareness.md)，它允许您将生成的资产复制到其他沙盒环境
- 如果您在使用用例行动手册时遇到错误或困难，请获取[疑难解答提示](/help/use-case-playbooks/playbooks/troubleshooting.md)。

## 基于属性的访问控制 {#abac}

基于属性的访问控制是 Adob&#x200B;&#x200B;e Experience Platform 的一项功能，它为注重隐私的品牌在管理用户访问权限方面提供了更大的灵活性。可以将架构字段和区段等单个对象分配给用户角色。此功能允许您授予或撤销组织中特定 Platform 用户对各个对象的访问权限。

通过基于属性的访问控制，您组织的管理员可以控制用户对所有 Platform 工作流程和资源中的敏感个人数据 (SPD)、个人身份信息 (PII) 和其他自定义类型数据的访问。管理员可以定义只能访问特定字段以及与这些字段对应的数据的用户角色。

**新文档或更新文档**

| 文档更新 | 描述 |
| --- | --- |
| 为基于属性的访问控制记录了新的API端点 | [访问控制API参考文档](https://developer.adobe.com/experience-platform-apis/references/access-control/)现在包含基于属性的访问控制API角色、策略和产品端点。 这些端点可用于检索指定沙盒中给定资源上用户的相关角色、策略和产品。 |

{style="table-layout:auto"}

有关基于属性的访问控制的详细信息，请参阅[基于属性的访问控制概述](../../access-control/abac/overview.md)。有关基于属性的访问控制工作流程的综合指南，请阅读[基于属性的访问控制端到端指南](../../access-control/abac/end-to-end-guide.md)。

## 数据准备 {#data-prep}

通过数据准备，数据工程师可从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 新的映射器函数 | <ul><li>`object_to_map`：使用`object_to_map`函数创建映射数据类型。 此函数支持多种不同的语法。 有关详细信息，请阅读有关层次结构 — 对象](../../data-prep/functions.md#objects)的[函数的指南。 </li><li>`to_map`：使用`to_map`函数创建映射，并使用对象指定字段名和值对。 有关详细信息，请阅读有关层次结构 — 映射](../../data-prep/functions.md#map)的[函数的指南。 </li><li>`array_to_map`：使用`array_to_map`函数创建映射，并使用对象数组指定字段名和值对。 有关详细信息，请阅读有关层次结构 — 映射](../../data-prep/functions.md#map)的[函数的指南。 |

{style="table-layout:auto"}

有关数据准备的更多信息，请阅读[数据准备概述](../../data-prep/home.md)。

## 仪表板 {#dashboards}

Adobe Experience Platform 提供多个仪表板，通过这些仪表板，可查看在每天保存快照期间捕获的关于您组织的数据的重要见解。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 查看 SQL | 您现在可以使用“查看SQL”切换来查看“用户档案”、“受众”、“目标”和自定义分析后面的SQL，然后通过查询编辑器按需执行查询。 访问支持Real-time Customer Data Platform分析的SQL可帮助您了解数据模型分析背后的逻辑。 这种透明度使您的AdobeReal-time CDP数据更易于访问、理解并影响决策。<br>从SQL中获取40多种现有见解作为灵感，以创建新的查询，这些查询可根据您的业务需求从Platform数据中获取独特的见解。 Experience League文档中的SQL还可用于您的[配置文件](../../dashboards/insights/profiles.md)、[受众](../../dashboards/insights/audiences.md)和[目标](../../dashboards/insights/destinations.md)分析。 这些文件突出显示可使用标准见解解答的业务用例。 有关详细信息，请参阅[查看分析SQL](../../dashboards/view-sql.md)指南。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义构件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新目标**{#new-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [公用连接](../../destinations/catalog/advertising/pubmatic.md) | 使用此目标将受众数据发送到[!DNL PubMatic Connect]平台。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 为Amazon S3目标新建&#x200B;**承担角色**&#x200B;身份验证类型 | 如果您不想与Experience Platform共享帐户密钥和密钥，请在将Experience Platform连接到Amazon S3存储桶时使用新的假定角色身份验证类型。 有关新的身份验证方法的更多信息，请参阅Amazon S3文档的[身份验证部分](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication)。 |

{style="table-layout:auto"}

有关目标的更多一般信息，请参阅[目标概览](../../destinations/home.md)。

## 身份服务 {#identity-service}

Adobe Experience Platform 身份服务通过跨设备和系统桥接身份，使您能够全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。

**新文档或更新文档**

| 文档更新 | 描述 |
| --- | --- |
| 文档重组 | Identity Service文档进行了重组，以改进Identity Service中概念的呈现和清晰性：<ul><li>访问[Identity Service概述页面](../../identity-service/home.md)，了解扩展的术语指南、详细说明典型客户历程的用例示例、Identity Service如何将身份链接在一起的细分以及Identity Service在Experience Platform生态系统中所扮演角色的摘要。</li><li>请阅读有关[的指南，了解Identity Service与Real-time Customer Profile](../../identity-service/identity-and-profile.md)之间的关系，详细了解这两种服务如何协作以及它们的目的、流程、输入和输出之间的差异。</li><li>请参阅[Identity Service链接逻辑指南](../../identity-service/features/identity-linking-logic.md)，以解释和可视化身份图在给定不同方案和时间戳时的行为方式。</li></ul> |

{style="table-layout:auto"}

若要了解有关Identity Service的更多信息，请阅读[Identity Service概述](../../identity-service/home.md)。

## Real-Time Customer Data Platform {#rtcdp}

建立在 Experience Platform 上的 Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 可以帮助公司汇集已知和未知数据，通过整个客户历程中通过智能决策激活客户配置文件。[!DNL Real-Time CDP] 结合多个企业数据源来实时创建客户配置文件。然后，根据这些配置文件构建的区段可以发送到下游目标，以便跨所有渠道和设备提供一对一的个性化客户体验。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [Real-Time CDP主页](https://experience.adobe.com)的更新 | <ul><li>**配置文件小组件**：您现在可以使用配置文件小组件导航到配置文件概述页面并查看您组织的配置文件量度。</li><li>**配置文件量度卡**：主页仪表板中的配置文件量度卡现在显示您组织中的配置文件总数，具体取决于您各自的合并策略。</li><li>**架构小组件**：您现在可以使用架构小组件导航到UI中的架构创建工作流。</li></ul> |

{style="table-layout:auto"}

**新文档或更新文档**

| 文档更新 | 描述 |
| --- | --- |
| 新的Real-Time CDP文档主页 | 访问[新的Real-Time CDP文档主页](/help/rtcdp/home.md)，概览有关如何开始使用产品、护栏、示例用例等的信息。 |
| 示例Real-Time CDP用例概述 | 访问[新示例用例概述页面](/help/rtcdp/use-case-guides/overview.md)，查看您的组织可以使用Real-Time CDP实现的示例用例集合。 |

{style="table-layout:auto"}

要了解有关Real-Time CDP的更多信息，请阅读[Real-Time CDP概述](../../rtcdp/overview.md)。

## 实时客户配置文件 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户配置文件，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。配置文件允许您将客户数据整合到一个统一视图中，并为每一次客户交互提供可操作的、有时间戳的描述。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 改进了配置文件查看器的默认仪表板卡片的本地化功能 | 默认个人资料卡现在将具有动态本地化的名称。 自定义个人资料卡可以继续具有可以编辑的自定义名称。 |

{style="table-layout:auto"}

若要了解有关实时客户个人资料的更多信息，请阅读[个人资料概述](../../profile/home.md)

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的配置文件子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 外部生成的受众上传 | 最大列数已增加到&#x200B;**25**。 |
| 区段生成器评估 | 预计值和符合条件的用户档案现在显示在受众属性部分中。 有关此更改的更多信息，请阅读[区段生成器UI指南](../../segmentation/ui/segment-builder.md)。 |

{style="table-layout:auto"}

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informational} [!DNL Oracle NetSuite]源 | 使用源目录中的[!DNL Oracle NetSuite]集成将来自[[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md)和[[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md)帐户的数据引入Experience Platform。 |
| [!BADGE Beta]{type=Informational} [!DNL Braze Currents]源 | 使用源目录中的[[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md)集成将[!DNL Braze]帐户中的数据导入Experience Platform。 |
| 支持[!DNL Snowflake]批次源的密钥对身份验证 | 在为批次数据创建新的[!DNL Snowflake]帐户时，您现在可以使用密钥对身份验证。 有关详细信息，请阅读[使用API创建 [!DNL Snowflake] 帐户的指南](../../sources/tutorials/api/create/databases/snowflake.md)或[使用UI创建 [!DNL Snowflake] 帐户的指南](../../sources/tutorials/ui/create/databases/snowflake.md)。 |

{style="table-layout:auto"}

若要了解有关源的更多信息，请阅读[源概述](../../sources/home.md)。
