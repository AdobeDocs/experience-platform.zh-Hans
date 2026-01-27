---
title: 在UI中将Oracle Eloqua (V2)连接到Experience Platform
description: 了解如何在UI中将您的Oracle Eloqua帐户连接到Experience Platform。
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 1%

---

# 在UI中将[!DNL Oracle Eloqua] (V2)连接到Experience Platform

[!DNL Oracle Eloqua (V2)]源连接器使您能够将您的Oracle Eloqua帐户与Adobe Experience Platform连接，从而自动且可伸缩地摄取关键的B2B营销数据，包括联系人、帐户、营销活动和参与活动。

使用此源连接器配置安全身份验证，选择所需的确切Eloqua数据实体，并将其映射到标准化体验数据模型(XDM)架构。 灵活的计划选项允许您设置初始数据加载和循环增量同步，确保营销数据保持最新和可操作。

[!DNL Oracle Eloqua (V2)]源连接器构建于Adobe的企业摄取框架之上，为活动优化、性能衡量和跨渠道个性化提供了可靠、可扩展的基础。

阅读本指南，了解如何使用Experience Platform用户界面中的源工作区将您的[!DNL Oracle Eloqua]帐户连接到Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

### 收集所需的凭据 {#credentials}

有关身份验证的信息，请阅读[[!DNL Eloqua] 概述](../../../../connectors/marketing-automation/eloqua.md)。

## 导航源目录 {#catalog}

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问&#x200B;*[!UICONTROL Sources]*&#x200B;工作区。 选择类别或使用搜索栏查找您的源。

要连接到[!DNL Eloqua]，请转到&#x200B;*[!UICONTROL Marketing Automation]*&#x200B;类别，选择&#x200B;**[!UICONTROL (V2) Oracle Eloqua]**&#x200B;源卡，然后选择&#x200B;**[!UICONTROL Set up]**。

>[!TIP]
>
>当给定的源尚未拥有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL Set up]**&#x200B;选项。 创建经过身份验证的帐户后，此选项将更改为&#x200B;**[!UICONTROL Add data]**。

![源目录中的Eloqua源卡的“设置”按钮突出显示。](../../../../images/tutorials/create/eloqua/catalog.png)

## 使用现有帐户 {#existing}

要使用现有帐户，请选择&#x200B;**[!UICONTROL Existing account]**，然后选择要使用的[!DNL Eloqua]帐户。

![在帐户创建界面中选择了“现有帐户”选项。](../../../../images/tutorials/create/eloqua/existing.png)

## 创建新帐户 {#new}

要创建新帐户，请选择&#x200B;**[!UICONTROL New account]**，然后在[!UICONTROL Source connection details]下提供名称和描述。 接下来，在[!UICONTROL Account authentication]下提供您的&#x200B;**客户端ID**、**客户端密钥**、**用户名**、**密码**&#x200B;和&#x200B;**基本终结点**&#x200B;的值。 您可以阅读[身份验证指南](../../../../connectors/marketing-automation/eloqua.md)以了解有关这些凭据的详细信息。 完成后，选择&#x200B;**[!UICONTROL Connect to source]**&#x200B;并等待几秒钟以建立连接。

![带有源连接详细信息和身份验证凭据字段的新帐户界面。](../../../../images/tutorials/create/eloqua/new.png)

## 选择数据

使用选择数据界面选择要摄取到Experience Platform的[!DNL Eloqua]实体。

>[!TIP]
>
>在选择数据时，您会注意到，除营销活动之外，其他实体会显示具有代表性的示例数据。 此方法可确保您预览可用字段和结构，因为[!DNL Eloqua]个公共API当前仅检索营销活动的实际数据。 对于其余实体，会提供示例数据以支持您的配置工作流。

![显示可用Eloqua数据实体的数据选择接口。](../../../../images/tutorials/create/eloqua/select-data.png)

## 数据集和数据流详细信息 {#details}

接下来，您必须提供有关数据集和数据流的信息。 在此步骤中，您可以使用现有数据集或创建新数据集。 此外，您可以选择启用数据集以在此步骤期间摄取到Real-time Customer Profile。

![数据集和数据流详细信息界面，带有用于配置数据集属性的选项。](../../../../images/tutorials/create/eloqua/details.png)

## 映射 {#mapping}

[!DNL Eloqua]的映射分为四种主要实体类型：

* **帐户** - [!DNL Eloqua]中的公司/组织记录。
* **活动** - [!DNL Eloqua]中的营销活动和参与事件。
* **营销活动** - [!DNL Eloqua]中的营销活动记录。
* **联系人** - [!DNL Eloqua]中的个人记录。

如果您需要访问默认提供的字段以外的其他字段，可以使用Experience Platform中的数据准备映射过程添加这些字段。 如果默认（标准）架构不支持某些必填字段，您可以选择在Experience Platform中定义自定义架构。 使用此功能创建和映射必要的字段，以便您可以无缝地将[!DNL Eloqua]中的所有相关数据摄取到Experience Platform。

后续步骤摘要：

* 查看集成中可用的默认映射字段。
* 在映射步骤中，包括[!DNL Eloqua]所需的任何其他字段。
* 如果标准架构中不存在新字段，请在Experience Platform中扩展或创建包含这些字段的自定义架构。
* 完成映射以确保摄取所有所需数据。

为确保准确反映您的外部CRM信息，只需使用数据准备中的计算字段函数，在源数据字段中用您的特定CRM实例ID更新`{CRM_INSTANCE_ID}`占位符即可。 这让您能够灵活地根据组织的独特设置定制集成。

要使用计算字段编辑器，请选择要更新的源字段。

![包含计算字段的Eloqua源字段。](../../../../images/tutorials/create/eloqua/select-calculated-field.png)

>[!BEGINTABS]

>[!TAB Salesforce]

对于[!DNL Salesforce]用户，请使用计算字段编辑器并使用适当的实例ID更新`{CRM_INSTANCE_ID}`。

![Salesforce的计算字段。](../../../../images/tutorials/create/eloqua/sf-field.png)

>[!TAB Microsoft Dynamics]

对于[!DNL Microsoft]用户，请使用计算字段编辑器并使用适当的实例ID更新`{CRM_INSTANCE_ID}`。

![Dynamics的计算字段。](../../../../images/tutorials/create/eloqua/dynamics-field.png)

>[!ENDTABS]

更新完计算字段后，请选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![映射接口显示Eloqua数据实体的字段映射。](../../../../images/tutorials/create/eloqua/mapping.png)

## 日程计划

>[!NOTE]
>
>以下是内部用于增量数据加载的增量字段：
>
>* **联系人：** `C_DateModified`
>* **帐户：** `M_DateModified`
>* **活动：** `CreatedAt`
>* **自定义对象：** `UpdatedAt`
>* **营销活动：** `updatedAt`

完成映射后，您现在可以为数据流配置摄取计划。 将您的[!UICONTROL Frequency]设置为`Once`以配置一次性摄取运行。 对于增量摄取，您可以将[!UICONTROL Frequency]设置为`Hour`、`Day`或`Week`。 使用增量摄取时，还必须配置[!UICONTROL Interval]以定义摄取运行之间发生的时间量。 例如，摄取频率设置为`Day`，间隔设置为`15`意味着您的数据流计划每15天摄取一次数据。

[!DNL Eloqua]源的每分钟摄取频率不可用。 您可以选择的最频繁的时间表是每小时。 选择与您的数据刷新需求相匹配的时间表。 请记住，选择更频繁的时间表将增加计算成本。

![计划界面，其中包含用于配置摄取频率和间隔的选项。](../../../../images/tutorials/create/eloqua/scheduling.png)

## 审阅

配置摄取计划后，使用[!UICONTROL Review]界面确认数据流的详细信息。 选择&#x200B;**[!UICONTROL Finish]**&#x200B;以完成设置，并留出一些时间让数据流启动。

![审阅界面显示数据流配置在完成前的摘要。](../../../../images/tutorials/create/eloqua/review.png)

## 监测

选择数据流后，它将按照指定的计划执行一次性数据回填和后续增量同步。 可以通过导航到数据流来监视同步的状态。 有关详细信息，请阅读UI[中](../../../../../dataflows/ui/monitor-sources.md)监视源数据流的指南。

## 后续步骤

您现在已在Experience Platform中完成[!DNL Eloqua]源的设置和配置。 建立数据流后，将根据您选择的计划摄取您的[!DNL Eloqua]数据并映射到标准体验数据模型(XDM)架构。 继续监测数据流并在Platform中探索摄取的数据，以获得见解并激活营销用例。 有关更高级的配置及疑难解答，请参阅相关文档或联系Adobe支持资源。

有关其他信息，请阅读以下文档：

* [源概述](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)
