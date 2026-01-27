---
title: 通过UI将您的Salesforce Marketing Cloud (V2)帐户连接到Experience Platform
description: 了解如何通过UI将您的Salesforce Marketing Cloud (V2)帐户连接到Experience Platform。
source-git-commit: 91bf8bf6e6f7030574d693484ce9797800c2d5dd
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 1%

---

# 将[!DNL Salesforce Marketing Cloud]连接到Experience Platform

阅读本指南，了解如何使用Experience Platform用户界面中的源工作区将您的[!DNL Salesforce Marketing Cloud]帐户连接到Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Salesforce Marketing Cloud] 概述](../../../../connectors/marketing-automation/sfmc.md#prerequisites)。

## 导航源目录

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问&#x200B;*[!UICONTROL Sources]*&#x200B;工作区。 选择类别或使用搜索栏查找您的源。

要连接到[!DNL Salesforce Marketing Cloud]，请转到&#x200B;*[!UICONTROL Marketing Automation]*&#x200B;类别，选择&#x200B;**[!UICONTROL (V2) Salesforce Marketing Cloud]**&#x200B;源卡，然后选择&#x200B;**[!UICONTROL Set up]**。

>[!TIP]
>
>当给定的源尚未拥有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL Set up]**&#x200B;选项。 创建经过身份验证的帐户后，此选项将更改为&#x200B;**[!UICONTROL Add data]**。

![已选择Salesforce Marketing Cloud源的源目录。](../../../../images/tutorials/create/sfmc/catalog.png)

## 使用现有帐户 {#existing}

要使用现有帐户，请选择&#x200B;**[!UICONTROL Existing account]**，然后选择要使用的[!DNL Salesforce Marketing Cloud]帐户。

![源工作流的现有帐户接口](../../../../images/tutorials/create/sfmc/existing.png)

## 创建新帐户 {#new}

要创建新帐户，请选择&#x200B;**[!UICONTROL New account]**，然后在[!UICONTROL Source connection details]下提供名称和描述。 接下来，在[!UICONTROL Account authentication]下提供您的&#x200B;**客户端ID**、**客户端密钥**&#x200B;和&#x200B;**基本终结点**&#x200B;的值。 您可以阅读[身份验证指南](../../../../connectors/marketing-automation/sfmc.md#gather-required-credentials)以了解有关这些凭据的详细信息。 完成后，选择&#x200B;**[!UICONTROL Connect to source]**&#x200B;并等待几秒钟以建立连接。

![源工作流的新帐户接口。](../../../../images/tutorials/create/sfmc/new.png)

## 选择数据

[!DNL Salesforce Marketing Cloud]源仅支持从[!DNL Salesforce Marketing Cloud]数据扩展进行数据摄取。

使用[!UICONTROL Select data]界面选择要从[!DNL Salesforce Marketing Cloud]实例中摄取的数据扩展。 选择数据扩展后，您可以使用预览面板来确认数据集包含预期的字段，然后再继续。

![源工作流的选择数据步骤](../../../../images/tutorials/create/sfmc/select-data.png)

## 数据集和数据流详细信息

接下来，您必须提供有关数据集和数据流的信息。 在此步骤中，您可以使用现有数据集或创建新数据集。 此外，您可以选择启用数据集以在此步骤期间摄取到Real-time Customer Profile。

![源工作流的数据集和数据流详细信息步骤。](../../../../images/tutorials/create/sfmc/dataset-details.png)

## 映射

在[!DNL Salesforce Marketing Cloud]中，数据扩展不被视为标准对象。 因此，没有预定义或固定的字段映射到Experience Platform架构。 虽然Experience Platform中的数据准备在[!DNL Salesforce Marketing Cloud]中的源字段和目标Experience Data Model (XDM)架构之间尽力保持一致，但在某些情况下，仍需要手动审查或调整以解决未映射或错误字段。

![源工作流的映射步骤。](../../../../images/tutorials/create/sfmc/mapping.png)

## 计划数据流

完成映射后，您现在可以为数据流配置摄取计划。 将您的[!UICONTROL Frequency]设置为`Once`以配置一次性摄取运行。 对于增量摄取，您可以将[!UICONTROL Frequency]设置为`Hour`、`Day`或`Week`。 使用增量摄取时，还必须配置[!UICONTROL Interval]以定义摄取运行之间发生的时间量。 例如，摄取频率设置为`Day`，间隔设置为`15`意味着您的数据流计划每15天摄取一次数据。

>[!TIP]
>
> [!DNL Salesforce Marketing Cloud]源的每分钟摄取频率不可用。 您可以选择的最频繁的时间表是每小时。 选择与您的数据刷新需求相匹配的时间表。 请记住，选择更频繁的时间表将增加计算成本。

必须在数据集中选择一个增量（日期/时间）字段以启用增量同步。 如果数据集不包含合适的增量字段，您将无法创建数据流。

![源工作流的计划步骤。](../../../../images/tutorials/create/sfmc/schedule.png)

## 审阅

配置摄取计划后，使用[!UICONTROL Review]界面确认数据流的详细信息。 选择&#x200B;**[!UICONTROL Finish]**&#x200B;以完成设置，并留出一些时间让数据流启动。

![源工作流的审核步骤。](../../../../images/tutorials/create/sfmc/review.png)

## 监测

选择数据流后，它将按照指定的计划执行一次性数据回填和后续增量同步。 可以通过导航到数据流来监视同步的状态。 有关详细信息，请阅读UI[中](../../../../../dataflows/ui/monitor-sources.md)监视源数据流的指南。

## 后续步骤

本教程将指导您使用用户界面将[!DNL Salesforce Marketing Cloud] (V2)帐户连接到Experience Platform。 您已了解如何选择或创建源帐户、提供所需的凭据、选择要摄取的数据扩展、指定数据集和数据流详细信息、映射数据、设置数据摄取计划以及监视数据流。 按照这些步骤，您已成功将[!DNL Salesforce Marketing Cloud]数据与Experience Platform集成以供激活和分析。

有关其他信息，请阅读以下文档：

* [源概述](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)

