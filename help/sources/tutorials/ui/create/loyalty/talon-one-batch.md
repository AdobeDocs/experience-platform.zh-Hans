---
title: 使用UI将批量数据从Talon.One引入到Experience Platform
description: 了解如何使用UI将批量数据从Talon.One摄取到Adobe Experience Platform。 本指南介绍设置、数据选择和数据流配置。
badge: Beta 版
hide: true
hidefromtoc: true
source-git-commit: 558a9d6ff3222acbf77edea0a82ef50725cd6203
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 1%

---

# 使用UI将批次数据从[!DNL Talon.One]摄取到Experience Platform

>[!AVAILABILITY]
>
>[!DNL Talon.One]源为测试版。 有关使用测试版标记源的更多信息，请阅读源概述中的[条款和条件](../../../../home.md#terms-and-conditions)。

阅读本教程，了解如何使用UI中的源工作区将批次数据从[!DNL Talon.One]帐户摄取到Adobe Experience Platform中。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

>[!IMPORTANT]
>
>请阅读[[!DNL Talon.One] 概述](../../../../connectors/loyalty/talon-one.md)，了解将帐户连接到Experience Platform之前需要完成的先决步骤。

## 导航源目录

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;*[!UICONTROL 源]*&#x200B;工作区。 在&#x200B;*[!UICONTROL 类别]*&#x200B;面板中选择相应的类别。 或者，使用搜索栏导航到要使用的特定源。

要从[!DNL Talon.One]中摄取数据，请在&#x200B;**[!UICONTROL 忠诚度]**&#x200B;下选择&#x200B;*[!UICONTROL Talon.One批次Source连接器]*&#x200B;源卡，然后选择&#x200B;**[!UICONTROL 添加数据]**。

>[!TIP]
>
>当给定的源尚未具有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL 设置]**&#x200B;选项。 创建经过身份验证的帐户后，此选项将更改为&#x200B;**[!UICONTROL 添加数据]**。

![已选择Talon.One批次源连接器卡的源目录。](../../../../images/tutorials/create/talon-one-batch/catalog.png)

### 创建新帐户

要为您的[!DNL Talon.One]源创建新帐户，请选择&#x200B;**[!UICONTROL 新建帐户]**，并为您的帐户提供名称和可选描述。 接下来，提供您的[!DNL Talon.One]域和[!UICONTROL Talon.One管理API密钥]。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，等待一段时间以建立连接。

![源工作流的创建新帐户步骤。](../../../../images/tutorials/create/talon-one-batch/new.png)

### 使用现有帐户

要使用现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后从帐户界面中选择要使用的[!DNL Talon.One]帐户。

## 选择数据

完成身份验证后，请提供您的&#x200B;**applicationId**&#x200B;和&#x200B;**sessionType**&#x200B;的值。 在此步骤中，您可以使用预览功能检查数据的结构。 完成后，选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![源工作流的选择数据和预览步骤。](../../../../images/tutorials/create/talon-one-batch/select-data.png)

## 配置数据集和数据流详细信息

接下来，您必须提供有关数据集和数据流的信息。

### 数据集详细信息

数据集是用于数据集合的存储和管理结构，通常是表格，其中包含架构（列/字段）和记录（行）。 成功引入Experience Platform的数据将作为数据集保留在数据湖中。

在此步骤中，您可以使用现有数据集或创建新数据集。

>[!NOTE]
>
>无论您是使用现有数据集还是创建新数据集，都必须确保为配置文件&#x200B;**引入启用数据集**。

+++选择相关步骤以启用配置文件摄取、错误诊断和部分摄取。

如果您的数据集启用了实时客户个人资料，那么在此步骤中，您可以切换&#x200B;**[!UICONTROL 个人资料数据集]**&#x200B;以启用您的数据以进行个人资料摄取。 您还可以使用此步骤启用&#x200B;**[!UICONTROL 错误诊断]**&#x200B;和&#x200B;**[!UICONTROL 部分摄取]**。

* **[!UICONTROL 错误诊断]**：选择&#x200B;**[!UICONTROL 错误诊断]**&#x200B;以指示源生成错误诊断，以便以后在监视数据集活动和数据流状态时可以引用这些诊断。
* **[!UICONTROL 部分摄取]**：部分批次摄取是摄取包含错误的数据的能力，最多可摄取特定可配置阈值。 此功能允许您成功地将所有准确的数据提取到Experience Platform中，同时将所有不正确的数据与有关其无效原因的信息单独进行批处理。

+++

## 数据流详细信息

配置数据集后，您必须提供有关数据流的详细信息，包括名称、可选描述和警报配置。

![数据流详细信息接口。](../../../../images/tutorials/create/talon-one-batch/dataflow-detail.png)

| 数据流配置 | 描述 |
| --- | --- |
| 数据流名称 | 数据流的名称。 默认情况下，这将使用正在导入的文件的名称。 |
| 描述 | （可选）数据流的简短说明。 |
| 警报 | Experience Platform可生成用户可以订阅的基于事件的警报，这些选项允许正在运行的数据流触发这些警报。  有关详细信息，请阅读[警报概述](../../alerts.md) <ul><li>**源数据流运行开始**：选择此警报以在数据流运行开始时接收通知。</li><li>**源数据流运行成功**：选择此警报以在数据流结束且没有任何错误时接收通知。</li><li>**源数据流运行失败**：选择此警报以在数据流运行结束时发生任何错误时接收通知。</li></ul> |

{style="table-layout:auto"}

## 映射

配置数据集和数据流详细信息后，您现在可以继续将源数据字段映射到其相应的目标XDM字段。 在将数据摄取到Experience Platform之前，使用映射界面将源数据映射到相应的架构字段。 有关详细信息，请阅读UI[中的](../../../../../data-prep/ui/mapping.md)映射指南。

>[!IMPORTANT]
>
>有关映射[!DNL Talon.One]源数据的其他指导，请阅读[[!DNL Talon.One] 概述](../../../../connectors/loyalty/talon-one.md#mapping)。

![源工作流的映射接口。](../../../../images/tutorials/create/talon-one-batch/mapping.png)

## 计划数据流摄取

出现[!UICONTROL 计划]步骤。 使用界面配置摄取计划，以使用配置的映射自动摄取选定的源数据。 默认情况下，计划设置为`Once`。 要调整您的摄取频率，请选择&#x200B;**[!UICONTROL 频率]**，然后从下拉菜单中选择一个选项。

>[!TIP]
>
>间隔和回填在一次性摄取期间不可见。

如果将摄取频率设置为`Minute`、`Hour`、`Day`或`Week`，则必须设置一个间隔，以便在每次摄取之间建立一个设置的时间范围。 例如，摄取频率设置为`Day`，间隔设置为`15`意味着您的数据流计划每15天摄取一次数据。

在此步骤中，您还可以启用&#x200B;**回填**&#x200B;并为增量数据摄取定义列。 回填用于摄取历史数据，而您为增量摄取定义的列允许从现有数据中区分新数据。

有关计划配置的详细信息，请参阅下表。

| 计划配置 | 描述 |
| --- | --- |
| 频率 | 配置频率以指示数据流运行的频率。 您可以将频率设置为： <ul><li>**一次**：将频率设置为`once`以创建一次性引入。 创建一次性摄取数据流时，间隔和回填配置不可用。 默认情况下，调度频率设置为一次。</li><li>**分钟**：将频率设置为`minute`，以计划数据流以每分钟摄取数据。</li><li>**小时**：将频率设置为`hour`，以计划数据流每小时摄取数据。</li><li>**天**：将频率设置为`day`，以计划数据流每天摄取数据。</li><li>**周**：将频率设置为`week`，以计划数据流每周摄取数据。</li></ul> |
| 间隔 | 选择频率后，可以配置间隔设置以建立每次引入之间的时间范围。 例如，如果将频率设置为天并将间隔配置为15，则数据流将每15天运行一次。 不能将间隔设置为零。 每个频率的最小接受间隔值如下：<ul><li>**一次**：不适用</li><li>**分钟**： 15</li><li>**小时**： 1</li><li>**天**： 1</li><li>**周**： 1</li></ul> |
| 开始时间 | 预计运行的时间戳，以UTC时区显示。 |
| 回填 | 回填可确定最初摄取的数据。 如果启用了回填，则指定路径中的所有当前文件将在第一次计划摄取期间摄取。 如果禁用回填，则只摄取在第一次引入运行到开始时间之间加载的文件。 将不会摄取在开始时间之前加载的文件。 |

![源工作流的计划配置步骤。](../../../../images/tutorials/create/talon-one-batch/scheduling.png)

## 审查

此时将显示&#x200B;*[!UICONTROL 审核]*&#x200B;步骤，允许您在创建数据流之前查看其详细信息。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示帐户名、源平台和源名。
* **[!UICONTROL 分配数据集并映射字段]**：显示目标数据集和数据集所遵循的架构。

确认详细信息正确后，选择&#x200B;**[!UICONTROL 完成]**。

![源工作流的审核步骤。](../../../../images/tutorials/create/talon-one-batch/review.png)

## 监测数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监视数据流的详细信息，请参阅有关UI[中](../../../../../dataflows/ui/monitor-sources.md)监视帐户和数据流的教程。