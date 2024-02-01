---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform 的 2024 年 1 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: fc7183cbc1ca3e27999d0ddd64c83ee19ccb1200
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 38%

---

# Adobe Experience Platform 发行说明

**发行日期： 2024年1月30日**

Adobe Experience Platform中的新增功能：

- [用例行动手册](#use-case-playbooks)

对Experience Platform中现有功能的更新：

- [仪表板](#dashboards)
- [数据准备](#data-prep)
- [目标](#destinations)
- [Real-Time Customer Data Platform](#rtcdp)
- [实时客户配置文件](#profile)
- [源](#sources)

## 用例行动手册 {#use-case-playbooks}

此 [!UICONTROL 用例行动手册] 功能现已正式提供给所有Real-Time CDP和Adobe Journey Optimizer客户。 [!UICONTROL 用例行动手册] 旨在帮助用户在开始使用Real-time Customer Data Platform或Adobe Journey Optimizer时克服挑战。 当您不确定从何处开始或如何为所需的用例创建正确的资产时，用例行动手册会提供灵感并创建不同的资产，以供您在准备就绪时测试并导入生产环境。

开始使用 [!UICONTROL 用例行动手册]，请阅读以下文档页面：

- 阅读 [“概述”页面](/help/use-case-playbooks/playbooks/overview.md) 了解行动手册的用途、可用性信息，并获取关于行动手册如何工作的端到端演示，从发现到创建实例，再到将生成的资源导入其他沙盒环境。
- 获取所有内容的列表 [可用的行动手册](/help/use-case-playbooks/playbooks/playbooks-list.md)，按产品分组(Real-Time CDP或Journey Optimizer)
- 获取关于所有的信息 [所需权限](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) 使用行动手册和行动手册生成的资源。
- 了解 [数据感知功能](/help/use-case-playbooks/playbooks/data-awareness.md) 这允许您将生成的资源复制到其他沙盒环境
- Get [疑难解答提示](/help/use-case-playbooks/playbooks/troubleshooting.md) 如果您在使用用例行动手册时遇到错误或困难。

## 数据准备 {#data-prep}

通过数据准备，数据工程师可从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 新的映射器函数 | <ul><li>`object_to_map`：使用 `object_to_map` 函数来创建映射数据类型。 此函数支持多种不同的语法。 有关详细信息，请阅读上的指南 [层次结构的函数 — 对象](../../data-prep/functions.md#objects). </li><li>`to_map`：使用 `to_map` 函数创建具有给定字段名和值对的映射。 有关详细信息，请阅读上的指南 [层次函数 — 映射](../../data-prep/functions.md#map). </li><li>`array_to_map`：使用 `array_to_map` 函数来创建具有给定字段名和值对的映射。 有关详细信息，请阅读上的指南 [层次函数 — 映射](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

有关数据准备的详细信息，请阅读 [数据准备概述](../../data-prep/home.md).

## 仪表板 {#dashboards}

Adobe Experience Platform 提供多个仪表板，通过这些仪表板，可查看在每天保存快照期间捕获的关于您组织的数据的重要见解。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 查看SQL | 您现在可以查看配置文件、受众、目标和自定义分析背后的SQL，然后通过查询编辑器按需执行查询。 从SQL中获取40多种现有见解作为灵感，以创建新查询，这些查询可根据您的业务需求从Platform数据获取独特的见解。 有关详细信息，请阅读上的指南 [查看分析SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义构件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新目标**{#new-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [公共连接](../../destinations/catalog/advertising/pubmatic.md) | 使用此目标可将受众数据发送到 [!DNL PubMatic Connect] 平台。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 新建 **假定的角色** Amazon S3目标的身份验证类型 | 如果您不想与Experience Platform共享帐户密钥和密钥，请在将Experience Platform连接到Amazon S3存储桶时使用新的假定角色身份验证类型。 有关新的身份验证方法的更多信息，请参阅 [身份验证部分](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) Amazon S3文档的URL名称。 |

{style="table-layout:auto"}

有关目标的更多一般信息，请参阅[目标概览](../../destinations/home.md)。

## Real-Time Customer Data Platform {#rtcdp}

建立在 Experience Platform 上的 Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 可以帮助公司汇集已知和未知数据，通过整个客户历程中通过智能决策激活客户配置文件。[!DNL Real-Time CDP] 结合多个企业数据源来实时创建客户配置文件。然后，根据这些配置文件构建的区段可以发送到下游目标，以便跨所有渠道和设备提供一对一的个性化客户体验。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 的更新 [Real-Time CDP主页](https://experience.adobe.com) | <ul><li>**配置文件小组件**：您现在可以使用配置文件小组件导航到配置文件概述页面，并查看贵组织的配置文件量度。</li><li>**配置文件量度卡片**：主页仪表板中的配置文件量度卡现在显示组织中的配置文件总数，具体取决于您各自的合并策略。</li><li>**架构小组件**：您现在可以使用架构构件导航到UI中的架构创建工作流。</li></ul> |

要进一步了解Real-Time CDP，请阅读 [Real-Time CDP概述](../../rtcdp/overview.md).

## 实时客户配置文件 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户配置文件，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。配置文件允许您将客户数据整合到一个统一视图中，并为每一次客户交互提供可操作的、有时间戳的描述。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 改进了配置文件查看器的默认仪表板卡片的本地化功能 | 默认个人资料卡现在将具有动态本地化的名称。 自定义个人资料卡可以继续具有可以编辑的自定义名称。 |

{style="table-layout:auto"}

要了解有关Real-time Customer Profile的更多信息，请参阅 [配置文件概述](../../profile/home.md)

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL Oracle NetSuite] 源 | 使用 [!DNL Oracle NetSuite] 源目录中的集成，可从 [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) 和 [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) 要Experience Platform的帐户。 |
| [!BADGE Beta]{type=Informative}[!DNL Braze Currents] 源 | 使用 [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) 集成到源目录中，以从您的目录中 [!DNL Braze] 帐户到Experience Platform。 |
| 支持以下项的密钥对身份验证 [!DNL Snowflake] 批次源 | 现在，您可以在创建新时使用密钥对身份验证 [!DNL Snowflake] 批处理数据的帐户。 有关详细信息，请阅读上的指南 [创建 [!DNL Snowflake] 使用API的帐户](../../sources/tutorials/api/create/databases/snowflake.md) 或上的指南 [创建 [!DNL Snowflake] 使用UI的帐户](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

若要了解有关源的更多信息，请阅读[源概述](../../sources/home.md)。