---
keywords: Experience Platform；主页；热门主题；来源；连接器；oracle;oracle雄辩；雄辩
solution: Experience Platform
title: 使用Platform UI创建OracleEloqua源连接
topic-legacy: tutorial
description: 了解如何使用Platform UI将Adobe Experience Platform连接到OracleEloqua。
source-git-commit: a40a1b8fae41c495afd9cdfc3c8d68148e90f2cd
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---


# 创建 [!DNL Oracle Eloqua] 源连接（使用Platform UI）

本教程提供了创建 [!DNL Oracle Eloqua] 源连接器。

## 快速入门

本指南要求您对平台的以下组件有充分的了解：

* [源](../../../../home.md):Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

如果您已经过身份验证 [!DNL Oracle Eloqua] 帐户，则您可以跳过本文档的其余部分，并继续阅读上的教程 [创建数据流以将营销自动化数据引入平台](../../dataflow/marketing-automation.md).

### 收集所需的凭据

为了连接 [!DNL Oracle Eloqua] 对于平台，必须为以下身份验证属性提供值：

| 凭据 | 描述 |
| --- | --- |
| 端点 | 您的 [!DNL Oracle Eloqua]. |
| 用户名 | 您的用户名 [!DNL Oracle Eloqua] 帐户。 用户名的格式必须为 `siteName + \\ + username`，其中 `siteName` 是您用来登录的公司名称 [!DNL Oracle Eloqua] 和 `username` 是您的用户名。 例如，您的登录用户名可以是： `adobe\\emily`. |
| 密码 | 与您的 [!DNL Oracle Eloqua] 用户名。 |

有关的身份验证凭据的详细信息 [!DNL Oracle Eloqua]，请参阅 [[!DNL Oracle Eloqua] 认证指南](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

收集所需的凭据后，您可以按照以下步骤链接 [!DNL Oracle Eloqua] 帐户到平台。

## 连接 [!DNL Oracle Eloqua] 帐户

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 [!UICONTROL 营销自动化] 类别，选择 **[!UICONTROL Oracle雄辩]**，然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

的 **[!UICONTROL 连接OracleEloqua帐户]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL Oracle Eloqua] 创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为您提供名称、可选描述和相应的值 [!DNL Oracle Eloqua] 凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后，再留出一些时间建立新连接。

![新建](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 后续步骤

通过本教程，您已通过身份验证，并在 [!DNL Oracle Eloqua] 帐户和平台。 您现在可以继续下一个教程和 [创建数据流以将营销自动化数据引入平台](../../dataflow/marketing-automation.md).

