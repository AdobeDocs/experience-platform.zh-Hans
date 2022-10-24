---
title: Adobe Experience Platform发行说明2020年11月
description: 2020年11月版Adobe Experience Platform发行说明。
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发行日期：2020 年 11 月 11 日**

Adobe Experience Platform的新增功能：

- [Adobe Experience Platform Data Lake迁移](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

现有功能的更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] 服务](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform Data Lake迁移 {#migration}

当Adobe将数据湖从Gen1迁移到Gen2时，用户将能够从数据湖中读取数据，但写入数据湖的所有功能都将受到影响。 Adobe将联系系统管理员以详细讨论迁移的影响，并确认特定IMS组织的迁移日期和时间。

欲知更多信息，请阅读 [Data Lake迁移指南](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] 利用 [Adobe Admin Console](https://adminconsole.adobe.com) 产品配置文件，用于将用户与权限和沙箱关联。 权限控制对各种平台功能的访问，包括数据建模、配置文件管理和沙盒管理。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 权限 | 在 [!DNL Admin Console], [!DNL Platform] 产品配置文件允许您自定义 [!DNL Platform] 附加到该用户档案的用户可以使用这些功能。 可用的权限类别包括： **[!UICONTROL 数据建模]**, **[!UICONTROL 数据管理]**, **[!UICONTROL 配置文件管理]**, **[!UICONTROL Identity Management]**, **[!UICONTROL 数据监控]**, **[!UICONTROL 沙盒管理]**, **[!UICONTROL 目标]**, **[!UICONTROL 数据摄取]**, **[!UICONTROL 数据科学工作区]**, **[!UICONTROL 查询服务]**&#x200B;和 **[!UICONTROL 数据管理]**. |
| 访问沙箱 | 的 **[!UICONTROL 权限]** 选项卡 [!DNL Platform] 产品配置文件可授予用户访问特定沙箱的权限。 请参阅 [沙箱](#sandboxes) 下面以了解更多信息。 |

有关详细信息，请参阅 [访问控制概述](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] 是与 [!DNL Experience Platform]. 它允许您利用 [!DNL Platform] 以在适当的时间跨所有接触点为客户提供最佳选件和体验。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 集中化优惠库 | 在该界面中，您可以创建和管理构成选件的不同元素，并定义其规则和约束。 |
| 优惠决策引擎 | 选件决策引擎可利用 [!DNL Platform] 数据和 [!DNL Real-time Customer Profiles]，以及选件库一起选择要将选件交付到的正确时间、客户和渠道。 |

有关详细信息，请参阅 [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=zh-Hans) 文档。

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] 旨在在全球范围内丰富数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。 为了满足这一需要， [!DNL Experience Platform] 提供用于划分单个 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 生产沙盒 | [!DNL Experience Platform] 提供了一个生产沙盒，无法删除或重置。 可用沙箱、生产和非生产的总数取决于所获得的许可证。 |
| 非生产沙箱 | 可以为单个沙箱创建多个非生产沙箱 [!DNL Platform] 实例，允许您测试功能、运行实验和创建自定义配置，而不会影响生产沙盒。 |
| 沙盒切换器 | 在 [!DNL Experience Platform] 用户界面屏幕左上角的沙盒切换器允许您通过下拉菜单在可用的沙盒之间进行切换。 沙盒切换器还提供了一个搜索功能，允许您过滤可用的沙箱。 |
| `x-sandbox-name` 标题 | 所有对 [!DNL Experience Platform] API现在必须包含新 `x-sandbox-name` 标题，其值引用 `name` 操作将在其中进行的沙盒的属性。 |

有关详细信息，请参阅 [沙箱概述](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 迭代运算 | [!DNL Data Prep] 映射程序现在支持对层次结构执行迭代操作。 |
| 映射器函数 | [!DNL Data Prep] 映射程序现在能够 **not** 将属性从源复制到目标XDM。 |

有关详细信息，请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## 数据科学工作区 {#dsw}

数据科学工作区使用机器学习和人工智能从您的数据中创建分析。 Data Science Workspace集成到Adobe Experience Platform中，可帮助您跨Adobe解决方案使用内容和数据资产进行预测。 数据科学工作区完成此操作的一种方式是通过使用 [!DNL JupyterLab]. [!DNL JupyterLab] 是 [[!DNL Project Jupyter]](https://jupyter.org/) 与Adobe Experience Platform紧密结合。 它为数据科学家提供了一个交互式开发环境，以便与之合作 [!DNL Jupyter] 笔记本、代码和数据。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL JupyterLab] 方法生成器模板 | 笔记本到方法要求使用情况和更新的版本。 [!DNL Python] ML运行时基本图像已更新为使用 [!DNL Python] 3.6.7和a [!DNL Conda] 环境。 |

欲知更多信息，请阅读 [使用Jupyter Notebooks创建方法](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] 服务 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目标是与目标平台的预建集成，可无缝地向这些合作伙伴激活数据。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| 布雷兹 | Braze是一个全面的客户参与平台，可为客户和他们喜爱的品牌之间提供相关且令人难忘的体验。 |
| Microsoft兵 | Microsoft Bing目标可帮助您在Microsoft展示广告中执行重定位和受众定位的数字营销活动。 |
| 交易台 | 交易台是一个自助平台，可让广告购买者跨展示、视频和移动设备库存源执行重定位和受众定位的数字促销活动。 |

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 目标详细信息UX更新 | Real-Time CDP的目标工作流现在包含内联监控，以便您能够查看哪些批量激活成功。 此功能将允许用户通过警报和监控功能板直接解决批量目标工作流中的问题，以跟踪处理管道中的错误。 |
| 文件加密 | 对于基于文件的目标，用户现在可以向其导出的文件添加加密。 |
| 文件计划 | 对于基于电子邮件的存储目标和云存储目标，用户可以创建一次性导出或创建每日快照。 |
| 必填字段 | 用户可以将字段标记为必填字段，以确保只导出包含必填字段的字段。 |

有关详细信息，请参阅 [目标概述](../../destinations/home.md).

## Intelligent Services {#intelligent-services}

“智能服务”使营销分析师和从业人员能够在客户体验用例中利用人工智能和机器学习的强大功能。 这允许营销分析人员使用业务级别配置来设置特定于公司需求的预测，而无需具备数据科学专业知识。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 消费者体验事件(CEE)数据集 | 现在，创建CEE数据集支持使用架构编辑器将身份字段添加到数据集。 Attribution AI和Customer AI使用主标识来组合事件。 |

有关更多信息，请阅读 [向数据集添加标识字段](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) （位于“智能服务”数据准备指南中）。

### 归因人工智能

Attribution AI，作为智能服务的一部分，是一种多渠道的算法归因服务，用于计算客户交互对特定结果的影响和增量影响。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据源链接 | 可以从选定服务实例的右边栏查看并导航到原始数据集源的链接。 |
| 编辑实例名称 | 您现在可以修改现有Attribution AI实例的名称。 |
| 克隆实例 | 复制当前选定的服务实例设置并允许进行修改。 |
| 修改实例配置参数 | 现在，如果现有Attribution AI实例尚未开始评分，您可以修改其配置。 |
| 一次打分 | 您现在可以在Attribution AI实例中触发临时模型评分。 |
| 传递列 | 您现在可以配置将添加到原始输出得分文件的附加列，以向BI工具视图添加其他维度。 |
| 实例激活和取消激活 | 您现在可以激活和取消激活计划的模型培训和Attribution AI实例评分。 |
| 授权跟踪 | 您可以在创建实例容器中找到您的帐户使用的归因分析总数。 |
| 按位置划分接触点 | 新的分析图，可按转化路径位置提供接触点分析。 |
| 热门转化路径 | 位于路径分析选项卡中的新分析图。 图表包含前五个转化路径的列表，其中显示了导致最多转化的营销渠道接触点的序列。 |
| 接触点有效性 | 提供对模型衡量接触点有效性所依据的三个最重要变量的深入分析。 变量包括接触的正反路径比、接触点效率和接触点体积。 |

欲知更多信息，请阅读 [Attribution AI概述](../../intelligent-services/attribution-ai/overview.md).

### 客户人工智能

Customer AI是Intelligent Services的一部分，它为营销人员提供了在个人级别生成客户预测并提供解释的功能。 在影响因素的帮助下，客户人工智能可以告诉您客户可能会做什么以及为什么。此外，营销人员可以从客户人工智能预测和洞察中受益，通过提供最合适的优惠和消息传递来个性化客户体验。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据源链接 | 可以从选定服务实例的右边栏查看并导航到原始数据集源的链接。 |
| 编辑实例名称 | 您可以修改现有Customer AI实例的名称。 |
| 修改实例配置参数 | 现在，如果现有Customer AI实例尚未开始评分，您可以修改其配置。 |
| 克隆实例 | 复制当前选定的服务实例设置并允许进行修改。 |
| 授权跟踪 | 您可以在创建实例容器中找到由Customer AI为您的帐户打分的用户档案总数。 |
| 预测目标 | 在创建预测目标时增加了灵活性，增加了新选项来预测“将会发生”还是“不会发生”。 此外，还添加了用于预测在使用多个事件时是“所有”事件发生还是“任何”事件发生的选项。 |
| 影响因素深入分析 | 倾向最大影响因素时段现在包含追溯。 深入分析是倾向时段内每个最主要影响因素的更深入的值汇总。 |

欲知更多信息，请阅读 [Customer AI概述](../../intelligent-services/customer-ai/overview.md).

## 实时客户个人资料 {#profile}

Adobe Experience Platform使您能够为客户在何处或何时与您的品牌进行交互，从而提供协调、一致的相关体验。 通过实时客户资料，您可以查看每个客户的整体视图，该视图将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）进行整合。 [!DNL Profile] 允许您将不同的客户数据整合到统一视图中，为每次客户互动提供一个可操作且带有时间戳的帐户。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 更新了合并策略工作流 | 平台已将合并策略配置升级为新的逐步式工作流。 通过此工作流，用户可以整合多个配置文件数据集中的数据片段，并为如何在这些数据集中合并数据设置优先级，以便创建每个数据集的综合视图。 通过选择适当的合并方法（按时间戳顺序或数据集优先顺序）并将ExperienceEvent数据集附加到配置文件数据集，用户可以合并选定的XDM个人配置文件数据集。 |
| 并集架构视图 | 在Experience PlatformUI中，用户可以更轻松地查找有关所有模式和对合并模式做出贡献的数据集的信息，以及身份和关系字段等表面键属性。 这些更新改进了对配置文件进行故障诊断和验证的功能，确认配置文件配置正确，身份拼合正确，数据已成功摄取。 |

有关实时客户资料的更多信息，包括与 [!DNL Profile] 数据，请阅读 [实时客户资料概述](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用 [!DNL Platform] 服务。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供了RESTful API和交互式UI，让您能够轻松为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**新来源**

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL Shopify] | 您现在可以连接 [!DNL Shopify] to [!DNL Experience Platform] 使用 [!DNL Flow Service] API或UI。 请参阅 [Shopify连接器概述](../../sources/connectors/ecommerce/shopify.md) 以了解更多信息。 |

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 更新连接信息 | 您现在可以使用 [!DNL Flow Service] API和UI。 有关更多信息，请参阅 [使用流服务API更新连接](../../sources/tutorials/api/update.md) 和 [使用UI编辑帐户详细信息](../../sources/tutorials/ui/monitor.md). |
| 删除连接 | 现在，可以使用 [!DNL Flow Service] API和UI。 有关更多信息，请参阅 [使用流量服务API删除连接](../../sources/tutorials/api/delete.md) 和 [使用UI删除帐户](../../sources/tutorials/ui/delete-accounts.md). |
| 分层映射 | 在数据获取过程中，您可以预览分层源文件，如JSON或Parquet。 请参阅 [在UI中为云存储连接器配置数据流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 以了解更多信息。 |
| 支持在流源中映射的API | 现在，您可以使用API来通过流源执行映射功能。 |
| 支持云存储源的自定义分隔符的API | 您现在可以使用云存储源收集非CSV分隔的文件。 您可以使用任何单列分隔符（如制表符、逗号、管道字符、分号或哈希）来收集任何格式的平面文件。 |
| 对Adobe Audience Manager连接器的沙盒支持 | Audience Manager连接器现在支持沙盒感知。 用户可以使连接器将Audience Manager数据集路由到他们选择的沙盒（包括非生产沙盒）。 配置限制为每个IMS组织只能有一个沙盒。 |
| UX改进 | 基于文件的摄取现在可通过源目录访问。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md).
