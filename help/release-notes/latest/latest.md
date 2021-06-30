---
title: Adobe Experience Platform 发行说明
description: Experience Platform2021年6月30日发行说明。
doc-type: release notes
last-update: June 30, 2021
author: ens60013
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: fc916f87bf07e5eabf7d1681059406e2fea362e0
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 6%

---


# Adobe Experience Platform 发行说明

**发布日期：2021 年 6 月 30 日**

Adobe Experience Platform 现有功能的更新包括：

- [实时客户资料](#profile)
- [沙盒](#sandboxes)
- [源](#sources)

## 实时客户资料 {#profile}

Adobe Experience Platform使您能够为客户在何处或何时与您的品牌进行交互，从而提供协调、一致的相关体验。 通过实时客户资料，您可以查看每个客户的整体视图，该视图将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）进行整合。 [!DNL Profile] 允许您将客户数据整合到统一视图中，为每次客户交互提供一个可操作且带有时间戳的帐户。

| 功能 | 描述 |
| ------- | ----------- |
| 合并策略工作流更新 | 现在，在UI中创建和更新合并策略时，用户可以基于并集架构预览20个示例用户档案。 这允许用户在保存合并策略配置之前预览客户配置文件的外观。 有关更多信息，请参阅[合并策略UI指南](../../profile/merge-policies/ui-guide.md)。 |
| 身份重叠报表 | 身份重叠报表是实时客户用户档案API的一部分，可显示用户档案存储的构成。 身份重叠报表使用`/previewsamplestatus`端点会公开对可寻址受众贡献最大的身份。 要了解更多信息，请访问[预览示例状态API端点指南](../../profile/api/preview-sample-status.md)。 |

有关实时客户资料的更多信息，包括有关使用[!DNL Profile]数据的教程和最佳实践，请首先阅读[实时客户资料概述](../../profile/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform旨在在全球范围内丰富数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。 为了满足这一需求，Experience Platform提供了将单个Platform实例分区为单独虚拟环境的沙盒，以帮助开发和改进数字体验应用程序。

| 功能 | 描述 |
| ------- | ----------- |
| 生产沙盒重置增强功能 | 您现在可以重置用于与Adobe Audience Manager或Audience Core Service进行双向区段共享的生产沙箱。 这可以从UI中完成，也可以使用API中新的`validationOnly`和`ignoreWarnings`参数来完成。 有关更多信息，请参阅有关在UI](../../sandboxes/ui/user-guide.md)中重置沙盒以及在API](../../sandboxes/api/sandboxes.md)中重置沙盒的教程。[[ |

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL Veeva CRM] （测试版） | 您现在可以使用[!DNL Flow Service] API或UI将[!DNL Veeva CRM]连接到Experience Platform。 有关更多信息，请参阅[[!DNL Veeva CRM] 连接器概述](../../sources/connectors/crm/veeva.md)。 |
| 支持监控流数据流 | 现在，您可以使用源UI工作区来监控来自具有相应量度和状态的流源的数据摄取活动。 有关更多信息，请参阅[监控流数据流](../../sources/tutorials/ui/monitor-streaming.md)教程。 |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
