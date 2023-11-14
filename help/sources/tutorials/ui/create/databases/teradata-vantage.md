---
keywords: Experience Platform；主页；热门主题；Teradata优势
title: 在UI中创建Teradata优势源连接
description: 了解如何使用Adobe Experience Platform UI创建TeradataVantage源连接。
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# (Beta)创建 [!DNL Teradata Vantage] UI中的源连接

>[!NOTE]
>
> 此 [!DNL Teradata Vantage] 源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记源代码的更多信息。

本教程提供了用于创建 [!DNL Teradata Vantage] 源连接器，使用Adobe Experience Platform用户界面。

## 快速入门

本教程需要您对Platform的以下组件有一定的了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

要访问 [!DNL Teradata Vantage] 帐户，您必须提供以下身份验证值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 连接字符串 | 连接字符串是一个字符串，它提供有关数据源以及如何连接到该数据源的信息。 的连接字符串模式 [!DNL Teradata Vantage] 是 `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

有关入门的更多信息，请参阅此 [[!DNL Teradata Vantage] 文档](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## 连接您的 [!DNL Teradata Vantage] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕中显示多种来源，您可以使用这些来源创建帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在 [!UICONTROL 数据库] 类别，选择 **[!UICONTROL teradata优势]** 然后选择 **[!UICONTROL 添加数据]**.

![](../../../../images/tutorials/create/teradata/catalog.png)

此 **[!UICONTROL 连接到Teradata Vantage]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择 [!DNL Teradata Vantage] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/teradata/existing.png)

### 新帐户

如果您正在使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在出现的输入表单上，提供名称、可选描述以及 [!DNL Teradata Vantage] 凭据。 完成后，选择 **[!UICONTROL 连接]** 然后等待一段时间以建立新连接。

![](../../../../images/tutorials/create/teradata/new.png)

## 后续步骤

通过学习本教程，您已与TeradataVantage帐户建立了连接。 您现在可以继续下一教程和 [配置数据流以将数据引入Platform](../../dataflow/databases.md).
