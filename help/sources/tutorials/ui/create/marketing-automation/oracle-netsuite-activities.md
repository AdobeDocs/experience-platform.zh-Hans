---
title: 在UI中创建 [!DNL Oracle NetSuite Activities] 源连接
description: 了解如何使用Adobe Experience Platform UI创建Oracle NetSuite活动源连接。
hide: true
hidefromtoc: true
badge: Beta 版
exl-id: 99ef0b50-c8d6-48d6-895f-46b7ade47520
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 2%

---

# 在用户界面中创建[!DNL Oracle NetSuite Activities]源连接

>[!NOTE]
>
>[!DNL Oracle NetSuite Activities]源为测试版。 有关使用测试版标记源的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

阅读以下教程，了解如何在UI中将[!DNL Oracle NetSuite Activities]帐户中的事件数据引入Adobe Experience Platform。

## 快速入门 {#getting-started}

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL Oracle NetSuite]帐户，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/marketing-automation.md)的教程。

>[!TIP]
>
>有关如何检索身份验证凭据的信息，请阅读[[!DNL Oracle NetSuite] 概述](../../../../connectors/marketing-automation/oracle-netsuite.md)。

## 连接您的[!DNL Oracle NetSuite]帐户 {#connect-account}

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;*营销自动化*&#x200B;类别下，选择&#x200B;**[!DNL Oracle NetSuite Activities]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

带有Experience Platform NetSuite活动信息卡的目录![Oracle UI屏幕截图](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/catalog-card.png)

此时会显示&#x200B;**[!UICONTROL 连接Oracle NetSuite活动帐户]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

>[!IMPORTANT]
>
>刷新令牌将在七天后过期。 令牌过期后，您必须在Experience Platform上使用更新的令牌创建帐户。 如果不使用更新后的令牌创建新帐户，您可能会看到以下错误消息：`The request could not be processed. Error from flow provider: The request could not be processed. Rest call failed with client error, status code 401 Unauthorized, please check your activity settings.`

### 现有账户 {#existing-account}

要使用现有帐户，请选择要用于创建新数据流的[!DNL Oracle NetSuite Activities]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![用于将Oracle NetSuite活动帐户与现有帐户连接的Experience Platform UI屏幕截图](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/existing.png)

### 新帐户 {#new-account}

如果要创建新帐户，请选择&#x200B;**[!UICONTROL 新建帐户]**，然后提供名称、可选描述和凭据。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

![用于将Oracle NetSuite活动帐户与新帐户连接的Experience Platform UI屏幕截图](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/new.png)

## 后续步骤 {#next-steps}

通过学习本教程，您已建立与[!DNL Oracle NetSuite Activities]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入Experience Platform](../../dataflow/marketing-automation.md)。

## 其他资源 {#additional-resources}

以下各节提供了在使用[!DNL Oracle NetSuite Activities]源时可以参考的其他资源。

### 映射 {#mapping}

Experience Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射器界面和计算字段的全面步骤，请参阅[数据准备UI指南](../../../../../data-prep/ui/mapping.md)。

>[!NOTE]
>
>显示的字段取决于您的[!DNL Oracle NetSuite]帐户有权访问的订阅。 例如，如果您无权访问计费，则不会看到与计费相关的字段。

### 计划中 {#scheduling}

在计划[!DNL Oracle NetSuite Activities]数据流进行摄取时，必须选择以下频率和间隔配置：

| 频度 | 间隔 |
| --- | --- |
| `Once` | 1 |

在检索数据时，[!DNL Oracle NetSuite]将上次修改或创建的日期作为日期格式而不是时间戳进行响应。 因此，调度限制为一天。

为您的计划提供值后，选择&#x200B;**[!UICONTROL 下一步]**。

![源工作流的计划步骤。](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/scheduling.png)
