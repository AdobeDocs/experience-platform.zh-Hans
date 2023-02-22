---
title: Adobe Experience Platform发行说明2023年2月
description: 2023年2月版Adobe Experience Platform发行说明。
source-git-commit: 1c2b7f291d0f8c0845a76ba4c863a9558da1bb4f
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 3%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 2 月 22 日**

Adobe Experience Platform 现有功能的更新包括：

- [体验数据模型(XDM)](#xdm)
- [查询服务](#query-service)
- [Real-Time CDP B2B版中的相关帐户](#related-accounts)
- [源](#sources)

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**更新功能**
&#x200B; |功能 |描述 | | — | — | |通过UI弃用字段 |现在，在摄取数据后，您可以弃用架构中的字段。 XDM字段弃用允许您从UI视图中删除字段，同时保留这些字段以供使用。 如果需要，您可以再次显示已弃用的字段，并且引用这些字段的任何区段、查询或下游解决方案将照常运行。 |

{style=&quot;table-layout:auto&quot;}有关&#x200B;Platform中XDM的详细信息，请阅读 [XDM系统概述](../../xdm/home.md).&#x200B;
<!-- Field deprecation: https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/field-deprecation.html -->

## 查询服务 {#query-service}

查询服务允许您使用标准SQL在Adobe Experience Platform中查询数据 [!DNL Data Lake]. 您可以加入来自数据湖的任何数据集，并作为新数据集捕获查询结果，以用于报表、Data Science Workspace或将其摄取到实时客户资料中。

**更新功能**
&#x200B; |功能 |描述 | | — | — | |为使用SQL的配置文件启用数据集 |在CTAS查询中使用LABEL来使数据集“启用配置文件”，或使用ALTER来更新要为配置文件启用的现有数据集。 | |监视计划查询 |使用计划查询选项卡查找有关查询运行和订阅警报的重要信息。 如果计划详细信息、状态和错误消息/代码失败，则监视查询。  | |切换自动完成功能 |通过切换查询编辑器自动完成功能，消除某些元数据命令并缩短处理时间。 此功能会在您编写查询时自动为查询建议潜在的SQL关键字和表详细信息。 | |数据集示例 |在查询中指定采样率，然后使用数据集示例创建统一的随机示例，或根据特定条件创建条件示例。 |

{style=&quot;table-layout:auto&quot;}有&#x200B;关查询服务的详细信息，请参阅 [查询服务概述](../../query-service/home.md).&#x200B;
<!-- Links for QS feature docs after release day: -->
<!-- Enable datasets for profile with SQL link: https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html#create-table-as-select -->
<!-- Monitor scheduled queries link: https://experienceleague.adobe.com/docs/experience-platform/query/monitor-queries.html  -->
<!-- Toggle auto-complete feature link: https://experienceleague.adobe.com/docs/experience-platform/query/ui/user-guide.html#auto-complete -->
<!-- dataset samples: https://experienceleague.adobe.com/docs/experience-platform/query/essential-concepts/dataset-samples.html -->

## Real-Time CDP B2B版中的相关帐户 {#related-accounts}

>[!NOTE]
>
>“相关帐户”功能仅适用于Real-Time CDP B2B Edition的客户。

相关帐户， [!DNL Real-Time CDP B2B] 允许您查看与您正在浏览的帐户类似的帐户列表。 您可以在区段定义中包含相关帐户，以扩大您的范围或在区段中应用更广泛的标准。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 启用相关帐户服务 | 新的切换功能允许您在帐户上启用相关帐户服务。 有关更多信息，请阅读 [启用相关帐户服务](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

请在以下文档页面中阅读有关相关帐户功能的更多信息：

- [Real-Time CDP B2B版中的相关帐户概述](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [帐户配置文件UI指南中的“相关帐户”选项卡](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [如何在区段定义中使用相关帐户](../../rtcdp/segmentation/b2b.md#related-accounts)

要了解有关Real-Time CDP B2B Edition的更多信息，请阅读 [Real-Time CDP B2B版概述](../../rtcdp/overview.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 指定订阅级别访问 [!DNL Google PubSub] | 现在，您可以在使用 [!DNL Google PubSub] 来源，方法是在进行身份验证时提供订阅ID。 有关更多信息，请阅读 [!DNL Google PubSub] 身份验证教程 [使用流量服务API](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) 或 [平台UI](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| 从中摄取自定义活动数据 [!DNL Marketo] | 您现在可以从 [!DNL Marketo] 实例Experience Platform。 要摄取自定义活动数据，您必须在B2B活动架构中设置自定义活动字段组，并使用活动数据集创建数据流。 数据流完成后，摄取的数据集将同时包含您 [!DNL Marketo] 实例。 然后，您可以使用 [查询服务](../../query-service/home.md) 以在Platform上访问自定义活动记录。 有关更多信息，请阅读 [为自定义活动数据创建数据流](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| 从 [!DNL Marketo] | 现在，您可以配置在为公司数据创建数据流时，是要从摄取中排除还是包含未声明的帐户。 有关更多信息，请阅读 [创建源连接和数据流 [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

要进一步了解来源，请阅读 [源概述](../../sources/home.md).