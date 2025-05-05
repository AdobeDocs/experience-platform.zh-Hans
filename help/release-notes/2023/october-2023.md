---
title: Adobe Experience Platform 发行说明（2023 年 10 月）
description: Adobe Experience Platform 的 2023 年 10 月发行说明。
exl-id: e9cf5299-8350-4b40-8f56-05e598846875
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 37%

---

# Adobe Experience Platform 发行说明

**发行日期： 2023年10月25日**

Experience Platform 中现有功能的更新：

- [仪表板](#dashboards)
- [数据收集](#data-collection)
- [目标](#destinations)
- [沙盒](#sandboxes)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 仪表板 {#dashboards}

Adobe Experience Platform 提供多个仪表板，通过这些仪表板，可查看在每天保存快照期间捕获的关于您组织的数据的重要见解。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 目标使用情况量度 | 新的计数指标已添加到许可证使用情况仪表板。 **[!UICONTROL Audience Activation Size]**&#x200B;和&#x200B;**[!UICONTROL Data Export Size]**&#x200B;量度提供了一种方便的方法来跟踪您已从Experience Platform导出多少数据以及您的许可证使用授权。 有关这些量度和其他许可证使用量度的说明，请参阅[可用量度](../../dashboards/guides/license-usage.md#available-metrics)文档。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义小组件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 扩展 | [!DNL Meta]转化API增强 | [Meta Conversions API](/help/tags/extensions/server/meta/overview.md)扩展有三个增强功能： <ul><li>与[[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe)集成：通过允许您共享您的像素ID并访问与Adobe的转化API集成的令牌，创建无缝登录体验。</li><li>与[[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq)集成：允许您向更有可能完成所需操作的人员投放广告，并将操作链接回所投放的广告。</li><li>与[[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha)集成：允许您在CIP字段中传递LiveRamp的RampID，而无需直接与合作伙伴或Meta共享PII。 </li></ul> |
| 扩展 | [!DNL LinkedIn]转化API | [[!DNL LinkedIn] 转化API](../../tags/extensions/server/linkedin/overview.md)扩展允许您通过将Experience Platform事件数据转发到LinkedIn来评估LinkedIn营销活动的有效性。 |
| 机密 | [!DNL LinkedIn] OAuth 2密码 | [[!DNL LinkedIn] OAuth 2密钥](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2)允许您在事件转发中将服务器与服务器的交互发送到[!DNL LinkedIn]。 |
| 事件转发 | 标记和事件转发的更新 | 为了在Experience Platform中保留[标记](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=zh-Hans)和[事件转发](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=zh-Hans)性能，将仅保留最近成功和不成功的开发和暂存构建。 将删除所有不再使用的内部版本。 此外，还实施了限制和速率限制以确保一些较重的API使用不会降低其他应用程序的API性能。 |
| 扩展 | 元素、规则和扩展 | [元素、规则和扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html?lang=zh-Hans)现在在库输出中排序，以确保同一库的多个生成和部署之间更加一致。 |

有关数据收集的更多信息，请参阅[数据收集概述](../../tags/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新目标**{#new-updated-destinations}

| 目标 | 新增还是更新 | 描述 |
| ----------- |----------------|----------- |
| [[!DNL MoEngage]](/help/destinations/catalog/mobile-engagement/moengage.md) | 新增 | 使用Moengage目标实时将Adobe数据（用户属性、区段和事件）连接并映射到MoEngage。 然后，客户可以根据这些数据采取行动，提供个性化、有针对性的体验。 |
| [[!DNL Qualtrics Automations]](/help/destinations/catalog/survey/qualtrics-automations.md) | 新增 | 在Adobe Experience Platform中将多个运营数据源的聚合用作Qualtrics Experience ID中的一项输入，以便更好地了解您的客户并实现有针对性的外联，从而在了解意图、情绪和体验驱动因素方面缩小差距。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| (Beta)计算字段中支持哈希函数 | 除了特定于[导出数组](../../destinations/ui/export-arrays-maps-objects.md)或数组中的元素的函数之外，您现在还可以使用其他[散列函数](../../destinations/ui/export-arrays-maps-objects.md#hashing-functions)对导出文件中的散列属性进行散列处理。 支持的哈希函数为： `sha`、`sha256`、`sha512`、`hash`、`md5`、`crc32`。 |
| （有限GA）将帐户受众激活到某些目标 | Real-Time CDP B2B客户现在可以将[帐户受众](../../segmentation/types/account-audiences.md)激活到某些目标。 有关此功能的详细信息，请参阅[激活帐户受众教程](/help/destinations/ui/activate-account-audiences.md)。 |

{style="table-layout:auto"}

**修复和增强** {#destinations-fixes-and-enhancements}

有关目标的更多一般信息，请参阅[目标概述](../../destinations/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform 旨在丰富全球范围内的数字体验应用。企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。为了满足此需求，Experience Platform提供了可将单个Experience Platform实例划分为多个单独的虚拟环境的沙盒，以帮助开发和改进数字体验应用程序。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 沙盒工具 | 利用沙盒工具功能，可跨沙盒提高配置准确性并在沙盒之间无缝导出和导入沙盒配置。 您可以使用沙盒工具功能选择不同的对象并将它们导出到包中。 有关详细信息，请参阅[沙盒工具用户界面指南](../../sandboxes/ui/sandbox-tooling.md)。 |

有关沙箱的详细信息，请参阅[沙箱概述](../../sandboxes/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Experience Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 帐户受众（限定GA） | 在Real-Time Customer Data Platform B2B edition中，您现在可以使用帐户分段功能实现从基于人员的受众到基于帐户的受众的营销分段体验的全部简易和复杂化。 有关此功能的更多信息，请阅读[帐户受众概览](../../segmentation/types/account-audiences.md)。 |

若要了解有关分段服务的更多信息，请阅读[分段服务概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 更新了数据登陆区的身份验证 | 现在，您可以在查看凭据时看到数据登陆区域的指定到期日期。 您必须在到期日期之前刷新令牌才能继续在应用程序中使用它。 如果您未在规定的到期日期之前手动刷新令牌，则它将在您下次检索凭据时自动刷新并提供新令牌。 有关详细信息，请阅读有关[使用数据登录区](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md)的文档。 |

{style="table-layout:auto"}

若要了解有关源的更多信息，请阅读[源概述](../../sources/home.md)。
