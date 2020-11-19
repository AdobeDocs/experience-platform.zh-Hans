---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年11月11日
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 6cf9c88f6dc751a4cc877670a89cc99d1efb1b2a
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 3%

---


# Adobe Experience Platform 发行说明

**发行日期：2020 年 11 月 11 日**

Adobe Experience Platform的新增功能：

- [Adobe Experience Platform数据湖移民](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

对现有功能的更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] 服务](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Adobe Experience Platform数据湖移民 {#migration}

当Adobe将数据湖从Gen1迁移到Gen2时，用户将能够从数据湖中读取数据，但写入数据湖的所有功能都将受到影响。 Adobe将与系统管理员联系，详细讨论迁移的影响，并确认特定IMS组织的迁移日期和时间。

有关详细信息，请阅读数 [据湖迁移指南](../../landing/adls2-gen2-migration.md)。

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] 利用 [Adobe Admin Console](https://adminconsole.adobe.com) ()产品用户档案将用户与权限和沙箱关联起来。 权限控制对各种平台功能的访问，包括数据建模、用户档案管理和沙箱管理。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 权限 | 在中， [!DNL Admin Console]产品用户档案中的选 [!DNL Platform] 项卡允许您自定义哪些功能 [!DNL Platform] 可供附加到该用户档案的用户使用。 可用权限类别包括： **[!UICONTROL 数据管理建]**&#x200B;模、 **[!UICONTROL Identity Management、]**&#x200B;用户档案管理 **[!UICONTROL 、查询管理、监测数据、管理、]**********************************、沙箱、、数据、、数据、、数据、数据、、、服务、管理数据、管理。 |
| 访问沙箱 | 产品 **[!UICONTROL 用户档案]** 中的“权限 [!DNL Platform] ”选项卡可授予用户对特定沙箱的访问权限。 有关更多信息，请 [参阅](#sandboxes) 以下沙箱部分。 |

有关详细信息，请参阅 [访问控制概述](../../access-control/home.md)。

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] 是与集成的应用程序服务 [!DNL Experience Platform]。 它允许您利用 [!DNL Platform] 在正确的时间跨所有接触点为客户提供最佳优惠和体验。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 集中式优惠库 | 创建和管理构成优惠的不同元素并定义其规则和约束的界面。 |
| 优惠决策引擎 | 优惠决策引 [!DNL Platform] 擎利 [!DNL Real-time Customer Profiles]用数据，以及优惠库，以选择正确的时间、客户和渠道，将优惠交付到这些时间。 |

For more information, please see the [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=en) documentation.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] 旨在在全球范围内丰富数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。 为了满足这一需求，提 [!DNL Experience Platform] 供了沙箱，将单个实例分 [!DNL Platform] 为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 生产沙箱 | [!DNL Experience Platform] 提供一个无法删除或重置的生产沙箱。 可用沙箱（生产和非生产）的总数取决于所购买的许可证。 |
| 非生产沙箱 | 可以为单个实例创建多个非生产沙箱， [!DNL Platform] 使您能够测试功能、运行实验并制作自定义配置，而不会影响生产沙箱。 |
| 沙箱切换器 | 在用 [!DNL Experience Platform] 户界面中，屏幕左上角的沙箱切换器允许您通过下拉菜单在可用沙箱之间切换。 沙箱切换器还提供了搜索功能，允许您过滤可用沙箱。 |
| `x-sandbox-name` 标题 | 对API的所 [!DNL Experience Platform] 有调用现在必须包 `x-sandbox-name` 括新标头，其值引 `name` 用将执行操作的沙箱的属性。 |

有关详细信息，请参阅 [沙箱概述](../../sandboxes/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 迭代运算 | [!DNL Data Prep] 映射器现在支持在层次上执行迭代操作。 |
| 映射器函数 | [!DNL Data Prep] 映射器现在不能 **将属** 性从源复制到目标XDM。 |

有关详细信息，请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## 数据科学工作区 {#dsw}

数据科学工作区使用机器学习和人工智能从数据中获得洞察。 数据科学工作区集成到Adobe Experience Platform，可帮助您跨Adobe解决方案使用内容和数据资产进行预测。 数据科学工作区实现这一点的方法之一是使用 [!DNL JupyterLab]。 [!DNL JupyterLab] 是一个基于Web的用户界面，它 [[!DNL Project Jupyter]](https://jupyter.org/) 与Adobe Experience Platform紧密集成。 它为数据科学家提供了交互式开发环境，使他们能 [!DNL Jupyter] 够处理笔记本、代码和数据。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL JupyterLab] Recipe Builder模板 | 笔记本到菜谱要求使用和版本更新。 [!DNL Python] ML Runtime基本图像已更新为只 [!DNL Python] 使用3.6.7和 [!DNL Conda] 环境。 |

有关详细信息，请阅读使用Jupyter笔 [记本创建菜谱的文档](../../data-science-workspace/jupyterlab/create-a-recipe.md)。

## [!DNL Destinations] 服务 {#destinations}

在实 [时客户数据平台中](../../rtcdp/overview.md)，目标是预建的与目标平台集成，以无缝方式向这些合作伙伴激活数据。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| 布雷兹 | Braze是一个全面的客户互动平台，它为客户与他们喜爱的品牌之间提供相关且难忘的体验。 |
| Microsoft Bing | Microsoft Bing目标可帮助您跨Microsoft展示广告执行重定位和受众目标数字活动。 |
| 交易台 | 交易台是一个自助平台，可供广告购买者跨展示广告、视频和移动库存来源执行重定向和受众目标数字活动。 |

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 目标详细信息UX更新 | 实时CDP的目标工作流现在包括内联监视，因此您可以查看哪些批处理激活成功。 此功能将允许用户通过警报和监视仪表板直接解决批处理目标工作流中的问题，以跟踪处理管道中的错误。 |
| 文件加密 | 对于基于文件的目标，用户现在可以向导出的文件添加加密。 |
| 文件计划 | 对于基于电子邮件的存储和云数据目标，用户可以创建一次性导出或创建每日快照。 |
| 必填字段 | 用户可以将字段标记为必填，确保只导出包含必填字段的字段。 |

有关详细信息，请参阅目 [标概述](../../rtcdp/destinations/destinations-overview.md)。

## Intelligent Services {#intelligent-services}

智能服务使营销分析师和从业人员能够在客户体验使用案例中利用人工智能和机器学习的强大功能。 这使营销分析师能够使用业务级配置设置特定于公司需求的预测，而无需数据科学专业知识。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 消费者体验事件(CEE)数据集 | 创建CEE数据集现在支持使用模式编辑器向数据集添加标识字段。 Attribution AI和客户人工智能使用主身份来组合事件。 |

有关详细信息，请阅读《Intelligent Services数据准 [备指南》中有关向数据集添](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) 加标识字段的部分。

### Attribution AI

Attribution AI作为智能服务的一部分，是一种多渠道算法归因服务，用于计算客户交互对特定结果的影响和增量影响。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据源链接 | 可以查看指向原始数据集源的链接，并从选定服务实例的右边栏导航到该链接。 |
| 编辑实例名称 | 您现在可以修改现有Attribution AI实例的名称。 |
| 克隆实例 | 复制当前选定的服务实例设置并允许修改。 |
| 修改实例配置参数 | 现在，如果现有Attribution AI实例尚未开始评分，您可以修改其配置。 |
| 一次性评分 | 您现在可以在Attribution AI实例中触发点对点模型评分。 |
| 通过列 | 您现在可以配置将添加到原始输出得分文件的附加列，以向BI工具视图添加其他尺寸。 |
| 实例激活和去激活 | 您现在可以激活和取消激活Attribution AI实例的计划模型培训和评分。 |
| 权利跟踪 | 您可以在创建实例容器中查找帐户占用的归因洞察总数。 |
| 触点细分（按位置） | 新的洞察图，可按转化路径位置提供接触点分析。 |
| 顶级转换路径 | 位于路径分析选项卡中的新洞察图。 该图表包含前5个转化路径的列表，这些转化路径显示导致转化率最高的营销渠道接触点的顺序。 |
| 触点有效性 | 深入了解模型衡量接触点有效性时所依据的三个最重要变量。 变量包括接触的正和负路径、接触点效率和接触点体积的比率。 |

有关详细信息，请阅读 [Attribution AI概述](../../intelligent-services/attribution-ai/overview.md)。

### 客户人工智能

作为智能服务的一部分，客户人工智能为营销人员提供了在个人层面生成客户预测并提供解释的能力。 在影响因素的帮助下，客户人工智能可以告诉您客户可能做什么以及为什么。 此外，营销人员还可以从客户人工智能预测和洞察中受益，通过提供最合适的优惠和消息来个性化客户体验。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据源链接 | 可以查看指向原始数据集源的链接，并从选定服务实例的右边栏导航到该链接。 |
| 编辑实例名称 | 您可以修改现有客户人工智能实例的名称。 |
| 修改实例配置参数 | 现在，如果现有客户AI实例尚未开始评分，您可以修改该实例的配置。 |
| 克隆实例 | 复制当前选定的服务实例设置并允许修改。 |
| 权利跟踪 | 您可以在创建实例用户档案中查找由客户AI为您的帐户计分的容器总数。 |
| 预测目标 | 通过新的选项来预测某事“会发生”还是“不会发生”，在制定预测目标方面的灵活性得到了增强。 此外，还添加了用于预测在使用多个事件时是“全部”事件还是“任何”事件发生的选项。 |
| 影响因素下钻 | 倾向最大影响因素时段现在包含追溯。 追溯是倾向时段内每个主要影响因素的更深层值摘要。 |

有关详细信息，请阅读客 [户人工智能概述](../../intelligent-services/customer-ai/overview.md)。

## 实时客户资料 {#profile}

Adobe Experience Platform使您能够为客户提供协调、一致和相关的体验，无论客户在何处或何时与您的品牌互动。 通过实时客户用户档案，您可以看到每个客户的整体视图，该将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）相结合。 [!DNL Profile] 允许您将不同的客户数据整合到统一的视图中，为每次客户互动提供可操作、有时间戳的帐户。

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 更新的合并策略工作流 | 平台已将合并策略配置升级为新的逐步式工作流。 此工作流程使用户能够整合来自多个用户档案集的数据片段，并为数据在这些数据集中的合并设置优先级，以便为每个数据集创建全面的视图。 用户可以通过选择适当的合并方法（按时间戳顺序或数据集优先级）并将ExperienceEvent数据集追加到用户档案数据集，来合并选定的XDM单个用户档案数据集。 |
| 合并模式视图 | 在Experience PlatformUI中，用户可以更轻松地找到有关所有模式和对合并模式有贡献的数据集的信息，以及表面关键属性，如标识和关系字段。 这些更新改进了对用户档案正确配置、身份正确拼接和数据成功摄取进行故障诊断和验证的能力。 |

有关实时客户用户档案的更多信息，包括有关使用数据的教程和最 [!DNL Profile] 佳实践，请阅 [读实时客户用户档案概述](../../profile/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部来源收集数据，同时允许您使用服务来构建、标记和增强该 [!DNL Platform] 数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新来源**

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL Shopify] | 您现在可以 [!DNL Shopify] 使 [!DNL Experience Platform] 用API [!DNL Flow Service] 或UI连接到。 有关详细 [信息，请参阅](../../sources/connectors/ecommerce/shopify.md) Shopify连接器概述。 |

**主要功能**

| 功能 | 描述 |
| ------- | ----------- |
| 更新连接信息 | 您现在可以使用API和UI更新现有批处理连接的名称、 [!DNL Flow Service] 说明和凭据。 有关详细信息，请参阅有关使用流 [服务API更新连接和](../../sources/tutorials/api/update.md)[使用UI编辑帐户详细信息的教程](../../sources/tutorials/ui/monitor.md)。 |
| 删除连接 | 现在，可以使用API和UI删除包含错误或已变得不必 [!DNL Flow Service] 要的批处理连接。 有关详细信息，请参阅教 [程，该教程涉及使用流服务API](../../sources/tutorials/api/delete.md)[删除连接以及使用UI删除帐户](../../sources/tutorials/ui/delete-accounts.md)。 |
| 分层映射 | 在预览获取过程中，您可以分层的源文件，如JSON或Parke。 有关详细信息，请 [参阅在UI中为云存储连接器配置流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 。 |
| 流源中映射的API支持 | 您现在可以使用API对流源执行映射功能。 |
| 对云存储源的自定义分隔符的API支持 | 您现在可以使用云存储源收集非CSV分隔文件。 您可以使用任何单列分隔符（如制表符、逗号、管道、分号或哈希）以任何格式收集平面文件。 |
| 对Adobe Audience Manager连接器的沙箱支持 | Audience Manager连接器现在可感知沙箱。 用户可以使连接器将Audience Manager数据集路由到自己选择的沙箱（包括非生产沙箱）。 此配置仅限于每个IMS组织一个沙箱。 |
| UX改进 | 现在可通过源目录访问基于文件的摄取。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md)。