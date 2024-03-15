---
title: 使用用户界面从Stripe帐户摄取支付数据以Experience Platform。
description: 了解如何使用用户界面将支付数据从您的Stripe账户摄取到Experience Platform。
hide: true
hidefromtoc: true
badge: Beta 版
source-git-commit: b5e791882ddb7cb8c87c15d4812470b3bbc9a72e
workflow-type: tm+mt
source-wordcount: '1636'
ht-degree: 3%

---

# 从贵机构接收支付数据 [!DNL Stripe] 要使用用户界面Experience Platform的帐户

>[!NOTE]
>
>此 [!DNL Stripe] 源为测试版。 阅读 [条款和条件](../../../../home.md#terms-and-conditions) 有关使用测试版标记源的更多信息，请参阅源概述。

请阅读以下教程，了解如何从贵机构接收支付数据 [!DNL Stripe] 使用用户界面登录到Adobe Experience Platform的帐户。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

### 身份验证

阅读 [[!DNL Stripe] 概述](../../../../connectors/payments/stripe.md) 有关如何检索身份验证凭据的信息。

## 连接您的 [!DNL Stripe] 帐户 {#connect}

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 *支付* 类别，选择 **[!DNL Stripe]**，然后选择 **[!UICONTROL 设置]**.

>[!TIP]
>
>源目录中的源显示 **[!UICONTROL 设置]** 选项。 经过身份验证的帐户存在后，此选项将更改为 **[!UICONTROL 添加数据]**.

![已选择Stripe源卡的Experience PlatformUI中的源目录。](../../../../images/tutorials/create/stripe/catalog.png)

此 **[!UICONTROL 连接Stripe帐户]** 页面。 在此页上，您可以使用新的或现有的身份证明。

>[!BEGINTABS]

>[!TAB 创建新帐户]

要创建新帐户，请选择 **[!UICONTROL 新帐户]** 并提供名称、可选描述和您的凭据。

完成后，选择 **[!UICONTROL 连接到源]** 然后等待一段时间以建立新连接。

![源工作流的新帐户创建界面。](../../../../images/tutorials/create/stripe/new.png)

| 凭据 | 描述 |
| --- | --- |
| 访问令牌 | 您的 [!DNL Stripe] 访问令牌。 有关如何检索访问令牌的信息，请参阅 [[!DNL Stripe] 身份验证指南](../../../../connectors/payments/stripe.md). |

>[!TAB 使用现有帐户]

要使用现有帐户，请选择 **[!UICONTROL 现有帐户]** 然后从现有帐户目录中选择要使用的帐户。

选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![源目录的现有帐户选择页面。](../../../../images/tutorials/create/stripe/existing.png)

>[!ENDTABS]

## 选择数据 {#select-data}

现在您已经拥有了帐户的访问权限，则必须确定指向 [!DNL Stripe] 要摄取的数据。 选择 **[!UICONTROL 资源路径]** 然后选择要从中摄取数据的端点。 可用的 [!DNL Stripe] 端点包括：

* 费用
* 订阅
* 退款
* 余额交易记录
* 客户
* 价格

![资源路径下拉窗口。](../../../../images/tutorials/create/stripe/select-resource-path.png)

选择端点后，界面将更新为预览屏幕，并显示 [!DNL Stripe] 您选择的端点。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![Stripe数据的预览窗口。](../../../../images/tutorials/create/stripe/preview.png)

## 提供数据集和数据流详细信息 {#provide-dataset-and-dataflow-details}

接下来，您必须提供有关数据集和数据流的信息。

### 数据集详细信息 {#dataset-details}

数据集是用于数据集合的存储和管理结构，通常是表格，其中包含架构（列）和字段（行）。成功引入Experience Platform的数据将作为数据集存储在数据湖中。 在此步骤中，您可以创建新数据集或使用现有数据集。

>[!BEGINTABS]

>[!TAB 使用新数据集]

要使用新数据集，请选择 **[!UICONTROL 新数据集]** 然后为数据集提供名称和可选描述。 您还必须选择数据集所遵循的体验数据模型(XDM)架构。

![新的数据集选择界面。](../../../../images/tutorials/create/stripe/new-dataset.png)

| 新数据集详细信息 | 描述 |
| --- | --- |
| 输出数据集名称 | 新数据集的名称。 |
| 描述 | （可选）新数据集的简短说明。 |
| 架构 | 您的组织中存在的架构的下拉列表。 您还可以在源配置过程之前创建自己的架构。 有关详细信息，请阅读上的指南 [在UI中创建XDM架构](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB 使用现有数据集]

如果您已经有一个现有数据集，请选择 **[!UICONTROL 现有数据集]** 然后使用 **[!UICONTROL 高级搜索]** 选项可查看贵组织中所有数据集的窗口，包括其各自的详细信息，如是否启用它们以摄取到Real-time Customer Profile。

![现有数据集选择界面。](../../../../images/tutorials/create/stripe/existing-dataset.png)

>[!ENDTABS]

+++选择相关步骤以启用配置文件摄取、错误诊断和部分摄取。

如果您的数据集启用了实时客户资料，那么在此步骤中，您可以切换 **[!UICONTROL 配置文件数据集]** 为配置文件摄取启用数据。 您还可以使用此步骤来启用 **[!UICONTROL 错误诊断]** 和 **[!UICONTROL 部分摄取]**.

* **[!UICONTROL 错误诊断]**：选择 **[!UICONTROL 错误诊断]** 指示源生成错误诊断，以便以后在监视数据集活动和数据流状态时可以参考这些诊断。
* **[!UICONTROL 部分摄取]**：部分批量摄取是指在特定可配置阈值之前摄取包含错误的数据的能力。 此功能允许您成功地将所有准确的数据提取到Experience Platform中，同时所有不正确的数据将单独进行批处理并显示有关其无效原因的信息。

+++

### 数据流详细信息 {#dataflow-details}

配置数据集后，您必须提供有关数据流的详细信息，包括名称、可选描述和警报配置。

![数据流详细信息配置步骤。](../../../../images/tutorials/create/stripe/dataflow-detail.png)

| 数据流配置 | 描述 |
| --- | --- |
| 数据流名称 | 数据流的名称。  默认情况下，这将使用正在导入的文件的名称。 |
| 描述 | （可选）数据流的简短说明。 |
| 警报 | Experience Platform可以生成基于事件的警报，供用户订阅。 这些选项都需要一个正在运行的数据流来触发它们。  欲知更多信息，请参阅 [警报概述](../../alerts.md) <ul><li>**源数据流运行开始**：选择此警报可在数据流运行开始时接收通知。</li><li>**源数据流运行成功**：选择此警报可在数据流结束并且没有任何错误时接收通知。</li><li>**源数据流运行失败**：选择此警报可在数据流运行结束并出现任何错误时接收通知。</li></ul> |

完成后，选择 **[!UICONTROL 下一个]** 以继续。

## 将字段映射到XDM架构 {#mapping}

此 **[!UICONTROL 映射]** 此时将显示步骤。 使用映射界面将源数据映射到相应的架构字段，然后再将该数据摄取到Experience Platform中。 有关如何使用映射界面的详细指南，请阅读 [数据准备UI指南](../../../../../data-prep/ui/mapping.md) 以了解更多信息。

![源工作流的映射界面。](../../../../images/tutorials/create/stripe/mapping.png)

## 配置摄取计划 {#scheduling}

接下来，使用计划界面为数据流创建摄取计划。

选择频率下拉菜单以配置数据流的摄取频率。

![频率下拉菜单。](../../../../images/tutorials/create/stripe/frequency.png)

您还可以选择日历图标并使用弹出日历来配置摄取开始时间。

![用于计划的可配置日历。](../../../../images/tutorials/create/stripe/calendar.png)

| 计划配置 | 描述 |
| --- | --- |
| 频度 | 配置频率以指示数据流运行的频率。 您可以将频率设置为： <ul><li>**一次**：将频率设置为 `once` 以创建一次性摄取。 创建一次性摄取数据流时，间隔和回填配置不可用。 默认情况下，调度频率设置为一次。</li><li>**分钟**：将频率设置为 `minute` 安排数据流以按分钟摄取数据。</li><li>**小时**：将频率设置为 `hour` 安排数据流以每小时摄取数据。</li><li>**天**：将频率设置为 `day` 安排数据流每天摄取数据。</li><li>**周**：将频率设置为 `week` 安排数据流每周摄取数据。</li></ul> |
| 间隔 | 选择频率后，可以配置间隔设置以建立每次引入之间的时间范围。 例如，如果将频率设置为天并将间隔配置为15，则数据流将每15天运行一次。 **注意**：不能将间隔设置为零。 |
| 开始时间 | 预计运行的时间戳，以UTC时区显示。 |
| 回填 | 回填可确定最初摄取的数据。 如果启用了回填，则指定路径中的所有当前文件将在第一次计划摄取期间摄取。 如果禁用回填，则只摄取在第一次引入运行到开始时间之间加载的文件。 将不会摄取在开始时间之前加载的文件。 |

配置数据流的摄取计划后，选择 **[!UICONTROL 下一个]**.

![源工作流的计划界面。](../../../../images/tutorials/create/stripe/scheduling.png)


## 查看您的数据流

数据流创建过程的最后一步是在执行数据流之前对其进行检查。 使用 **[!UICONTROL 审核]** 步骤以在运行新数据流之前查看其详细信息。 详细信息按以下类别分组：

* **连接**：显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **分配数据集和映射字段**：显示要将源数据摄取到哪个数据集，包括数据集所遵循的架构。
* **正在计划**：显示摄取计划的活动时段、频率和间隔。

查看数据流后，选择 **[!UICONTROL 完成]** 留出一段时间来创建数据流。

![源工作流的审核步骤。](../../../../images/tutorials/create/stripe/review.png)

## 后续步骤

通过学习本教程，您已成功地创建了数据流以从贵机构的 [!DNL Stripe] 要Experience Platform的源。 有关其他资源，请访问下面列出的文档。

### 监测数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监视数据流的更多信息，请访问上的教程 [在UI中监控帐户和数据流](../../../../../dataflows/ui/monitor-sources.md).

### 更新您的数据流

要更新数据流计划、映射和常规信息的配置，请访问上的教程 [在UI中更新源数据流](../../update-dataflows.md).

### 删除您的数据流

您可以删除不再必需的数据流或使用 **[!UICONTROL 删除]** 函数位于 **[!UICONTROL 数据流]** 工作区。 有关如何删除数据流的更多信息，请访问上的教程 [在UI中删除数据流](../../delete.md).
