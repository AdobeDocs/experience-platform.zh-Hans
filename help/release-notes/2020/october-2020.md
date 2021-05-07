---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年10月
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 4%

---

# Adobe Experience Platform 发行说明

**发行日期：2020 年 10 月 14 日**

- [数据准备](#data-prep)
- [实时客户资料](#profile)
- [Segmentation Service](#segmentation)
- [源](#sources)
- [价值转化时间](#time-to-value)

## 数据准备 {#data-prep}

数据准备使数据工程师能够映射、转换和验证数据到体验数据模型(XDM)和从体验数据模型(XDM)的数据。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| `is_set` 函数 | `is_set`函数允许您检查源数据中是否存在属性。 `is_set` 可以与组合使 `is_empty` 用，以检查属性的存在和属性中值的存在。 |
| `get_values` 函数 | `get_values`函数允许您从输入映射中获取任何给定键的值。 |

有关详细信息，请阅读[数据准备概述](../../data-prep/home.md)。

## 实时客户资料 {#profile}

Adobe Experience Platform使您能够在客户与您的品牌互动的任何地方或何时为其提供协调一致的相关体验。 通过[!DNL Real-time Customer Profile]，您可以看到每个客户的整体视图，该客户综合了来自多个渠道的数据，包括在线、离线、CRM和第三方数据。 [!DNL Profile] 允许您将不同的客户数据整合到一个统一的视图中，为每次客户互动提供一个可操作、有时间戳的帐户。

| 功能 | 描述 |
| ------- | ----------- |
| 用户档案预览API附加 | 用户档案预览API(`/previewsamplestatus`)现在包括在您的IMS组织中视图用户档案片段总数的细目，以及在身份命名空间中视图用户档案片段分布的功能。 |
| 合并模式视图更新 | 在Experience Platform UI中，用户可以更轻松地查找有关所有对合并模式有贡献的模式和数据集的信息，以及身份和关系字段等表面关键属性。 这些更新改进了对正确配置用户档案、正确拼接身份和成功摄取数据进行故障诊断和验证的能力。 |

有关[!DNL Real-time Customer Profile]的详细信息，包括使用[!DNL Profile]数据的教程和最佳实践，请阅读[实时客户用户档案概述](../../profile/home.md)。

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service提供用户界面和RESTful API，使您能够根据[!DNL Real-time Customer Profile]数据构建区段和生成受众。 这些区段在[!DNL Platform]上集中配置和维护，使任何Adobe应用程序都可轻松访问它们。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准，定义特定的用户档案子集。细分可以基于记录数据（如人口统计信息）或表示客户与您品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 删除流分段限制 | 已删除回顾周期的七天限制。 |

有关[!DNL Segmentation Service]的详细信息，请参阅[分段概述](../../segmentation/home.md)

## 源 {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强该数据。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供RESTful API和交互式UI，让您可以轻松为各种数据提供者设置源连接。这些源连接允许您对外部存储系统和CRM服务进行身份验证并连接，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| SFTP的SSH身份验证支持 | 您可以使用RSA/DSA Open SSH密钥将您的SFTP帐户连接到[!DNL Platform]。 有关详细信息，请参阅[SFTP概述](../../sources/connectors/cloud-storage/sftp.md)。 |
| UX改进 | 在数据获取过程中，可以为[!DNL Profile]启用数据集。 有关详细信息，请参阅[云存储数据流工作流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)教程。 |

要了解有关源的详细信息，请参阅[源概述](../../sources/home.md)。

## 值{#time-to-value}的时间

Adobe Experience Platform完全支持营销运营团队构建客户的360度全方位视图，而无需大量数据工程专业知识。 目标是通过数据速度加快团队和价值。

“时间到价值”贯穿各个角色。 数据工程师可以以高效、加速的方式完成任务，并具备数据活动透明度，从而更快地提供可靠、可扩展的实时客户用户档案。 然后，营销人员可以使用完整、强大的客户用户档案进行细分和激活。

### 功能亮点

#### 架构

升级可用性和工作流程，提供模式构图中关键字段的开箱即用洞察、标准化和透明度。 显示表示为“合并模式”的各个数据模型组合的数据谱系，为实时客户用户档案提供对结构和组成的洞察。

- 模式工作流升级
   - 使用快捷键处理最常见的XDM模式类型，在模式编辑器和模式字段组建议中根据您的目标自动设置
   - 通过多字段组选择和预览功能提高工作流效率
   - 对模式合成的关键属性（包括标识、关系以及必填和已弃用字段）提供透明度
- 合并模式数据谱系和关键属性透明度

#### 数据摄取和收集

自动映射、映射预览和可用性升级从任何平台或源引入数据，用于用户档案、下游分段和激活。 该系统具有高效和智能性，使此过程更易于使用，即使是对IT以外的人员也是如此。

- 通过目录页卡和数据表内联操作模式升级更轻松地访问数据源
- 用于数据获取的计算字段/表达式
- 数据映射建议可加快摄取过程
- 映射预览和验证

#### 用户档案配置

具有自定义功能的适合营销人员的用户档案查看器可帮助您了解用于细分、规划和激活案例的用户档案组成。 通过为合并策略提供分步工作流，整合的工作流以受控和高效的方式为用户档案补充水分。

- 在增强的用户档案查看器中视图每个用户档案，该查看器显示具有完全自定义的仪表板，可根据营销人员的业务目标实现分组的跨渠道数据。
- 根据业务需要，在基本信息构件中编辑标准属性和自定义属性。
- 使用合并用户档案选择器，使用实时客户模式中的属性自定义构件。 合并模式是从用户档案数据获取中使用的基础数据模型派生的。


#### 监控

确保数据流的透明性，并从源连接器分析进入系统的数据流的运行状况，为故障排除情况提供更多自助服务和更快的操作能力。

- 监视所有流运行并查看每个运行的详细视图，包括完成状态、运行持续时间、处理文件的列表、错误和可操作的诊断
