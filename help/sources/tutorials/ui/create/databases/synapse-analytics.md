---
title: 在UI中创建Azure synapse分析源连接
description: 了解如何使用Adobe Experience Platform UI创建Azure synapseAnalytics（以下简称“Synapse”）源连接。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 1f1ce317-eaaf-4ad2-a5fb-236983220bd7
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# 创建 [!DNL Azure Synapse Analytics] UI中的源连接

>[!IMPORTANT]
>
>此 [!DNL Azure Synapse Analytics] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

本教程提供了用于创建 [!DNL Azure Synapse Analytics] (以下简称“[!DNL Synapse]&quot;)源连接器使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Synapse] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/databases.md).

### 收集所需的凭据

要访问 [!DNL Synapse] 帐户 [!DNL Platform]中，您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您的关联的连接字符串 [!DNL Synapse] 身份验证。 此 [!DNL Synapse] 连接字符串模式为 `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |

有关此值的更多信息，请参阅 [此 [!DNL Synapse] 文档](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-sql-data-warehouse).

## 连接您的 [!DNL Synapse] 帐户

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL Synapse] 帐户至 [!DNL Platform].

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问 **[!UICONTROL 源]** 工作区。 此 **[!UICONTROL 目录]** 屏幕显示了多种来源，您可以使用这些来源创建帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 **[!UICONTROL 数据库]** 类别，选择 **[!UICONTROL azure synapse分析]**. 如果这是您第一次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，选择 **[!UICONTROL 添加数据]** 以新建 [!DNL Synapse] 连接器。

![](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

此 **[!UICONTROL 连接到Azure synapse Analytics]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在出现的输入表单上，提供名称、可选描述以及 [!DNL Synapse] 凭据。 完成后，选择 **[!UICONTROL 连接]** 然后等待一段时间以建立新连接。

![](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL Synapse] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## 后续步骤

通过学习本教程，您已建立与的连接 [!DNL Synapse] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据引入 [!DNL Platform]](../../dataflow/databases.md).
