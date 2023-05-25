---
title: 使用Platform UI创建OracleEloqua源连接
description: 了解如何使用Platform UI将Adobe Experience Platform连接到OracleEloqua。
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 1%

---

# 创建 [!DNL Oracle Eloqua] 使用Platform UI的源连接

本教程提供了创建 [!DNL Oracle Eloqua] 源连接(使用Adobe Experience Platform用户界面)。

## 快速入门

本指南需要深入了解Platform的以下组件：

* [源](../../../../home.md)：Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

如果您已经通过了身份验证 [!DNL Oracle Eloqua] 帐户，则可以跳过本文档的其余部分并继续阅读上的教程 [创建数据流以将营销自动化数据引入平台](../../dataflow/marketing-automation.md).

### 收集所需的凭据

为了连接 [!DNL Oracle Eloqua] 到Platform时，必须提供以下身份验证属性的值：

| 凭据 | 描述 |
| --- | --- |
| 端点 | 的端点 [!DNL Oracle Eloqua] 服务器。 [!DNL Oracle Eloqua] 支持多个数据中心。 要查找您的端点，请登录 [[!DNL Oracle Eloqua] 界面](https://login.eloqua.com) ，然后从重定向URL中复制基本URL部分。 URL模式的格式为 `xxx.xx.eloqua.com` 并且输入时不应包含 `http` 或 `https`. |
| 用户名 | 您的用户名 [!DNL Oracle Eloqua] 服务器。 用户名格式必须是 `siteName + \\ + username`，其中 `siteName` 是您用来登录的公司名称 [!DNL Oracle Eloqua] 和 `username` 是您的用户名。 例如，您的登录用户名可以是： `Eloqua\Andy`. **注释**：必须使用单个反斜杠(`\`)在使用UI时，因为Experience PlatformUI会自动添加额外的反斜杠(`\`)输入用户名时。 |
| 密码 | 与您的对应的密码 [!DNL Oracle Eloqua] 用户名。 |

有关以下项的身份验证凭据的详细信息： [!DNL Oracle Eloqua]，请参见 [[!DNL Oracle Eloqua] 身份验证指南](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL Oracle Eloqua] Platform帐户。

## 连接您的 [!DNL Oracle Eloqua] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 [!UICONTROL 营销自动化] 类别，选择 **[!UICONTROL oracleEloqua]**，然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

此 **[!UICONTROL 连接OracleEloqua帐户]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL Oracle Eloqua] 要用于创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为提供名称、可选描述和相应的值 [!DNL Oracle Eloqua] 凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后留出一些时间来建立新连接。

![新](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 后续步骤

按照本教程，您已验证并创建了源连接，该连接位于 [!DNL Oracle Eloqua] 帐户和平台。 您现在可以继续下一教程和 [创建数据流以将营销自动化数据引入平台](../../dataflow/marketing-automation.md).
