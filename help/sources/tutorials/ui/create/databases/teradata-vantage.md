---
keywords: Experience Platform；主页；热门主题；Data Vantage
title: 在UI中创建TeradataVantage源连接
description: 了解如何使用Adobe Experience Platform UI创建TeradataVantage源连接。
source-git-commit: f140dac67ccd09ec1e6cab794f53e0090af55442
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# （测试版）创建 [!DNL Teradata Vantage] UI中的源连接

>[!NOTE]
>
> 的 [!DNL Teradata Vantage] 来源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

本教程提供了创建 [!DNL Teradata Vantage] 源连接器。

## 快速入门

本教程需要对Platform的以下组件有一定的了解：

* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

为了访问 [!DNL Teradata Vantage] 帐户，则必须提供以下身份验证值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 连接字符串 | 连接字符串是提供有关数据源以及如何连接到该数据源的信息的字符串。 的连接字符串模式 [!DNL Teradata Vantage] is `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

有关入门的更多信息，请参阅此 [[!DNL Teradata Vantage] 文档](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## 连接 [!DNL Teradata Vantage] 帐户

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以为其创建帐户的各种来源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在 [!UICONTROL 数据库] 类别，选择 **[!UICONTROL Teradata]** 然后选择 **[!UICONTROL 添加数据]**.

![](../../../../images/tutorials/create/teradata/catalog.png)

的 **[!UICONTROL 连接到TeradataVantage]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择 [!DNL Teradata Vantage] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/teradata/existing.png)

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述以及 [!DNL Teradata Vantage] 凭据。 完成后，选择 **[!UICONTROL 连接]** 然后，再留出一些时间建立新连接。

![](../../../../images/tutorials/create/teradata/new.png)

## 后续步骤

通过阅读本教程，您已建立了与TeradataVantage帐户的连接。 您现在可以继续下一个教程和 [配置数据流以将数据导入平台](../../dataflow/databases.md).
