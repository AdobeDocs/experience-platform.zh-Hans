---
title: 在UI中创建Merkury企业身份解析Source连接和数据流
description: 了解如何使用Adobe Experience Platform UI创建Merkury企业身份解析源连接。
last-substantial-update: 2023-12=12
badge: Beta 版
exl-id: 2af48c18-76f9-4615-8e76-8f030a312a8f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '2015'
ht-degree: 1%

---

# 在UI中创建[!DNL Merkury Enterprise Identity Resolution]源连接和数据流

>[!NOTE]
>
>[!DNL Merkury Enterprise Identity Resolution]源为测试版。 有关使用测试版标记源的更多信息，请阅读[源概述](../../../../home.md#terms-and-conditions)。

本教程提供了使用Adobe Experience Platform用户界面创建[!DNL Merkury Enterprise Identity Resolution]源连接和数据流的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

### 收集所需的凭据

要在Experience Platform时访问存储段，您需要为以下凭据提供有效值：

| 凭据 | 描述 |
| --- | --- |
| 访问密钥 | 存储段的访问密钥ID。 您可以从[!DNL Merkury]团队中检索此值。 |
| 密钥 | 存储桶的密钥ID。 您可以从[!DNL Merkury]团队中检索此值。 |
| 存储桶名称 | 这是您的Merkury存储桶，将在其中共享文件。 您可以从[!DNL Merkury]团队中检索此值。 |

有关为[!DNL Merkury]设置和其他先决条件的详细信息，请阅读[[!DNL Merkury] 源概述](../../../../connectors/data-partners/merkury.md)。

## 连接您的Merkury帐户

在Platform UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;**[!UICONTROL 数据合作伙伴]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Merkury]**，然后选择&#x200B;**[!UICONTROL 设置]**。

![已选择Merkury源的源目录。](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到Merkury]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 创建新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入表单上，提供名称、可选描述和您的[!DNL Merkury]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

![Merkury的新帐户接口。](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/new-account.png)

### 使用现有帐户

要使用现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后选择要使用的[!DNL Merkury]帐户。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![Merkury的现有帐户接口。](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/existing-account.png)

>[!BEGINSHADEBOX]

**支持的文件格式**

您可以使用[!DNL Merkury]源摄取以下文件格式：

* 分隔符分隔值(DSV)：任何单字符值都可以用作DSV格式的数据文件的分隔符。
* [!DNL JavaScript Object Notation] (JSON)： JSON格式的数据文件必须符合XDM。
* [!DNL Apache Parquet]： Parquet格式的数据文件必须符合XDM。
* 压缩文件： JSON和分隔文件可以压缩为： `bzip2`、`gzip`、`deflate`、`zipDeflate`、`tarGzip`和`tar`。

>[!ENDSHADEBOX]

## 添加数据

创建您的[!DNL Merkury]帐户后，将显示&#x200B;**[!UICONTROL 添加数据]**&#x200B;步骤，该步骤为您提供了一个界面，让您能够探索[!DNL Merkury]文件层次结构并选择要带入Experience Platform的文件夹或特定文件。

* 界面的左侧是目录浏览器，显示您的[!DNL Merkury]文件层次结构。
* 界面的右侧部分允许您预览兼容文件夹或文件中最多100行数据。

![源工作流的文件和文件夹目录，您可以在其中选择要摄取的数据。](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/add-data.png)

选择根文件夹以访问您的文件夹层次结构。 在此处，您可以选择单个文件夹以递归方式摄取文件夹中的所有文件。 摄取整个文件夹时，必须确保该文件夹中的所有文件共享相同的数据格式和架构。

选择文件夹后，正确的界面将更新为所选文件夹中第一个文件的内容和结构的预览。

![选定进行摄取的数据和文件预览界面。](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/selected-data.png)


在此步骤中，您可以在继续之前对数据做出多个配置。 首先，选择&#x200B;**[!UICONTROL 数据格式]**，然后在出现的下拉面板中为文件选择适当的数据格式。

下表显示了所支持文件类型的相应数据格式：

| 文件类型 | 数据格式 |
| --- | --- |
| CSV | [!UICONTROL 已分隔] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL XDM Parquet] |

### 选择列分隔符

+++选择以查看有关如何设置分隔符的步骤

配置数据格式后，可在引入分隔文件时设置列分隔符。 选择&#x200B;**[!UICONTROL 分隔符]**&#x200B;选项，然后从下拉菜单中选择一个分隔符。 菜单显示最常用的分隔符选项，包括逗号(`,`)、制表符(`\t`)和管道字符(`|`)。

如果您希望使用自定义分隔符，请选择&#x200B;**[!UICONTROL 自定义]**，然后在弹出输入栏中输入您选择的单个字符分隔符。

+++

### 摄取压缩文件

+++ 选择可查看有关如何摄取压缩文件的步骤

您还可以通过指定压缩JSON或分隔文件的压缩类型来摄取它们。

在[!UICONTROL 选择数据]步骤中，选择要摄取的压缩文件，然后选择其相应的文件类型以及是否符合XDM。 接下来，选择&#x200B;**[!UICONTROL 压缩类型]**，然后为您的源数据选择适当的压缩文件类型。

要将特定文件带入Platform，请选择一个文件夹，然后选择要摄取的文件。 在此步骤中，还可以使用文件名旁边的预览图标预览给定文件夹中其他文件的文件内容。

完成后，选择&#x200B;**[!UICONTROL 下一步]**。

+++

## 提供数据流详细信息

[!UICONTROL 数据流详细信息]页面允许您选择是要使用现有数据集，还是使用新数据集。 在此过程中，您还可以配置要摄取到配置文件的数据，并启用[!UICONTROL 错误诊断]、[!UICONTROL 部分摄取]和[!UICONTROL 警报]等设置。

### 使用现有数据集

要将数据摄取到现有数据集，请选择&#x200B;**[!UICONTROL 现有数据集]**。 您可以使用[!UICONTROL 高级搜索]选项或通过滚动下拉菜单中的现有数据集列表来检索现有数据集。 选择数据集后，为数据流提供名称和描述。

![现有数据集界面。](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/existing-dataset.png)

### 使用新数据集

要摄取到新数据集中，请选择&#x200B;**[!UICONTROL 新数据集]**，然后提供输出数据集名称和可选描述。 接下来，使用[!UICONTROL 高级搜索]选项或通过滚动下拉菜单中的现有架构列表来选择要映射到的架构。 选择架构后，为数据流提供名称和描述。

![新数据集界面。](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/new-dataset.png)

### 启用配置文件和错误诊断

+++选择以查看启用错误诊断和配置文件摄取的步骤

接下来，选择&#x200B;**[!UICONTROL 个人资料数据集]**&#x200B;切换开关以启用您的数据集以提供实时客户个人资料。 这允许您创建实体的属性和行为的整体视图。 来自所有启用配置文件的数据集的数据将包含在配置文件中，并在保存数据流时应用更改。

[!UICONTROL 错误诊断]允许为数据流中发生的任何错误记录生成详细的错误消息，而[!UICONTROL 部分摄取]允许您摄取包含错误的数据，摄取阈值为您手动定义的某个阈值。 有关详细信息，请参阅[部分批次摄取概述](../../../../../ingestion/batch-ingestion/partial.md)。

+++

### 启用警报

+++选择此选项可查看启用警报的步骤

您可以启用警报以接收有关数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅源警报指南](../../alerts.md)。

完成向数据流提供详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

+++

## 将数据字段映射到XDM架构

此时将显示[!UICONTROL 映射]步骤，该步骤为您提供了一个接口，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射器界面和计算字段的全面步骤，请参阅[数据准备UI指南](../../../../../data-prep/ui/mapping.md)。

成功映射源数据后，选择&#x200B;**[!UICONTROL 下一步]**。

![映射接口。](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/mapping.png)

## 计划摄取运行

此时将显示[!UICONTROL 计划]步骤，允许您配置摄取计划，以使用配置的映射自动摄取选定的源数据。 默认情况下，计划设置为`Once`。 要调整您的摄取频率，请选择&#x200B;**[!UICONTROL 频率]**，然后从下拉菜单中选择一个选项。

>[!TIP]
>
>间隔和回填在一次性摄取期间不可见。

![计划接口](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/schedule.png)

如果将摄取频率设置为`Minute`、`Hour`、`Day`或`Week`，则必须设置一个间隔，以便在每次摄取之间建立一个设置的时间范围。 例如，摄取频率设置为`Day`，间隔设置为`15`意味着您的数据流计划每15天摄取一次数据。

在此步骤中，您还可以启用&#x200B;**回填**&#x200B;并为增量数据摄取定义列。 回填用于摄取历史数据，而您为增量摄取定义的列允许从现有数据中区分新数据。

有关计划配置的详细信息，请参阅下表。

| 字段 | 描述 |
| --- | --- |
| 频度 | 摄取发生的频率。 可选择频率包括`Once`、`Minute`、`Hour`、`Day`和`Week`。 |
| 间隔 | 设置所选频率间隔的整数。 间隔值应为非零整数，且应设置为大于或等于15。 |
| 开始时间 | UTC时间戳，指示何时设置第一次引入。 开始时间必须大于或等于当前UTC时间。 |
| 回填 | 一个布尔值，用于确定最初摄取的数据。 如果启用了回填，则指定路径中的所有当前文件将在第一次计划摄取期间摄取。 如果禁用回填，则只摄取在第一次引入运行到开始时间之间加载的文件。 将不会摄取在开始时间之前加载的文件。 |

>[!NOTE]
>
>对于批量摄取，每个后续数据流会根据其&#x200B;**上次修改时间**&#x200B;时间戳选择从源中摄取的文件。 这意味着批处理数据流从源中选择新的文件，或者自上次流运行以来修改的文件。 此外，您必须确保在文件上传与计划流量运行之间有足够的时间跨度，因为可能无法提取在计划流量运行时间之前未完全上传到您的云存储帐户的文件以供摄取。

完成摄取计划配置后，选择&#x200B;**[!UICONTROL 下一步]**。

## 查看您的数据流

将显示&#x200B;**[!UICONTROL 审核]**&#x200B;步骤，允许您在创建新数据流之前对其进行审核。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**：显示要将源数据摄取到哪个数据集，包括数据集所遵循的架构。
* **[!UICONTROL 计划]**：显示摄取计划的活动时段、频率和间隔。

查看数据流后，单击&#x200B;**[!UICONTROL 完成]**&#x200B;并留出一些时间来创建数据流。

![审核页面。](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/review.png)

## 后续步骤

通过完成本教程，您已成功地创建了一个数据流以将批次数据从[!DNL Merkury]源引入Experience Platform。 有关其他资源，请访问下面列出的文档。

### 监测数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监视数据流的详细信息，请访问有关UI中[监视帐户和数据流的教程](../../monitor.md)。

### 更新您的数据流

要更新数据流计划、映射和常规信息的配置，请访问有关[在UI中更新源数据流的教程](../../update-dataflows.md)

### 删除您的数据流

您可以删除不再必需的数据流或使用&#x200B;**[!UICONTROL 数据流]**&#x200B;工作区中提供的&#x200B;**[!UICONTROL 删除]**&#x200B;功能错误地创建的数据流。 有关如何删除数据流的详细信息，请访问有关[在UI中删除数据流](../../delete.md)的教程。
