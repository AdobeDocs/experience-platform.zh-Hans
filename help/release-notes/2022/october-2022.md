---
title: Adobe Experience Platform发行说明2022年10月
description: 2022年10月版Adobe Experience Platform发行说明。
source-git-commit: 0ea2718247792e997b7a90ab9027946e800c8157
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发行日期：2022 年 10 月 26 日**

- [客户管理的密钥](#cmk)

Adobe Experience Platform 现有功能的更新包括：

- [数据收集](#data-collection)
- [体验数据模型(XDM)](#xdm)
- [查询服务](#query-service)
- [源](#sources)

## 客户管理的密钥 {#cmk}

存储在Adobe Experience Platform上的所有数据都将使用系统级别密钥在静态时进行加密。 如果您使用的是基于平台构建的应用程序，您现在可以选择使用自己的加密密钥，从而更好地控制数据安全。

请参阅 [客户管理密钥](../../landing/governance-privacy-security/customer-managed-keys.md) 以了解有关该功能的详细信息。

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，允许您收集客户端客户体验数据，并将其发送到Adobe Experience Platform边缘网络，以便对其进行扩充、转换和分发到Adobe或非Adobe目标。

**新增功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 数据流的敏感数据处理 | 数据流现在利用多种平台技术适当地处理受法规(如健康保险流通和责任法案(HIPAA))强制实施的敏感数据。 请参阅 [处理数据流中的敏感数据](../../edge/datastreams/overview.md#sensitive) 以了解更多信息。 |
| [!DNL Splunk] 事件转发扩展 | 您现在可以将数据发送到 [!DNL Splunk] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Splunk] 扩展概述](../../tags/extensions/web/splunk/overview.md) 以了解更多信息。 |
| [!DNL Zendesk] 事件转发扩展 | 您现在可以将数据发送到 [!DNL Zendesk] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Zendesk] 扩展概述](../../tags/extensions/web/zendesk/overview.md) 以了解更多信息。 |

{style=&quot;table-layout:auto&quot;}

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**更新了XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 数据类型 | [[!UICONTROL 会话详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 更新了 `authorized` 字段。 `season` 和 `episode` 已从整数更改为字符串。 |
| 数据类型 | [[!UICONTROL 广告详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` 已重命名为 `friendlyName`和 `ID` 已重命名为 `name`. |
| 数据类型 | [[!UICONTROL 错误详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` 已更名为 `name`。 |

{style=&quot;table-layout:auto&quot;}

有关Platform中XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md).

## 查询服务 {#query-service}

查询服务允许您使用标准SQL在Adobe Experience Platform中查询数据 [!DNL Data Lake]. 您可以连接 [!DNL Data Lake] 并将查询结果捕获为新数据集，以用于报表、Data Science Workspace或摄取到实时客户资料。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 查询加速报告分析数据模型 | 作为Data Distiller SKU的一部分，查询加速存储使您能够减少从数据中获得关键分析所需的时间和处理能力。 通过查询加速存储，您可以构建自定义数据模型和/或扩展现有的Adobe Real-time Customer Data Platform数据模型，以改进报表分析及其可视化图表。 请参阅 [查询加速存储报告分析文档](https://experienceleague.adobe.com/docs/experience-platform/query/query-accelerated-store/reporting-insights-data-model.html) 以了解有关此功能的更多信息。 |

{style=&quot;table-layout:auto&quot;}

有关查询服务的更多信息，请参阅 [查询服务概述](../../query-service/home.md).
Adobe Experience Platform的新增功能：

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- | 
| Adobe Workfront源的测试版可用性 | 使用 [Adobe Workfront源](../../sources/connectors/adobe-applications/workfront.md) 将Workfront数据Experience Platform并执行用例，例如将工作记录与第三方数据结合、对工作记录应用历史和时间序列分析，以及使用标准SQL查询工作数据。 有关更多信息，请阅读 [在UI中创建Workfront源连接](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| oracle服务云源的测试版可用性 | 使用Oracle服务云源将数据从您的Oracle服务云帐户中摄取到Experience Platform。 有关更多信息，请阅读 [Oracle服务云源](../../sources/connectors/customer-success/oracle-service-cloud.md). |

要进一步了解来源，请阅读 [源概述](../../sources/home.md).
