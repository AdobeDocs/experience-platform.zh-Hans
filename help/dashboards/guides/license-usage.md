---
keywords: Experience Platform；用户界面；UI；自定义；许可证使用仪表板；仪表板；许可证使用；权利；使用
title: 许可证使用情况仪表板
description: Adobe Experience Platform提供了一个功能板，通过该功能板可查看有关贵组织许可证使用情况的重要信息。
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 62f5ecf82df46284365e64d633c8242ac45567bc
workflow-type: tm+mt
source-wordcount: '3455'
ht-degree: 38%

---

# 许可证用量仪表板 {#license-usage-dashboard}

>[!CONTEXTUALHELP]
>id="testy-mctestface"
>title="不应显示的测试对话框"
>abstract="正在{date}上查看对象{name}。"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_core"
>title="核心产品表"
>abstract="表中列出的核心产品在沙盒级别有各自的量度、使用情况跟踪和钻取视图。这些核心产品提供了用于跟踪的关键量度，并且任何附加组件都包含在这些量度中。"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_addons"
>title="附加组件表"
>abstract="附加组件表列出了许可证数量与核心产品支持的量度相结合的产品。这些附加组件没有单独的量度，但增强了与其关联的核心产品的使用情况跟踪功能。"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage"
>title="许可证用量仪表板"
>abstract="通过许可证用量仪表板，可了解已购买的 Adobe Experience Platform 产品。该仪表板概述显示产品的主要量度，包括您对每个主要量度的用量以及您的合同许可证数量。详细信息工作区显示特定沙盒中每个产品的量度细分。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="自动数据集过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_licenseusage"
>title="许可证用量仪表板"
>abstract="通过许可证用量仪表板，可了解已购买的 Adobe Experience Platform 产品。该仪表板概述显示产品的主要量度，包括您对每个主要量度的用量以及您的合同许可证数量。详细信息工作区显示特定沙盒中每个产品的量度细分。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="自动数据集过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_computehours"
>title="预测计算小时数"
>abstract="“计算小时数”衡量查询服务引擎在运行批量查询时读取、处理和写入数据所花费的时间。<br>您的使用量可能已达到已授予许可量。要评估或减少使用情况，请前往查询>日志以查看您的查询历史记录。如果您无权访问查询工作区，请联系您的管理员。"
>additional-url="https://experience.adobe.com/#/platform/query/log.html" text="查询日志工作区"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_addressableaudience"
>title="预测的可寻址受众"
>abstract="可寻址受众是您的组织有权参与的实时客户轮廓中的一组个人轮廓。该量度包括直接可识别的轮廓和假名轮廓。<br>您的使用量可能已达到已授予许可量。为了减少使用量，请配置数据集或假名轮廓数据过期时间。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="体验事件过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_engageableprofiles"
>title="预测的可参与的轮廓"
>abstract="可参与轮廓是指您的组织在过去 12 个月内尝试使用 Journey Optimizer 进行互动的实时客户轮廓中的个人轮廓。<br>您的使用量可能已达到已授予许可量。为了减少使用量，请配置数据集或假名轮廓数据过期时间。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="体验事件过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_businesspersonprofile"
>title="预测的商务人士轮廓"
>abstract="商业人士轮廓是实时客户轮廓中代表 B2B 环境中个人的记录。<br>您的使用量可能已达到已授予许可量。为了减少使用量，请配置数据集或假名轮廓数据过期时间。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="体验事件过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_corehours"
>title="预测的核心小时数"
>abstract="核心小时数表示 Experience Platform 各项服务所消耗的处理时间。<br>您的使用量可能已达到已授予许可量。为了减少使用量，请配置数据集或假名轮廓数据过期时间。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="体验事件过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_totaldatavolume"
>title="预测的总数据量"
>abstract="”总数据量“是指实时客户轮廓中可用于互动和个性化工作流程的数据量。<br>您的使用量可能已达到已授予许可量。为了减少使用量，请配置数据集或假名轮廓数据过期时间。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="体验事件过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_cjaRowsAvailable"
>title="预测的 CJA 可用行"
>abstract="可用的 Customer Journey Analytics 行数指的是可供在 Customer Journey Analytics 中分析的数据的每日平均行数。<br>您的使用量可能已达到已授予许可量。为了减少使用量，请配置数据集或假名轮廓数据过期时间。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="体验事件过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_addressableaudience"
>title="预测的可寻址受众"
>abstract="可寻址受众是您的组织有权参与的实时客户轮廓中的一组个人轮廓。这包括直接可识别的轮廓和假名轮廓。<br>您的使用量已超出许可量。为了减少使用量，请配置数据集或假名轮廓数据过期时间。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="体验事件过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_engageableprofiles"
>title="预测的可参与的轮廓"
>abstract="可参与轮廓是指您的组织在过去 12 个月内尝试使用 Journey Optimizer 进行互动的实时客户轮廓中的个人轮廓。<br>您的使用量已超出许可量。为了减少使用量，请配置数据集或假名轮廓数据过期时间。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="体验事件过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_businesspersonprofile"
>title="预测的商务人士轮廓"
>abstract="商业人士轮廓是实时客户轮廓中代表 B2B 环境中个人的记录。<br>您的使用量已超出许可量。为了减少使用量，请配置数据集或假名轮廓数据过期时间。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="体验事件过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_corehours"
>title="预测的核心小时数"
>abstract="核心小时数表示 Experience Platform 各项服务所消耗的处理时间。<br>您的使用量已超出许可量。为了减少使用量，请配置数据集或假名轮廓数据过期时间。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="体验事件过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_totaldatavolume"
>title="预测的总数据量"
>abstract="”总数据量“是指实时客户轮廓中可用于互动和个性化工作流程的数据量。<br>您的使用量已超出许可量。为了减少使用量，请配置数据集或假名轮廓数据过期时间。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="体验事件过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_cjaRowsAvailable"
>title="预测的 CJA 可用行"
>abstract="可用的 Customer Journey Analytics 行数指的是可供在 Customer Journey Analytics 中分析的数据的每日平均行数。<br>您的使用量已超出许可量。为了减少使用量，请配置数据集或假名轮廓数据过期时间。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html" text="体验事件过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

您可以通过Adobe Experience Platform [!UICONTROL 许可证使用情况]仪表板查看有关贵组织许可证使用情况的重要信息。 此处显示的信息是在Experience Platform实例的每日快照期间捕获的。

许可证使用情况报告提供了高度的粒度。 大多数量度是在多个产品之间共享的，反映的是使用它们的所有产品的汇总使用情况，而不是按产品计算的总数。 功能板提供这些指标在所有生产或开发沙盒中的综合使用情况，以及特定沙盒的使用情况指标。 可以使用使用情况量度跟踪以下Experience Platform应用程序：Real-Time Customer Data Platform、Adobe Journey Optimizer和Customer Journey Analytics。

本指南概述如何在UI中访问和使用许可证使用情况仪表板，并提供有关仪表板中显示的可视化的更多信息。

有关Experience Platform UI的一般概述，请参阅[Experience Platform UI指南](../../landing/ui-guide.md)。

## [!UICONTROL 许可证使用情况]仪表板数据

[!UICONTROL 许可证使用情况]仪表板显示您已购买的所有Experience Platform产品以及这些产品的任何加载项的列表。 在此功能板中，您可以找到贵组织在任何关联沙盒中用于Experience Platform的许可证相关数据的快照。

此仪表板中的数据与拍摄快照的特定时间点所显示的数据完全相同。 它不是近似值或示例，但仪表板不会实时更新。

>[!NOTE]
>
>功能板中的大多数量度每天都会根据Experience Platform实例的快照进行更新。 [!UICONTROL 可用的CJA行数]是一个异常，每月更新一次。 标记为“包”的量度，如[!UICONTROL Adhoc Query Service Users Packs]、[!UICONTROL Profile Richness No of Packs]和[!UICONTROL Streaming Segmentation No of Packs]，可反映附加组件产品的许可证权利，且不会跟踪日常使用情况。 在拍摄下一个快照之前，在快照之后所做的更改不可见。

## 浏览许可证使用情况仪表板 {#explore}

要导航到Experience Platform UI中的许可证使用情况仪表板，请在左边栏中选择&#x200B;**[!UICONTROL 许可证使用情况]**。 仪表板包含两个选项卡：**[!UICONTROL Metrics]**&#x200B;和&#x200B;**[!UICONTROL Products]**。

>[!NOTE]
>
>默认情况下，许可证使用情况仪表板未启用。 必须向用户授予“查看许可证使用情况仪表板”权限才能查看仪表板。 有关授予访问权限的步骤，请参阅[仪表板权限指南](../permissions.md)。

## [!UICONTROL 量度]选项卡 {#metrics-tab}

**[!UICONTROL 量度]**&#x200B;选项卡提供了整个组织内所有许可证使用量度的集中视图。 由于大多数量度在产品之间共享，因此这些量度没有单独的按产品细分。

度量表包含以下列：

| 列名 | 描述 |
|---|---|
| **[!UICONTROL 量度名称]** | 许可证使用量度的名称。 每个条目都包含一个信息图标(`ⓘ`)，该图标显示相关产品的说明和列表。 |
| **[!UICONTROL 已许可]** | 您的组织有权使用的单位数（在合同中定义）。 此量度与“产品”选项卡中的&#x200B;**许可证数量**&#x200B;的值相同。 |
| **[!UICONTROL 已测量]** | 您的组织当前使用的量度数量。 |
| **[!UICONTROL 使用情况%]** | 当前使用的许可值的百分比。 |
| **[!UICONTROL 预测的使用率%]** | 未来6周内量度使用的预测范围。 |

使用&#x200B;**[!UICONTROL 生产]**&#x200B;或&#x200B;**[!UICONTROL 开发]**&#x200B;沙盒切换开关筛选沙盒显示的量度。

>[!NOTE]
>
>使用情况报告按沙盒类型累计。 选择[!UICONTROL 生产]或[!UICONTROL 开发]将显示该类型的所有沙盒的组合使用情况。

![许可证使用情况仪表板的“量度”选项卡显示量度、许可证金额和使用数据列表。](../images/license-usage/metrics-tab.png)

>[!WARNING]
>
>必须在沙盒级别指定查看许可证使用情况仪表板的权限。 向每个沙盒添加权限，以便在功能板中查看它们。 此限制将在未来版本中解决。 同时，提供以下解决方法：
>
>1. 在Adobe Admin Console中创建产品配置文件。
>2. 在沙盒类别中的权限下，添加您希望在许可证使用情况仪表板中查看的所有沙盒。
>3. 在“用户仪表板权限”类别下，添加“查看许可证使用情况仪表板”权限。

### 查看量度详细信息 {#view-metric-details}

要查看特定量度的使用情况详细信息，请在列表中选择量度名称。 此时将显示指标的详细视图，其中包括：

- 显示一段时间内的使用情况的历史折线图
- 许可值和测量值的比较
- 按单个沙盒的使用情况
- 用于筛选数据的沙盒选择器
- 用于CSV下载的导出选项

此可视化允许您跟踪趋势，了解每个沙盒对总体使用率的贡献情况，并导出数据以供离线分析。

每个图表都包含用于筛选数据的下拉菜单。 使用日期范围下拉菜单调整回看时段（默认：过去30天），或使用沙盒下拉菜单查看特定生产或开发沙盒的使用情况。

![包含历史使用图形、沙盒表和导出按钮的可寻址受众量度详细信息视图。](../images/license-usage/metric-details-view.png)

您还可以选择&#x200B;**[!UICONTROL 自定义日期]**&#x200B;以选择显示的时间段。

![突出显示自定义日期范围选项的“许可证使用情况”仪表板的“概述”选项卡。](../images/license-usage/custom-date-range.png)

### CSV导出 {#export-metric-usage-data}

您可以直接从量度详细信息视图将选定量度和沙盒的历史使用数据导出为CSV文件。 选择&#x200B;**[!UICONTROL 导出]**&#x200B;图标以表格格式下载图表数据。 利用导出的CSV，可轻松分析离线趋势或在团队之间共享使用见解。

## [!UICONTROL 产品]选项卡 {#products-tab}

**[!UICONTROL 产品]**&#x200B;选项卡显示按购买的产品和任何关联的加载项分组的许可证使用数据。 [!UICONTROL Products]选项卡包含两个表：

- **[!UICONTROL 核心产品]表**：此表列出了您的组织许可的主要Adobe Experience Platform产品。 每个产品都列出了其主要量度、使用情况跟踪和预测使用情况。
- **[!UICONTROL 附加组件]表**：列出许可证金额对核心产品量度有贡献的附加项目。 加载项没有单独的量度，但可增强对其关联核心产品的使用跟踪。

| 列名 | 描述 |
|---|---|
| **[!UICONTROL 产品]** | 由您的组织许可的Adobe解决方案。 |
| **[!UICONTROL 主要指标]** | 用于跟踪该产品的主要指标。 |
| **[!UICONTROL 许可证数量]** | 主要指标的最大值的约定值。 |
| **[!UICONTROL 用法]** | 您使用的主要量度的数量。 |
| **[!UICONTROL 使用情况%]** | 根据您的许可证数量使用的主要量度的百分比。 |
| **[!UICONTROL 预测的使用量]** | 主要量度的预测使用百分比。 |

>[!NOTE]
>
>加载项的[!UICONTROL 许可证金额]包含在核心产品的总许可证金额中。 加载项不会单独进行跟踪，但可以增强其关联产品的功能。 例如，如果您购买一包5个沙盒作为附加产品，则金额将添加到基础产品的金额中。 加载项表显示特定于加载项的[!UICONTROL 许可证金额]，但实际使用情况是通过基本产品进行跟踪的。

![许可证使用情况仪表板的“产品”选项卡，其中包含核心产品和加载项的表格。](../images/license-usage/products-tab.png)

### 预测使用量 {#predicted-usage}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage_prediction"
>title="预测使用量"
>abstract="预测基于过去 6-7 个月的使用情况，并每周五生成一次。请注意, 许可证使用预测是基于过去使用情况的近似值。您有责任了解您组织的实际使用情况，并确保使用不超出您与 Adobe 的许可证范围。为了减少使用量，您可以为沙箱和数据集配置数据集或匿名轮廓的数据有效期限设置。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="自动数据集过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

>[!CONTEXTUALHELP]
>id="platform_licenseusage_prediction"
>title="预测使用量"
>abstract="预测基于过去 6-7 个月的使用情况，并在每个月的 15 日生成。请注意, 许可证使用预测是基于过去使用情况的近似值。您有责任了解您组织的实际使用情况，并确保使用不超出您与 Adobe 的许可证范围。为了减少使用量，您可以为沙箱和数据集配置数据集或匿名轮廓的数据有效期限设置。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="自动数据集过期"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html" text="假名轮廓数据过期"

通过准确、最新的使用预测主动管理和优化您的许可资源。 [!UICONTROL 预测的使用量]列预测所有已购产品的所有生产和开发沙盒中沙盒级别的未来许可证使用量。 现在，预测每周更新，根据最新的使用情况数据提供六周的预测。 每个预测包括下限和上限以支持知情规划。

>[!IMPORTANT]
>
>预测每周五更新。 刷新日期包含在信息图标（![此信息图标）中。](../images/license-usage/info-icon.png))位于列标题上方。

从[!UICONTROL 核心产品]表下的[!UICONTROL 产品]选项卡查看产品权利使用情况的摘要。

![产品及预测使用列突出显示的[!UICONTROL 许可证使用情况][!UICONTROL 产品]选项卡。](../images/license-usage/product-predicted-usage.png)

>[!NOTE]
>
>请注意, 许可证使用预测是基于过去使用情况的近似值。您有责任了解贵组织的实际使用情况，并确保使用情况不会超出贵组织获得Adobe许可证的范围。

预计使用率的百分比确定如下：

- 如果下限和上限有显着差异，则它们将显示为范围（例如，32% - 35%）。
- 如果下限和上限几乎完全相同且不为零，则它们将显示为近似值（例如，~34%）。
- 如果下限和上限几乎完全相同且为零，则它们将显示为0%。

>[!NOTE]
>
>在此上下文中，“几乎相同”意味着值对于小数点两位具有统计意义（例如，0.342的下限和0.344的上限都舍入到34%）。

预测的使用量功能支持以下量度：

- [!UICONTROL 可寻址受众]
- [!UICONTROL 业务人员配置文件]
- [!UICONTROL 计算小时数]
- [!UICONTROL 客户历程受众行数]
- [!UICONTROL 可参与的配置文件]
- [!UICONTROL 总数据量]

## 可用量度 {#available-metrics}

>[!IMPORTANT]
>
>从8月20日开始，有权使用“[!UICONTROL 平均配置文件丰富度]”和“[!UICONTROL 总存储量]”的客户在“许可证使用情况”仪表板中看到了“[!UICONTROL 总数据量]”。 客户权利没有变化，只是简化了跟踪量度。 [!UICONTROL 总数据量]表示参与和个性化工作流的实时客户配置文件中可用的数据。 此简化的量度改进了实时客户配置文件使用的管理和测量。 我们鼓励客户联系其Adobe代表，以进一步了解此更改。

许可证使用情况仪表板报告适用于组织中多个产品的多个唯一量度。 可用的量度包括：

| 量度 | 描述 |
|---|---|
| [!UICONTROL Audience Activation大小] | 一年内激活到任何基于文件的目标的轮廓的总大小。注意：这不包括通过流式处理目标发送的轮廓。 |
| [!UICONTROL 可寻址受众] | 您的组织有权参与的Real-time Customer Profile中的人员配置文件集，包括直接可识别的配置文件和假名配置文件。 这些配置文件可能包含属性、行为和区段成员资格数据。 配置文件卷使用Adobe Experience Platform的默认确定性标识图进行计算，并被视为共享功能。 |
| [!UICONTROL 临时查询服务用户包] | 一个附加组件，用于增加您授权的并发查询服务用户权利，每个包可增加五个并发查询服务用户和一个并发运行的额外临时查询。可授权多个额外的临时查询用户包。 |
| [!UICONTROL 平均配置文件丰富度] | **已弃用** — 在任何时间点存储在中心配置文件服务中的所有生产数据的总和除以授权的业务人员配置文件数量的五倍。 [!UICONTROL 平均配置文件丰富度]是共享功能。 |
| [!UICONTROL CJA行可用] | Customer Journey Analytics 中可供分析的每日平均数据行数。 |
| [!UICONTROL 计算属性] | 整合的配置文件行为数据，该数据基于转换为配置文件属性并可以包含在人员配置文件中的体验事件。 |
| [!UICONTROL 使用者受众] | 销售订单上标识为“消费者受众”的人员配置文件数。 |
| [!UICONTROL 数据导出大小] | 一年内通过激活数据集发送的数据量。 |
| [!UICONTROL 数据导出] | 一年内可导出到任何非 Adobe 解决方案（直接或间接）的数据集的总大小。 |
| [!UICONTROL 数据湖存储] | Adobe Experience Platform 中存储的分析数据的使用数量。 |
| [!UICONTROL 可参与受众] | 在过去的12个月中，您尝试使用Journey Optimizer的创作、决策、交付、试验或编排功能参与的一组Real-time Customer Profile人员配置文件。 |
| [!UICONTROL 相似受众] | 消费者相似受众是通过建模现有消费者受众以识别具有相似属性或行为的人员配置文件而生成的受众。 |
| [!UICONTROL AMM模型数] | 用于根据您的投资衡量和/或预测指定结果的机器学习模型（内置于 Adobe Mix Modeler）的计数。 |
| [!UICONTROL 沙盒数] | 访问 Adobe Experience Platform 的任何 Adobe 按需服务实例中隔离数据和操作的逻辑分离数。 |
| [!UICONTROL 包的配置文件丰富度] | 对于每个额外的轮廓丰富度包，每个轮廓的授权总数据量将增加 25 KB。 |
| [!UICONTROL 查询服务计算小时数] | 执行批量查询时，查询服务引擎读取、处理数据并将数据写回到数据湖所需的时间量。 |
| [!UICONTROL 流式分段数（包）] | 当新数据通过流式处理流程进入分段服务时，包会更新个人轮廓的区段会员资格。区段会员资格是根据当前个人轮廓属性和当前事件的值进行评估的，而不考虑历史行为。流式分段是一项共享功能。 |
| [!UICONTROL 总数据量] | 可用于参与工作流中的实时客户个人资料的数据总量。 总数据量使用以下公式计算： **总数据量=可寻址受众×平均配置文件丰富度**。 此量度反映仅存储在配置文件存储中的数据，并排除数据湖存储。 它提供了与基于用户档案的参与相关的更集中的数据视图。 请参阅有关总数据量](../../landing/license-usage-and-guardrails/total-data-volume.md)的[常见问题解答，以了解更多信息。 |
| [!UICONTROL 总数据输出量] | 从Adobe Experience Platform导出到第三方数据仓库的累积年数据量。 |

<!-- |  [!UICONTROL Sandbox No of Packs] |  A logical separation within your instance of any Adobe On-demand Service that accesses Adobe Experience Platform isolating data and operations | -->

>[!TIP]
>
>您可以检查销售订单中的许可证权利以计算指标，如“存储容量”。<br>例如，<ul><li>存储容量=合同中“授权配置文件”的数量X平均配置文件丰富度</li></ul>

这些指标的可用性和每个指标的特定定义因贵组织购买的许可而异。 有关每个量度的详细定义，请参阅相应的产品描述文档：

| 许可证 | 产品描述 |
| --- | --- |
| <ul><li>Adobe Experience Platform：OD LITE</li><li>Adobe Experience Platform：OD STANDARD</li><li>Adobe Experience Platform：OD粗</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform：OD</li></ul> | [Experience Platform、应用程序服务和智能服务](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT CUSTOMER DATA PLATFORM：OD</li><li>RT客户数据平台：OD PRFL到10M</li><li>RT客户数据平台：OD PRFL到50M</li></ul> | [Adobe Real-Time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP：OD激活</li><li>AEP：OD激活PRFL至10M</li><li>AEP：OD激活PRFL，最长可达50M</li></ul> | [Adobe Experience Platform激活](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP：OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>Journey Optimizer SELECT：OD</li><li>Journey Optimizer PRIME：OD</li><li>Journey Optimizer ULTIMATE：OD</li><li>UNP AJO PRIME STARTER：OD</li><li>UNP AJO ULTIMATE STARTER：OD</li><li>UNP Real-Time CDP：OD配置文件编排</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/cn/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>许可证使用仪表板仅报告为您的组织配置的最新许可证。 如果为贵组织配置的最新许可证未在上表中显示，则许可证使用情况仪表板可能无法正确显示。 计划在未来的版本中，支持单个组织中的其他许可证和多个许可证。

## 后续步骤

阅读本文档后，您可以找到许可证使用情况仪表板，并查看每个已购产品、所有生产或开发沙盒以及特定沙盒的使用量度。 您可以根据贵组织购买的许可协议，查找有关贵组织可用量度的更多信息。

要了解有关Experience Platform UI中其他可用功能的更多信息，请参阅[Experience Platform UI指南](../../landing/ui-guide.md)。
