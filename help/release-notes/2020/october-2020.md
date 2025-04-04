---
title: Adobe Experience Platform 发行说明（2020 年 10 月）
description: Adobe Experience Platform 的 2020 年 10 月发行说明。
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 17%

---

# Adobe Experience Platform 发行说明

**发行日期： 2020年10月14日**

- [数据准备](#data-prep)
- [实时客户轮廓](#profile)
- [Segmentation Service](#segmentation)
- [源](#sources)
- [价值实现时间](#time-to-value)

## 数据准备 {#data-prep}

通过数据准备，数据工程师可从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| `is_set`函数 | `is_set`函数允许您检查源数据中是否存在属性。 `is_set`可以与`is_empty`结合使用，以检查属性是否存在以及该属性中值的存在。 |
| `get_values`函数 | `get_values`函数允许您从输入映射获取任何给定键的值。 |

有关更多信息，请参阅[数据准备概述](../../data-prep/home.md)。

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。通过[!DNL Real-Time Customer Profile]，您可以查看合并来自多个渠道（包括在线、离线、CRM和第三方数据）的数据的每个单个客户的整体视图。 [!DNL Profile]允许您将不同的客户数据整合到一个统一视图中，并提供每个客户交互的带时间戳的可操作帐户。

| 功能 | 描述 |
| ------- | ----------- |
| 配置文件预览API添加 | 配置文件预览API (`/previewsamplestatus`)现在包括查看组织内配置文件片段总数的细分以及查看跨身份命名空间配置文件片段分布的功能。 |
| 合并架构视图更新 | 在Experience Platform UI中，用户可以更轻松地找到有关参与合并架构的所有架构和数据集的信息，以及表面关键属性，如身份和关系字段。 这些更新提高了对配置文件是否正确配置、身份是否正确拼合以及数据是否已成功摄取进行故障排除和验证的能力。 |

有关[!DNL Real-Time Customer Profile]的更多信息，包括有关使用[!DNL Profile]数据的教程和最佳实践，请阅读[实时客户配置文件概述](../../profile/home.md)。

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service提供了一个用户界面和RESTful API，允许您根据[!DNL Real-Time Customer Profile]数据构建区段并生成受众。 这些区段是在[!DNL Experience Platform]上集中配置和维护的，因此任何Adobe应用程序都可以轻松访问它们。

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流分段限制移除 | 已删除回顾期限的七天限制。 |

有关[!DNL Segmentation Service]的详细信息，请参阅[分段概述](../../segmentation/home.md)

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强该数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform]提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| SFTP的SSH身份验证支持 | 您可以使用RSA/DSA Open SSH密钥将SFTP帐户连接到[!DNL Experience Platform]。 有关详细信息，请参阅[SFTP概述](../../sources/connectors/cloud-storage/sftp.md)。 |
| UX改进 | 您可以在数据摄取过程中为[!DNL Profile]启用数据集。 有关详细信息，请参阅[云存储数据流工作流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)教程。 |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。

## 价值实现时间 {#time-to-value}

Adobe Experience Platform完全支持营销运营团队建立其客户的360度视图，而无需广泛的数据工程专业知识。 目标是通过数据速度加快团队和价值实现。

“实现价值的时间”跨越了角色之间的界限。 数据工程师可以利用数据活动透明度以高效、加速的方式完成任务，从而更快地提供强大、可扩展的实时客户档案。 然后，营销人员可以使用完整、可靠的客户配置文件进行分段和激活。

### 功能亮点

#### 架构

升级可用性和工作流程，并提供架构组合中关键字段的现成见解、标准化和透明度。 为表示为“合并架构”的单个数据模型的组合公开数据谱系，从而深入了解实时客户档案的结构和组成部分。

- 架构工作流升级
   - 使用最常见的XDM架构类型快捷方式，在架构编辑器中实现自动设置，并根据您的目标对架构字段组进行推荐
   - 利用多字段组选择和预览功能提高工作流效率
   - 提供架构组合关键属性的透明度，包括身份、关系以及必需和已弃用的字段
- 合并架构数据谱系和关键属性透明度

#### 数据引入和收集

自动映射、映射预览和可用性升级从任何平台或源引入数据，以用于用户档案、下游分段和激活。 该系统具有高效和智能性，使此过程更易于使用，即使对于IT之外的人也是如此。

- 通过目录页面卡和数据表内联操作模式升级，更轻松地访问数据源
- 数据提取的计算字段/表达式
- 数据映射推荐可加快摄取过程
- 映射预览和验证

#### 配置文件配置

具有自定义功能的营销人员友好的配置文件查看器可帮助您了解用于分段、规划和激活案例的配置文件组成。 合并的工作流通过提供合并策略的分步工作流，以可控且高效的方式对配置文件进行水合。

- 在增强型配置文件查看器中查看每个配置文件，该查看器可显示一个包含完全自定义的功能板，从而可以根据营销人员的业务目标分组跨渠道数据。
- 根据业务需求，在基本信息构件中编辑标准和自定义属性。
- 使用合并架构选择器，使用实时客户配置文件中的属性自定义构件。 合并架构从配置文件数据摄取中使用的底层数据模型派生。


#### 监控

确保数据流的透明度，并深入了解源连接器进入系统的数据流量的运行状况，从而提供更自助的服务，并加快故障排除情况的可操作性。

- 监控所有流运行并查看每次运行的详细视图，包括完成状态、运行持续时间、已处理文件的列表、错误和可操作的诊断
