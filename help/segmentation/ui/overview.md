---
solution: Experience Platform
title: 分段服务UI指南
description: 了解如何在Adobe Experience Platform UI中创建和管理受众和区段定义。
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 692cdd3d8b30c3e5187a556e4f9ec80d675cb443
workflow-type: tm+mt
source-wordcount: '3910'
ht-degree: 3%

---

# 分段服务UI指南

[!DNL Adobe Experience Platform Segmentation Service] 提供了一个用于创建和管理受众和区段定义的用户界面。

## 快速入门

使用受众和区段定义需要了解各种 [!DNL Experience Platform] 与分段相关的服务。 在阅读本用户指南之前，请查看以下服务的文档：

- [[!DNL Segmentation Service]](../home.md)： [!DNL Segmentation Service] 允许您对存储在以下位置的数据分段： [!DNL Experience Platform] 将个人（如客户、潜在客户、用户或组织）关联到较小的组中。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md)：通过桥接被摄取到的不同数据源中的身份来创建客户用户档案 [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：[!DNL Platform] 用于组织客户体验数据的标准化框架。为了更好地利用分段，请确保您的数据被作为配置文件和事件摄取，并根据 [数据建模的最佳实践](../../xdm/schema/best-practices.md).

您还应该了解本文档中使用的两个关键术语并了解它们之间的差异：

- **受众**：一组具有相似行为和/或特征的人。 此人员集合可以由Adobe Experience Platform使用区段定义或受众合成（平台生成的受众）生成，也可以由外部源(例如自定义上传（外部生成的受众）)生成。
- **区段定义**：Adobe Experience Platform用于描述目标受众关键特征或行为的规则。
- **划分**：将配置文件划分为受众的行为。

## 概述

在Experience PlatformUI中，选择 **[!UICONTROL 受众]** 在左侧导航中打开 **[!UICONTROL 概述]** 选项卡显示 [!UICONTROL 受众] 仪表板。

>[!NOTE]
>
>如果您的组织是初次使用Platform，但尚未创建活动配置文件数据集或合并策略，则 [!UICONTROL 受众] 仪表板不可见。 相反， [!UICONTROL 概述] 选项卡会显示链接和文档，以帮助您开始使用受众。

### [!UICONTROL 受众] 仪表板 {#segments-dashboard}

此 **[!UICONTROL 受众]** 仪表板概述了与贵组织的受众数据相关的关键量度。

要了解更多信息，请访问 [受众仪表板指南](../../dashboards/guides/audiences.md).

![将显示受众仪表板。 该可视化图表显示各种构件，包括受众规模、按身份列出的配置文件、身份重叠以及受众规模变化趋势。](../../dashboards/images/segments/dashboard-overview.png)

## 浏览 {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="流失率"
>abstract="流失率表示与上次运行区段作业时相比，受众内正在更改的配置文件的百分比。"

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="评估方法"
>abstract="受众的评估方法包括批量评估、流式评估和边缘评估。"

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="将所有受众添加到计划"
>abstract="启用以将使用批次处理分段评估的所有受众包括在每日计划更新中。禁用此项可从计划更新中删除所有受众。"

选择 **[!UICONTROL 浏览]** 选项卡，查看贵组织的所有受众的列表。 此视图列出有关受众的信息，包括配置文件计数、来源、创建日期、上次修改日期、标记和细分。

![将显示浏览屏幕。 此时将显示属于该组织的所有受众的列表。](../images/ui/overview/audience-browse.png)

每个受众旁边都有一个省略号图标。 选择此选项将显示受众可用的快速操作列表。 此操作列表因受众的来源而异。

![对于起源的受众，将显示快速操作列表 [!UICONTROL 受众构成].](../images/ui/overview/browse-audience-composition-details.png)

| 操作 | 来源 | 描述 |
| ------ | ------- | ----------- |
| [!UICONTROL 编辑] | Segmentation Service | 允许您打开区段生成器以编辑受众。 有关使用区段生成器的更多信息，请参阅 [区段生成器UI指南](./segment-builder.md). |
| [!UICONTROL 打开合成] | 受众组合 | 允许您打开受众合成以查看受众。 有关受众构图的更多信息，请参阅 [受众合成UI指南](./audience-composition.md). |
| [!UICONTROL 激活到目标] | Segmentation Service | 允许您将受众激活到目标。 有关将受众激活到目标的更多详细信息，请参阅 [激活概述](../../destinations/ui/activation-overview.md). |
| [!UICONTROL 与合作伙伴共享] | 受众构成、自定义上传、分段服务 | 可让您与其他Platform用户共享受众。 有关此功能的详细信息，请阅读 [区段匹配概述](./segment-match/overview.md). |
| [!UICONTROL 管理标记] | 受众构成、自定义上传、分段服务 | 允许您管理属于受众的用户定义标记。 有关此功能的更多信息，请阅读以下部分： [过滤和标记](#manage-audiences). |
| [!UICONTROL 移至文件夹] | 受众构成、自定义上传、分段服务 | 允许您管理受众属于哪个文件夹。 有关此功能的更多信息，请阅读以下部分： [过滤和标记](#manage-audiences). |
| [!UICONTROL 复制] | 受众构成、自定义上传、分段服务 | 复制所选受众。 |
| [!UICONTROL 应用访问标签] | 受众构成、自定义上传、分段服务 | 允许您管理属于受众的访问标签。 有关访问标签的详细信息，请阅读以下文档： [管理标签](../../access-control/abac/ui/labels.md). |
| [!UICONTROL 存档] | 自定义上传 | 存档所选受众。 |
| [!UICONTROL 删除] | 受众构成、自定义上传、分段服务 | 删除所选受众。 |
| [!UICONTROL 添加到包] | 受众构成、自定义上传、分段服务 | 允许您在沙盒之间移动受众。 有关此功能的详细信息，请阅读 [沙盒工具指南](../../sandboxes/ui/sandbox-tooling.md). |

>[!NOTE]
>
> 您会 **非** 能够删除在目标激活中使用的受众。

页面顶部提供了以下选项：将所有受众添加到计划、导入受众、创建新受众以及查看更新频率的细分。

切换 **[!UICONTROL 计划所有受众]** 将启用计划分段。 有关计划分段的更多信息，请参阅 [本用户指南的计划分段部分](#scheduled-segmentation).

选择 **[!UICONTROL 导入受众]** 将允许您导入外部生成的受众。 要了解有关导入受众的更多信息，请阅读以下部分： [用户指南中的导入受众](#import-audience).

选择 **[!UICONTROL 创建受众]** 将允许您创建受众。 要了解有关创建受众的更多信息，请阅读以下部分： [在用户指南中创建受众](#create-audience).

![受众浏览页面上的顶部导航栏会突出显示。 此栏包含一个用于创建受众的按钮和一个用于导入受众的按钮。](../images/ui/overview/browse-audiences-top.png)

您可以选择 **[!UICONTROL 更新频率摘要]** 显示显示更新频率的饼图。

![更新频率摘要按钮突出显示。](../images/ui/overview/browse-audience-update-frequency-summary.png)

此时将显示饼图，其中按更新频率显示了受众的细分。 图表在中间显示受众总数。 如果将鼠标悬停在受众的不同部分上，则会显示属于每种更新频率类型的受众数量。

![将显示更新频率饼图。](../images/ui/overview/update-frequency-chart.png)

### 自定义 {#customize}

您可以将附加字段添加到 [!UICONTROL 浏览] 页面，选择 ![过滤器属性图标](../images/ui/overview/filter-attribute.png). 这些附加字段包括生命周期状态、更新频率、上次更新者、描述、创建者和访问标签。

| 字段 | 描述 |
| ----- | ----------- |
| [!UICONTROL 名称] | 受众的名称。 |
| [!UICONTROL 配置文件计数] | 符合受众条件的配置文件总数。 |
| [!UICONTROL Origin] | 受众的来源。 它指明了受众的来源。 可能的值包括分段服务、自定义上传、受众组合和Audience Manager。 |
| [!UICONTROL 生命周期状态] | 受众的状态。 此字段的可能值包括 `Draft`， `Published`、和 `Archived`. |
| [!UICONTROL 更新频率] | 一个值，表示受众数据的更新频率。 此字段的可能值包括 [!UICONTROL 批次]， [!UICONTROL 流]， [!UICONTROL Edge]、和 [!UICONTROL 未计划]. |
| [!UICONTROL 上次更新者] | 上次更新受众的人员姓名。 |
| [!UICONTROL 已创建] | 创建受众的日期和时间（UTC时区）。 |
| [!UICONTROL 上次更新时间] | 上次更新受众的日期和时间(UTC)。 |
| [!UICONTROL 标记] | 属于受众的用户定义标记。 有关这些标记的详细信息，请参阅 [标记部分](#tags). |
| [!UICONTROL 描述] | 受众的描述。 |
| [!UICONTROL 创建者] | 创建受众的人员姓名。 |
| [!UICONTROL 访问标签] | 受众的访问标签。 访问标签允许您根据应用于该数据的使用策略对数据集和字段进行分类。 这些标签可随时应用，从而为您选择如何管理数据提供了灵活性。 有关访问标签的详细信息，请阅读以下文档： [管理标签](../../access-control/abac/ui/labels.md). |
| [!UICONTROL 细分] | 受众的个人资料状态细分。 此用户档案状态划分的更详细描述可以在下面找到。 |

如果选择了“划分”，则显示一个条形图，其中概述了属于以下每种已计算用户档案状态的用户档案的百分比： [!UICONTROL 已实现]， [!UICONTROL 现有]、和 [!UICONTROL 正在退出]. 此外，在页面上显示的细分 [!UICONTROL 浏览] 选项卡是对区段定义状态最准确的划分。 如果此数字与 [!UICONTROL 概述] 选项卡上，您应使用 [!UICONTROL 浏览] 制表符作为正确的信息源，因为 [!UICONTROL 概述] 选项卡编号每天只更新一次。

| 状态 | 描述 |
| ------ | ----------- |
| [!UICONTROL 已实现] | 符合以下条件的配置文件计数： **合格** 自上次运行批处理区段作业以来的24小时内的区段。 |
| [!UICONTROL 现有] | 满足以下条件的配置文件计数： **剩余** 自上次运行批处理区段作业以来的24小时内的区段中。 |
| [!UICONTROL 正在退出] | 满足以下条件的配置文件计数： **已退出** 自上次运行批处理区段作业以来的最后24小时内的区段。 |

在选择了要显示的字段后，您还可以重新调整所显示列的宽度。 可通过拖动列之间的区域或选择 ![箭头图标](../images/ui/overview/arrow-icon.png) 要重新调整大小的列的，后跟 **[!UICONTROL 调整列大小]**.

![“调整列大小”按钮会突出显示。](../images/ui/overview/browse-audience-resize-column.png)

### 筛选、文件夹和标记 {#manage-audiences}

为了提高工作效率，您可以搜索现有受众、将用户定义的标记添加到受众、将受众放入文件夹并筛选显示的受众。

**搜索**{#search}

您最多可以使用9种不同的语言搜索现有受众 [!DNL Unified Search].

使用 [!DNL Unified Search]，在突出显示的搜索栏中添加要搜索的词语。

![搜索栏会突出显示。](../images/ui/overview/browse-audience-search.png)

有关详情 [!DNL Unified Search]，包括支持的功能，请阅读 [统一搜索文档](https://experienceleague.adobe.com/docs/core-services/interface/services/search-experience-cloud.html).

**标记** {#tags}

您可以添加用户定义的标记，以更好地描述、查找和管理您的受众。

要添加标记，请选择 **[!UICONTROL 管理标记]** 标记的受众上。

![此 [!UICONTROL 管理标记] 已为指定受众选择按钮。](../images/ui/overview/browse-manage-tags.png)

此 **[!UICONTROL 管理标记]** 弹出窗口出现。 在此弹出窗口中，您可以选择已分类的标记或未分类的标记。

| 标记类型 | 描述 |
| -------- | ----------- |
| 已分类 | 由贵组织的管理员创建并管理的标记。 |
| 未分类 | 在中创建的标记 [!UICONTROL 管理标记] 弹出窗口。 任何人都可以创建或管理这些类型的标记。 |

![此 [!UICONTROL 管理标记] 此时会显示弹出框。 用于选择已分类或未分类的选项会突出显示。](../images/ui/overview/create-tag.png)

添加要附加到受众的所有标记后，选择 **[!UICONTROL 保存]**.

![在 [!UICONTROL 管理标记] 弹出窗口时，添加的标记会突出显示。](../images/ui/overview/created-tags.png)

有关创建和管理标记的更多信息，请参阅 [管理标记指南](../../administrative-tags/ui/managing-tags.md).

**文件夹** {#folders}

您可以将受众放入文件夹中，以便更好地管理受众。

要将受众移动到文件夹中，请选择 **[!UICONTROL 移至文件夹]** 对要移动的受众执行标记。

![此 [!UICONTROL 移至文件夹] 按钮可供特定受众选择。](../images/ui/overview/browse-move-to-folder.png)

此 **将受众移动到文件夹** 弹出窗口出现。 选择要将受众移动到的文件夹，然后选择 **[!UICONTROL 保存]**.

![此时会显示“将受众移动到文件夹”弹出框。 将突出显示受众将移动到的文件夹。](../images/ui/overview/move-to-folder.png)

将受众放入文件夹中后，您可以选择仅显示属于特定文件夹的受众。

![将显示属于特定文件夹的受众。](../images/ui/overview/browse-folders.png)

**过滤器** {#filter}

您还可以根据各种设置筛选受众。

要筛选可用的受众，请选择 ![过滤器图标](../images/ui/overview/filter-icon.png).

![此时会显示浏览受众页面，其中过滤器图标会突出显示。](../images/ui/overview/browse-select-filter.png)

此时将显示可用筛选器列表。

| 过滤器 | 描述 |
| ------ | ----------- |
| [!UICONTROL Origin] | 允许您根据受众的来源进行筛选。 可用选项包括分段服务、自定义上传、受众组合和Audience Manager。 |
| [!UICONTROL 具有任何标记] | 允许您按标记过滤。 您可以选择 **[!UICONTROL 具有任何标记]** 和 **[!UICONTROL 具有所有标记]**. 时间 **[!UICONTROL 具有任何标记]** 选中，则过滤的受众将包括 **任意** 已添加的标记的URL编号。 时间 **[!UICONTROL 具有所有标记]** ，则过滤的受众必须包括 **所有** 已添加的标记的URL编号。 |
| [!UICONTROL 生命周期状态] | 可让您根据受众的生命周期状态进行过滤。 可用选项包括 [!UICONTROL 活动]， [!UICONTROL 已存档]， [!UICONTROL 已删除]， [!UICONTROL 草稿]， [!UICONTROL 不活动]、和 [!UICONTROL 已发布]. |
| [!UICONTROL 更新频率] | 可让您根据受众的更新频率进行过滤。 可用选项包括 [!UICONTROL 已计划]， [!UICONTROL 连续]、和 [!UICONTROL 按需]. |
| [!UICONTROL 创建者] | 允许您根据创建受众的人员进行筛选。 |
| [!UICONTROL 创建日期] | 可让您根据受众的创建日期进行筛选。 您可以选择创建受众时要过滤的日期范围。 |
| [!UICONTROL 修改日期] | 可让您根据受众的上次修改日期进行筛选。 您可以选择上次修改受众时要过滤的日期范围。 |

![浏览受众页面上会显示并突出显示可用的筛选器。](../images/ui/overview/filter-audiences.png)

### 受众详细信息 {#audience-details}

要查看有关特定受众的更多详细信息，请在 **[!UICONTROL 浏览]** 选项卡。

此时会显示受众详细信息页面。 顶部显示了受众摘要、有关合格受众规模的信息以及激活区段的目标。

![将显示受众详细信息页面。 突出显示受众摘要、受众总数和激活的目标卡片。](../images/ui/overview/audience-details-summary.png)

**受众摘要** {#segment-summary}

此 **[!UICONTROL 受众摘要]** 部分提供属性的ID、名称、描述、来源和详细信息等信息。

此外，您还可以选择将受众激活到目标、应用访问标签或编辑/更新受众。

选择 **[!UICONTROL 激活到目标]** 允许您将受众激活到目标。 有关将受众激活到目标的更多详细信息，请参阅 [激活概述](../../destinations/ui/activation-overview.md).

![“激活到目标”按钮会突出显示。](../images/ui/overview/audience-details-activate.png)

选择 **[!UICONTROL 应用访问标签]** 允许您管理属于受众的访问标签。 有关访问标签的详细信息，请阅读以下文档： [管理标签](../../access-control/abac/ui/labels.md).

![应用访问标签按钮会突出显示。](../images/ui/overview/audience-details-access-labels.png)

>[!BEGINTABS]

>[!TAB 受众组合]

![此时将显示受众详细信息页面，其中包含 [!UICONTROL 打开合成] 按钮突出显示。](../images/ui/overview/audience-details-open-composition.png)

选择 **[!UICONTROL 打开合成]** 允许您在受众构成中查看受众。 有关受众构图的更多信息，请阅读 [受众合成UI指南](./audience-composition.md).

>[!TAB 自定义上传]

![此时将显示受众详细信息页面，其中包含 [!UICONTROL 更新受众] 按钮突出显示。](../images/ui/overview/audience-details-update-audience.png)

选择 **[!UICONTROL 更新受众]** 允许您重新上传外部生成的受众。 有关导入外部生成的受众的更多信息，请阅读以下章节： [导入受众](#import-audience).

>[!TAB Segmentation Service]

![此时将显示受众详细信息页面，其中包含 [!UICONTROL 编辑受众] 按钮突出显示。](../images/ui/overview/audience-details-edit-audience.png)

选择 **[!UICONTROL 编辑受众]** 允许您在区段生成器中编辑受众。 有关使用 [!DNL Segment Builder] 工作区，请阅读 [[!DNL Segment Builder] 用户指南](./segment-builder.md).

>[!ENDTABS]

选择 **[!UICONTROL 编辑属性]** 将允许您编辑受众的基本详细信息，如名称、描述和标记。

![](../images/ui/overview/audience-details-edit-properties.png)

**受众总数** {#audience-total}

此 **[!UICONTROL 受众总数]** 部分显示符合受众条件的配置文件总数。

通过使用当天样本数据的样本量生成预估。 如果您的配置文件存储中的实体少于100万，则使用完整数据集；对于100万到2,000万个之间的实体，使用100万个实体；而对于2000万个以上的实体，使用总实体的5%。 有关生成预计值的更多信息，请参阅 [估计值生成部分](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 受众创建教程的内容。

**激活的目标** {#activated-destinations}

此 **[!UICONTROL 激活的目标]** 部分显示激活此受众的目标。

>[!NOTE]
>
> “目标”功能适用于 [!DNL Adobe Real-Time Customer Data Platform]，并允许您将数据导出到外部平台。 欲知目标的详情，请阅读 [目标概述](../../destinations/home.md). 要了解如何将区段激活到目标，请参阅 [激活概述](../../destinations/ui/activation-overview.md).

**配置文件示例** {#profile-samples}

下面是符合区段资格的用户档案样本，详细说明以下信息： [!DNL Profile] ID、名字、姓氏和个人电子邮件。

数据采样的触发方式取决于摄取方法。

对于批量摄取，每十五分钟自动扫描一次配置文件存储区，以查看自上次采样作业运行以来是否成功摄取新批次。 如果是这种情况，随后扫描配置文件存储以查看记录数量是否至少有5%的变化。 如果满足这些条件，则会触发新的取样作业。

对于流式摄取，每小时自动扫描一次配置文件存储以确定记录数量是否至少有5%的更改。 如果满足此条件，则会触发新的取样作业。

扫描的样本大小取决于配置文件存储中的实体总数。 下表显示了这些样本量：

| 配置文件存储中的实体 | 样本量 |
| ------------------------- | ----------- |
| 少于100万 | 完整数据集 |
| 100万到2000万 | 100万 |
| 超过2000万 | 占总数的5% |

有关每个报表包的更多详细信息 [!DNL Profile] 通过选择 [!DNL Profile] 标识。 要了解有关用户档案的详细信息，请阅读 [[!DNL Real-Time Customer Profile] 用户指南](../../profile/ui/user-guide.md#profile-detail).

![受众的样本配置文件会突出显示。 配置文件信息示例包括配置文件ID、名字、姓氏和人员的电子邮件。](../images/ui/overview/audience-details-profiles.png)

### 创建受众 {#create-audience}

您可以选择 **[!UICONTROL 创建受众]** 以创建受众。

![在受众浏览页面上，创建受众按钮突出显示。](../images/ui/overview/browse-create-audience.png)

此时会出现一个弹出窗口，允许您在构成受众或构建规则之间进行选择。

![显示您可以创建的两种受众类型的弹出窗口。](../images/ui/overview/create-audience-type.png)

**受众组合** {#audience-composition}

选择 **[!UICONTROL 组合受众]** 使您转到“受众合成”。 此工作区为构建和编辑受众提供了直观的控件，例如用于表示不同操作的拖放图块。 要了解有关创建受众的更多信息，请阅读 [受众构成指南](./audience-composition.md).

![此时将显示“受众合成”工作区。](../images/ui/overview/audience-composition.png)

**区段生成器** {#segment-builder}

选择 **[!UICONTROL 生成规则]** 使您转到区段生成器。 此工作区为构建和编辑区段定义提供了直观的控件，例如用于表示数据属性的拖放图块。 要了解有关创建区段定义的更多信息，请参阅 [区段生成器指南](./segment-builder.md)

![此时将显示“区段生成器”工作区。](../images/ui/overview/segment-builder.png)

### 导入受众 {#import-audience}

您可以选择 **[!UICONTROL 导入受众]** 导入外部生成的受众。

![在受众浏览页面上，导入受众按钮突出显示。](../images/ui/overview/browse-import-audience.png)

此 **[!UICONTROL 导入受众CSV]** 此时会出现工作流。 您可以选择要导入为外部生成受众的CSV文件。

![在 [!UICONTROL 导入受众CSV] 工作流， [!UICONTROL 拖放文件] 框会突出显示，其中显示了可在何处上传外部生成的受众。](../images/ui/overview/import-audience-csv.png)

>[!NOTE]
>
>外部生成的受众 **必须** 为CSV格式，具有 **最大值** 列中，小于1 GB。

选择要导入的CSV文件后，将显示此外部生成受众的示例数据列表。 确认样本数据正确后，选择 **[!UICONTROL 下一个]**.

![将显示外部生成的受众的示例数据。](../images/ui/overview/import-audience-sample-data.png)

此 **[!UICONTROL 受众详细信息]** 页面。 您可以添加有关受众的信息，包括其名称、描述、主要身份和身份命名空间值。

导入外部生成的受众时，必须选择其中一列作为主标识字段并指定命名空间值。 请注意，将考虑其余所有字段 **有效负载属性**. 这些属性会被考虑在内 **非持久**，因为它们将仅与此受众关联以进行个性化，并且 **非** 已连接到配置文件。

![此 [!UICONTROL 受众详细信息] 页面。](../images/ui/overview/import-audience-audience-details.png)

填写受众详细信息后，选择 **[!UICONTROL 下一个]**.

![此 [!UICONTROL 下一个] 按钮会高亮显示 [!UICONTROL 受众详细信息] 页面。](../images/ui/overview/import-audience-filled-details.png)

此 **[!UICONTROL 审核]** 页面。 您可以查看新导入的外部生成受众的详细信息。

![此 [!UICONTROL 审核] 此时将显示页面，其中显示新导入的外部生成受众的详细信息。](../images/ui/overview/import-audience-review-details.png)

确认详细信息正确后，选择 **[!UICONTROL 完成]** 将外部生成的受众导入Adobe Experience Platform。

>[!IMPORTANT]
>
>默认情况下，外部生成的受众的数据过期时间为30天。 如果以任何方式更新或修改受众，则会重置数据过期时间。
>
>此外，如果您的外部生成的受众包含敏感信息和/或医疗保健相关信息， **必须** 在将数据激活到任何目标之前，请应用必需的数据使用标签。 有关应用数据使用标签的更多信息，请阅读以下文档： [管理标签](../../access-control/abac/ui/labels.md).

## 计划分段 {#scheduled-segmentation}

创建受众后，您可以通过按需评估或计划（连续）评估来评估受众。 评估方法移动 [!DNL Real-Time Customer Profile] 数据通过区段作业来生成相应的受众。 创建受众后，将保存并存储这些受众，以便可以使用导出它们 [!DNL Experience Platform] API。

按需评估包括使用API执行评估并根据需要构建受众，而计划评估（也称为“计划分段”）允许您创建定期计划以在特定时间（最多，每天一次）评估受众。

### 启用计划分段 {#enable-scheduled-segmentation}

可以使用UI或API启用受众进行计划评估。 在UI中，返回到 **[!UICONTROL 浏览]** 选项卡范围 **[!UICONTROL 受众]** 并打开 **[!UICONTROL 计划所有受众]**. 这将导致根据贵组织设置的计划评估所有受众。

>[!NOTE]
>
>可以为最多具有五(5)个合并策略的沙盒启用计划评估。 [!DNL XDM Individual Profile]. 如果贵组织的合并策略超过5个，则 [!DNL XDM Individual Profile] 在单个沙盒环境中，您将无法使用计划的评估。

当前只能使用API创建计划。 有关使用API创建、编辑和使用计划的详细步骤，请按照教程中的说明来评估和访问分段结果，特别是以下部分： [使用API的计划评估](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![在受众浏览页面上，切换到“计划所有受众”会突出显示。](../images/ui/overview/browse-audiences-scheduled.png)

## 合成 {#compositions}

选择 **[!UICONTROL 合成]** 选项卡，查看通过受众构成为您的组织生成的所有受众的列表。

![在受众构成中为您的组织创建的受众列表。](../images/ui/overview/compositions.png)

默认情况下，此视图会列出有关受众的信息，包括名称、状态、创建日期、创建者、上次更新日期和上次更新者。

您可以选择 ![自定义表](../images/ui/overview/customize-table.png) 图标以更改显示的字段。

![自定义表格按钮会突出显示。 选择此按钮允许您自定义在受众组合页面上显示的字段。](../images/ui/overview/compositions-select-customize-table.png)

此时会出现一个弹出窗口，其中列出了可在该表中显示的所有字段。

![可以为“构成”部分显示的属性。](../images/ui/overview/compositions-customize-table.png)

| 字段 | 描述 |
| ----- | ----------- | 
| [!UICONTROL 名称] | 受众的名称。 |
| [!UICONTROL 状态] | 受众的状态。 此字段的可能值包括 `Draft`， `Published`、和 `Archived`. |
| [!UICONTROL 已创建] | 创建受众的时间和日期。 |
| [!UICONTROL 创建者] | 创建受众的人员姓名。 |
| [!UICONTROL 更新] | 上次更新受众的时间和日期。 |
| [!UICONTROL 更新者] | 上次更新受众的人员姓名。 |

要查看受众的构成方式，请在左侧导航栏中选择受众的名称， [!UICONTROL 受众] 选项卡。

此时将显示“受众构成”页面，其中包含构成受众的构建基块。 有关如何使用受众构图的更多详细信息，请参阅 [受众合成UI指南](./audience-composition.md).

## 流式客户细分 {#streaming-segmentation}

流式分段是在以下项上进行分段的能力 [!DNL Platform] 近乎实时，同时专注于数据丰富性。 借助流式分段，现在可以在数据进入时进行分段鉴别 [!DNL Platform]，从而无需安排和运行分段作业。

有关流式客户细分的更多信息，请参阅 [流式分段用户指南](./streaming-segmentation.md).

>[!NOTE]
>
>为了使流式分段正常工作，您需要为组织启用计划分段。 有关启用计划分段的详细信息，请参阅 [本用户指南中的流分段部分](#scheduled-segmentation).

## 边缘分段 {#edge-segmentation}

边缘分段能够在边缘即时评估Platform中的受众，启用同一页面和下一页面个性化用例。

有关边缘分段的更多信息，请参阅 [边缘分段UI指南](./edge-segmentation.md)

## 策略违规

>[!NOTE]
>
>策略违规仅适用于创建已分配给目标的受众。

创建完受众后，Adobe Experience Platform数据管理将分析受众，以确保受众内没有违反策略的情况。 请参阅 [数据管理概述](../../data-governance/home.md) 以了解更多信息。

![将显示受众的策略违规。](../images/ui/overview/audience-dule-policy-violations.png)

## 后续步骤和其他资源 {#next-steps}

此 [!DNL Segmentation Service] UI提供了一个丰富的工作流，允许您从创建可营销受众 [!DNL Real-Time Customer Profile] 数据。

要了解有关 [!DNL Segmentation Service]，请继续阅读文档。 要了解如何使用 [!DNL Segmentation Service] API，请阅读 [[!DNL Segmentation Service] 开发人员指南](../api/overview.md).
