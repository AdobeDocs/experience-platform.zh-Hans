---
title: Adobe Experience Platform发行说明2020年11月
description: Adobe Experience Platform 2020年11月版发行说明。
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2179'
ht-degree: 11%

---

# Adobe Experience Platform 发行说明

**发行日期：2020 年 11 月 11 日**

Adobe Experience Platform中的新增功能：

- [Adobe Experience Platform数据湖迁移](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

现有功能更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] 服务](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform数据湖迁移 {#migration}

当Adobe将数据湖从Gen1迁移到Gen2时，用户将能够从Data Lake中读取，但写入Data Lake的所有功能都将受到影响。 Adobe将与系统管理员联系以详细讨论迁移的影响，并确认特定组织的迁移日期和时间。

欲知更多信息，请阅读 [Data Lake迁移指南](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] 利用 [Adobe Admin Console](https://adminconsole.adobe.com) 产品配置文件，用于将用户与权限和沙盒相关联。 权限控制对各种平台功能的访问，包括数据建模、配置文件管理和沙盒管理。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 权限 | 在 [!DNL Admin Console]，中的选项卡 [!DNL Platform] 产品配置文件允许您自定义要 [!DNL Platform] 功能适用于附加到该配置文件的用户。 可用的权限类别包括： **[!UICONTROL 数据建模]**， **[!UICONTROL 数据管理]**， **[!UICONTROL 用户档案管理]**， **[!UICONTROL Identity Management]**， **[!UICONTROL 数据监测]**， **[!UICONTROL 沙盒管理]**， **[!UICONTROL 目标]**， **[!UICONTROL 数据摄取]**， **[!UICONTROL 数据科学工作区]**， **[!UICONTROL 查询服务]**、和 **[!UICONTROL 数据管理]**. |
| 沙盒访问权限 | 此 **[!UICONTROL 权限]** 选项卡 [!DNL Platform] 产品配置文件可以授予用户对特定沙盒的访问权限。 请参阅以下部分 [沙盒](#sandboxes) 有关更多信息，请参阅下文。 |

欲知更多信息，请参见 [访问控制概述](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] 是与集成的应用程序服务 [!DNL Experience Platform]. 它允许您利用 [!DNL Platform] 以便在适当的时间将优质的产品和体验提供给您在所有接触点上的客户。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 集中式优惠库 | 在该界面中，您可以创建和管理组成优惠的不同元素，并定义其规则和限制。 |
| 优惠决策引擎 | 优惠决策引擎可利用 [!DNL Platform] 数据和 [!DNL Real-Time Customer Profiles]以及选件库，以便选择合适的时间、客户和渠道来提供选件。 |

欲知更多信息，请参见 [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=zh-Hans) 文档。

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] 旨在丰富全球范围的数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署需要，同时确保操作法规遵从性。 为了满足这一需求， [!DNL Experience Platform] 提供对单个文件夹进行分区的沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 生产沙盒 | [!DNL Experience Platform] 提供单个生产沙盒，无法删除或重置。 生产和非生产可用的沙盒总数取决于获得的许可证。 |
| 非生产沙盒 | 可以为单个创建多个非生产沙盒 [!DNL Platform] 实例，允许您在不影响生产沙盒的情况下测试功能、运行实验以及进行自定义配置。 |
| 沙盒切换器 | 在 [!DNL Experience Platform] 用户界面中，屏幕左上角的沙盒切换器允许您通过下拉菜单在可用沙盒之间切换。 沙盒切换器还提供搜索功能，允许您筛选可用的沙盒。 |
| `x-sandbox-name` 标题 | 所有呼叫 [!DNL Experience Platform] API现在必须包含新的 `x-sandbox-name` 标头，其值引用 `name` 将在其中执行操作的沙盒的属性。 |

欲知更多信息，请参见 [沙盒概述](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师映射、转换和验证进出体验数据模型(XDM)的数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 迭代运算 | [!DNL Data Prep] 映射器现在支持在层次结构上执行迭代操作。 |
| 映射器函数 | [!DNL Data Prep] 映射器现在能够 **非** 将属性从源复制到目标XDM。 |

欲知更多信息，请参见 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## 数据科学工作区 {#dsw}

数据科学工作区使用机器学习和人工智能从您的数据创建见解。 数据科学工作区集成到Adobe Experience Platform中，可帮助您在各个Adobe解决方案中使用内容和数据资源做出预测。 数据科学工作区实现此目标的一种方式就是使用 [!DNL JupyterLab]. [!DNL JupyterLab] 是基于Web的用户界面，用于 [[!DNL Project Jupyter]](https://jupyter.org/) 并与Adobe Experience Platform紧密集成。 它为数据科学家提供了一个交互式开发环境 [!DNL Jupyter] 笔记本、代码和数据。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL JupyterLab] 方法生成器模板 | 笔记本到配方要求使用情况和版本已更新。 [!DNL Python] ML运行时基本映像已更新为使用 [!DNL Python] 3.6.7和a [!DNL Conda] 环境专用。 |

欲知更多信息，请阅读以下文档： [使用Jupyter Notebooks创建方法](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] 服务 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目标是预先构建的与目标平台的集成，可无缝地向这些合作伙伴激活数据。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| 布拉泽 | Braze是一个全面的客户参与平台，可为客户与他们所喜爱的品牌之间提供相关且令人难忘的体验。 |
| Microsoft兵 | Microsoft Bing目标可帮助您在Microsoft展示广告中执行重定位和面向受众的数字营销活动。 |
| 交易台 | Trade Desk是一个自助服务平台，供广告购买者跨显示器、视频和移动库存源执行重定位和面向受众的数字活动。 |

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 目标详细信息UX更新 | Real-Time CDP的目标工作流现在包括内联监测，以便您查看哪些批次激活成功。 此功能使用户能够通过警报和监视仪表板直接解决批量目标工作流中的问题，以跟踪处理管道中的错误。 |
| 文件加密 | 对于基于文件的目标，用户现在可以向其导出的文件添加加密。 |
| 文件计划 | 对于基于电子邮件的目标和云存储目标，用户可以创建一次性导出或创建每日快照。 |
| 必填字段 | 用户可以将字段标记为必填字段，确保仅导出包含必填字段的字段。 |

欲知更多信息，请参见 [目标概述](../../destinations/home.md).

## Intelligent Services {#intelligent-services}

智能服务可让营销分析师和从业人员在客户体验用例中利用人工智能和机器学习的功能。 借助此功能，营销分析人员可使用商业级别配置来设置特定于公司需求的预测，而无需具备数据科学专业知识。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| Consumer Experience Events (CEE)数据集 | 现在，创建CEE数据集支持使用架构编辑器将身份字段添加到数据集。 Attribution AI和客户人工智能使用主要标识来组合事件。 |

欲知更多信息，请阅读 [向数据集添加身份字段](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) （在Intelligent Services数据准备指南中）。

### 归因人工智能

作为Intelligent Services的一部分，Attribution AI是一种多渠道的算法归因服务，它计算客户交互对指定结果的影响和增量影响。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据源链接 | 可以查看原始数据集源的链接，并从所选服务实例的右边栏导航到。 |
| 编辑实例名称 | 您现在可以修改现有Attribution AI实例的名称。 |
| 克隆实例 | 复制当前选择的服务实例设置，并允许进行修改。 |
| 修改实例配置参数 | 如果现有Attribution AI实例尚未开始评分，您现在可以修改其配置。 |
| 一次得分 | 您现在可以在Attribution AI实例中触发临时模型评分。 |
| 通过列 | 您现在可以配置要添加到原始输出得分文件的附加列，以向BI工具视图添加附加维度。 |
| 实例激活和停用 | 您现在可以激活和停用计划的Attribution AI实例模型训练和评分。 |
| 权利跟踪 | 您可以在创建实例容器中找到您的帐户使用的归因分析总数。 |
| 按位置划分接触点 | 新的见解图形，按转化路径位置提供接触点分析。 |
| 热门转化路径 | 位于路径分析选项卡中的新见解图形。 该图包含排名前五的转化路径列表，其中显示了导致转化最多的营销渠道接触点顺序。 |
| 接触点有效性 | 深入分析模型用于衡量接触点效率的三个最重要的变量。 变量为接触正路径与接触负路径的比值、接触点效率以及接触点数量。 |

欲知更多信息，请阅读 [Attribution AI概述](../../intelligent-services/attribution-ai/overview.md).

### 客户人工智能

客户人工智能，作为Intelligent Services的一部分，为营销人员提供了在个人层面生成客户预测并提供解释的能力。 在影响因素的帮助下，客户人工智能可以告诉您客户可能会做什么以及为什么。此外，营销人员可以从客户人工智能预测和洞察中受益，通过提供最合适的优惠和消息传递来个性化客户体验。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据源链接 | 可以查看原始数据集源的链接，并从所选服务实例的右边栏导航到。 |
| 编辑实例名称 | 您可以修改现有客户人工智能实例的名称。 |
| 修改实例配置参数 | 如果现有客户人工智能实例尚未开始评分，您现在可以修改其配置。 |
| 克隆实例 | 复制当前选择的服务实例设置，并允许进行修改。 |
| 权利跟踪 | 在创建实例容器中，您可以找到客户人工智能针对您的帐户评分的用户档案总数。 |
| 预测目标 | 创建预测目标的灵活性得到了提高，现在有了新的选项可用于预测某件事是“将发生”还是“不会发生”。 此外，添加了用于预测在使用多个事件时是发生“所有”事件还是发生“任何”事件的选项。 |
| 影响因素深入分析 | 倾向主要影响因素存储段现在包含深入分析。 深入分析是倾向区间中每个主要影响因素值的更深入级别摘要。 |

欲知更多信息，请阅读 [Customer AI概述](../../intelligent-services/customer-ai/overview.md).

## 实时客户配置文件 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户配置文件，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。[!DNL Profile] 允许您将不同的客户数据整合到一个统一视图中，并提供每个客户交互的带时间戳的可操作帐户。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 更新了合并策略工作流 | 平台已将合并策略配置升级到新的逐步工作流。 此工作流使用户能够将来自多个用户档案数据集的数据片段整合在一起，并设置数据在这些数据集之间的合并优先级，以便创建每个人的全面视图。 用户可以通过选择适当的合并方法（已排序的时间戳或数据集优先级）并将ExperienceEvent数据集附加到配置文件数据集，来合并选定的XDM个人配置文件数据集。 |
| 合并架构视图 | 在Experience PlatformUI中，用户可以更轻松地找到有关参与合并架构的所有架构和数据集的信息，以及表面关键属性，如身份和关系字段。 这些更新提高了对配置文件是否正确配置、身份是否正确拼合以及数据是否已成功摄取进行故障排除和验证的能力。 |

有关Real-time Customer Profile的更多信息，包括有关使用的教程和最佳实践 [!DNL Profile] 数据，请阅读 [Real-time Customer Profile概述](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用来构建、标记和增强这些数据。 [!DNL Platform] 服务。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新源**

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL Shopify] | 您现在可以连接 [!DNL Shopify] 到 [!DNL Experience Platform] 使用 [!DNL Flow Service] API或UI。 请参阅 [Shopify连接器概述](../../sources/connectors/ecommerce/shopify.md) 以了解更多信息。 |

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 更新连接信息 | 您现在可以使用更新现有批处理连接的名称、说明和凭据 [!DNL Flow Service] API和UI。 有关更多信息，请参阅以下教程： [使用流服务API更新连接](../../sources/tutorials/api/update.md) 和 [使用UI编辑帐户详细信息](../../sources/tutorials/ui/monitor.md). |
| 删除连接 | 现在可以使用删除包含错误或变得不必要的批处理连接 [!DNL Flow Service] API和UI。 有关更多信息，请参阅以下教程： [使用流服务API删除连接](../../sources/tutorials/api/delete.md) 和 [使用用户界面删除帐户](../../sources/tutorials/ui/delete-accounts.md). |
| 分层映射 | 您可以在数据摄取过程中预览分层源文件，如JSON或Parquet。 请参阅上的教程 [在UI中为云存储连接器配置数据流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 以了解更多信息。 |
| API支持在流源中映射 | 您现在可以使用API对流源执行映射功能。 |
| API支持云存储源的自定义分隔符 | 您现在可以使用云存储源收集非CSV分隔的文件。 可以使用任何单列分隔符（如制表符、逗号、管道、分号或哈希）收集任何格式的平面文件。 |
| Adobe Audience Manager连接器的沙盒支持 | Audience Manager连接器现在支持沙盒识别。 用户可以启用连接器将Audience Manager数据集路由到他们选择的沙盒（包括非生产沙盒）。 每个组织的配置限制为一个沙盒。 |
| UX改进 | 基于文件的摄取现在可通过源目录访问。 |

要了解有关源的详细信息，请参阅 [源概述](../../sources/home.md).
