---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform 2023年10月版发行说明。
source-git-commit: ac7597a2e63559f3af91d559dd77f7778c9f27bb
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 36%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 10 月 25 日**

 Experience Platform 中现有功能的更新：

- [数据收集](#data-collection)
- [目标](#destinations)
- [沙盒](#sandboxes)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 扩展 | [!DNL Meta] 转化API增强功能 | 有三项增强功能 [元转化API](/help/tags/extensions/server/meta/overview.md) 扩展名： <ul><li>与集成 [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe)：通过允许您共享用于转化API与Adobe集成的像素ID和访问令牌，创建无缝登录体验。</li><li>与集成 [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq)：用于向更有可能完成所需操作的人投放广告，并将操作链接回投放的广告。</li><li>与集成 [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha)：允许您在CIP字段中传递LiveRamp的RampID，而无需直接与合作伙伴或Meta共享PII。 </li></ul> |

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
| 计算字段中支持哈希函数 | 除了的特定功能外 [导出数组](../../destinations/ui/export-arrays-calculated-fields.md) 或数组中的元素时，您现在可以使用 [哈希函数](../../destinations/ui/export-arrays-calculated-fields.md#hashing-functions) 以散列导出文件中的属性。 支持的哈希函数包括： `sha`， `sha256`， `sha512`， `hash`， `md5`， `crc32`. |

{style="table-layout:auto"}

**修复和增强** {#destinations-fixes-and-enhancements}

有关目标的更多一般信息，请参阅[目标概览](../../destinations/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform旨在丰富全球范围内的数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署需要，同时确保操作法规遵从性。 为了满足此需求，Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的沙箱，以帮助开发和改进数字体验应用程序。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 沙盒工具 | 利用沙盒工具功能，可跨沙盒提高配置准确性并在沙盒之间无缝导出和导入沙盒配置。 您可以使用沙盒工具功能选择不同的对象并将它们导出到包中。 欲了解更多信息，请参见 [沙盒工具UI指南](../../sandboxes/ui/sandbox-tooling.md). |

有关沙箱的详细信息，请参阅 [沙盒概述](../../sandboxes/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 帐户受众（限定GA） | 在Real-time Customer Data Platform B2B版本中，您现在可以使用帐户分段，从基于人员的受众到基于帐户的受众，全面简化营销分段体验。 有关此功能的详细信息，请阅读 [帐户受众概述](../../segmentation/ui/account-audiences.md). |

要了解有关分段服务的更多信息，请阅读 [分段服务概述](../../segmentation/home.md).

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 更新了数据登陆区的身份验证 | 现在，您可以在查看凭据时看到数据登陆区域的指定到期日期。 您必须在到期日期之前刷新令牌才能继续在应用程序中使用它。 如果您未在规定的到期日期之前手动刷新令牌，则它将在您下次检索凭据时自动刷新并提供新令牌。 有关详细信息，请阅读以下文档： [使用数据登陆区](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

要了解有关来源的更多信息，请阅读 [源概述](../../sources/home.md).
