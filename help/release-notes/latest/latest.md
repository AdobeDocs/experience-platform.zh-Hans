---
title: Adobe Experience Platform发行说明2024年6月
description: Adobe Experience Platform 的 2024 年 6 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: af27ca20b7d611bb6f6b13b57dfc2df1f643a0b6
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 18%

---

# Adobe Experience Platform 发行说明

**发布日期： 2024年6月18日**

>[!TIP]
>
>[Experience Platform中的AI助手](https://platform.adobe.com) 现已推出。 使用AI Assistant加速Adobe应用程序中的工作流。 [了解更多](#ai-assistant) 关于新功能。

Adobe Experience Platform中的新增功能：

- [AI 助手](#ai-assistant)
- [Experience Platform API 身份验证](#authentication-platform-apis)
- [数据准备](#data-prep)
- [目标](#destinations)
- [身份服务](#identity-service)
- [Privacy Service](#privacy)
- [Segmentation Service](#segmentation)
- [用例战术手册](#use-case-playbooks)

## AI 助手 {#ai-assistant}

Adobe Experience Platform中的AI助手是一种对话体验，可用于加快Adobe应用程序中的工作流程。 您可以使用AI Assistant更好地了解产品知识、排除问题或搜索信息并查找运营见解。 AI Assistant支持Experience Platform、Real-time Customer Data Platform、Adobe Journey Optimizer和Customer Journey Analytics。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| Experience Platform中的AI助手 | 您现在可以在Experience Platform中使用AI助手。 AI Assistant支持Experience Platform、Real-time Customer Data Platform、Adobe Journey Optimizer和Customer Journey Analytics。 <br> ![Experience Platform中的AI助手。](../2024/assets/june/ai-assistant-full.png "Experience Platform中的AI助手。"){width="100" zoomable="yes"} <br> 有关此功能的详细信息，请参阅 [AI助手UI指南](../../ai-assistant/ui-guide.md). |
| 支持产品知识问题 | [产品知识](../../ai-assistant/home.md#product-knowledge) 是以Experience League文档为基础的概念和主题，可用于有针对性的学习、开放式发现和故障排除。 您可以询问AI Assistant产品知识问题，例如： <ul><li>哪些受众具有相似性？</li><li>如何计算配置文件丰富度？</li><li> 能否在摄取数据后删除启用配置文件的架构？</li></ul> |
| [!BADGE 测试版]{type=Informative}支持操作分析问题 | [运营见解](../../ai-assistant/home.md#operational-insights) 是AI Assistant生成的有关您的元数据对象的答案，包括计数、查找和谱系影响。 操作分析不会查看沙盒中的任何数据。 您可以询问AI Assistant操作见解问题，例如： <ul><li>哪些目标处于活动状态？</li><li>我有多少个数据集？</li><li>列出实时历程中使用的受众。</li></ul> 以下域支持运营分析：属性、受众、数据流、数据集、目标、历程、架构和源。 |
| 访问AI助手 | 要访问用于Experience Platform、Real-Time CDP和Journey Optimizer的AI助手，必须将您添加到角色中，该角色包括 **启用AI助手** 和 **查看运营分析** 权限。 欲知更多信息，请参阅 [功能访问指南](../../ai-assistant/access.md). 您必须将Admin Console用于 [在Customer Journey Analytics中访问](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant?lang=en#feature-access). |

有关AI Assistant的详细信息，请阅读 [AI Assistant概述](../../ai-assistant/home.md).

## Experience Platform API 身份验证 {#authentication-platform-apis}

用于获取访问令牌的JWT方法现在因新集成而被弃用，并替换为更简单的OAuth服务器到服务器身份验证方法。<p>![突出显示用于获取访问令牌的新 OAuth 身份验证方法。](/help/landing/images/api-authentication/oauth-authentication-method.png "突出显示用于获取访问令牌的新 OAuth 身份验证方法。"){width="100" zoomable="yes"}</p>

虽然现有使用 JWT 身份验证方法的 API 集成将继续有效直至 2025 年 1 月 1 日，但 Adobe 强烈建议您在该日期之前将现有的集成迁移到新的 OAuth 服务器到服务器方法。阅读有关[从服务帐户 (JWT) 凭据迁移到 OAuth 服务器到服务器凭据](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)的指南。

## 数据准备 {#data-prep}

使用数据准备来映射、转换和验证往来于Experience Data Model (XDM)的数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 保留关键字列表的添加 | 以下词已添加到数据准备保留关键字列表：<ul><li>`do`</li><li>`empty`</li><li>`function`</li><li>`size`</li></ul> 欲了解更多信息，请阅读 [数据准备函数指南](../../data-prep/functions.md). |

{style="table-layout:auto"}

有关数据准备的详细信息，请阅读 [数据准备概述](../../data-prep/home.md).

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 增强了用于导出外部受众的临时导出API | 您现在可以使用临时导出API来导出外部（自定义上传）受众。 [了解更多](/help/destinations/api/ad-hoc-activation-api.md) . |
| (Beta)在导出阵列支持的测试阶段还支持其他功能 | 以前，将受众激活到基于文件的目标并选择使用计算字段时，您只能使用通过数据准备提供的受众子集。 这一限制现已解除，在将受众导出到基于文件的目标时，客户可以访问数据准备提供的所有功能。 [了解详情](/help/destinations/ui/export-arrays-calculated-fields.md#supported-functions)。 |
| 仅显示映射步骤中包含数据的字段 | 将配置文件属性映射到目标时，您现在可以在所有配置文件属性之间切换，或者仅切换包含数据的配置文件属性。 默认情况下，仅显示包含数据的字段。 请参阅激活指南，了解 [批次](../../destinations/ui/activate-batch-profile-destinations.md#mapping) 和 [流式](../../destinations/ui/activate-segment-streaming-destinations.md#mapping) 目标，以了解更多详细信息。 |

{style="table-layout:auto"}

有关目标的更多一般信息，请参阅[目标概览](../../destinations/home.md)。

## 身份服务 {#identity-service}

使用Adobe Experience Platform Identity Service跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，从而全面了解客户及其行为。

**即将推出的功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE 测试版]{type=Informational}标识图链接规则 | Beta计划的参与者可以使用标识图链接规则来通过防止“共享设备”和其他图形折叠场景来确保系统中人员实体的表示方式。 为实现此目标，Beta版计划中的参与者将有权访问开发沙盒环境中的三项功能： <ul><li>图形模拟工具，用于了解图形算法的运行方式。</li><li>身份设置屏幕，用于配置唯一的命名空间和命名空间优先级。</li><li>用于深入了解所摄取图形的身份仪表板。</li></ul> 此外，Beta版计划还包括配置文件行为稳定性的改进。 欲知更多信息，请参阅 [身份图链接规则](../../identity-service/identity-graph-linking-rules/overview.md) 文档。 |

{style="table-layout:auto"}

有关Identity Service的详细信息，请阅读 [Identity服务概述](../../identity-service/home.md).

## [!DNL Privacy Service] {#privacy}

根据几项法律和组织法规，用户有权应请求从您的数据存储中访问或删除其个人数据。 Adobe Experience Platform [!DNL Privacy Service] 提供了RESTful API和用户界面，帮助您管理来自客户的这些数据请求。 替换为 [!DNL Privacy Service]，您可以提交从Adobe Experience Cloud应用程序访问和删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
|--- | ---|
| Adobe Journey Optimizer的Privacy Service支持 | Privacy Service功能现在与Adobe Journey Optimizer协议兼容，可用于处理删除请求。 请参阅 [Adobe Journey Optimizer隐私请求文档](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/requests) 有关详细信息，请参阅此Experience Platform文档，其中列出了 [Experience Cloud与Privacy Service集成的应用程序](../../privacy-service/experience-cloud-apps.md). |

请参阅 [Privacy Service概述](../../privacy-service/home.md) 以了解有关该服务的更多信息。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的配置文件子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 时间限制更新 | “本月”和“今年”的行为已更新，它们现在分别表示“月至今”和“年初至今”。 有关此更改的详细信息，请阅读 [区段生成器指南](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## 用例战术手册 {#use-case-playbooks}

[!DNL Use Case Playbooks] 所有Adobe Experience Platform客户均可免费使用。 要在Experience PlatformUI中访问丰富的用例行动手册，您现在可以选择 **[!UICONTROL 行动手册]** 从左侧导航栏中。

[!DNL Use Case Playbooks] 旨在帮助克服在开始使用Real-time Customer Data Platform或Adobe Journey Optimizer时遇到的挑战。 它们提供了指南，可生成各种资源，您可以在准备就绪时测试并导入生产环境，即使您不确定从何处开始或者如何为预期用例生成正确的资源。

要开始使用，请阅读 [用例行动手册概述](/help/use-case-playbooks/playbooks/overview.md)，概述了行动手册的功能、用途和端到端演示，包括如何创建实例并将生成的资源导入其他沙盒环境中。

要了解如何访问和设置富有启发的沙盒以试验并探索各种用例行动手册，请参阅 [导航到用例行动手册](/help/use-case-playbooks/playbooks/navigate.md) 文档。

要了解有关 [!DNL Use Case Playbooks]，请阅读以下文档页面：

- 获取全部列表 [可用的行动手册](/help/use-case-playbooks/playbooks/playbooks-list.md)，按产品分组(Real-Time CDP或Journey Optimizer)。
- 了解内容 [权限](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) 是您使用行动手册及其创建的资源所必需的。
- 了解 [数据感知功能](/help/use-case-playbooks/playbooks/data-awareness.md) 这允许您将生成的资源复制到其他沙盒环境。
