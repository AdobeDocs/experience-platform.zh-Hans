---
title: 使用Platform UI创建OracleEloqua源连接
description: 了解如何使用Platform UI将Adobe Experience Platform连接到OracleEloqua。
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---

# 使用Platform UI创建[!DNL Oracle Eloqua]源连接

本教程提供了使用Adobe Experience Platform用户界面创建[!DNL Oracle Eloqua]源连接的步骤。

## 快速入门

本指南要求您对Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Platform允许从各种源摄取数据，同时允许您使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Platform提供了将单个Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

如果您在Platform上已经拥有经过身份验证的[!DNL Oracle Eloqua]帐户，则可以跳过本文档的其余部分，并继续阅读有关[创建数据流以将营销自动化数据引入Platform](../../dataflow/marketing-automation.md)的教程。

### 收集所需的凭据

为了将[!DNL Oracle Eloqua]连接到Platform，您必须提供以下身份验证属性的值：

| 凭据 | 描述 |
| --- | --- |
| 终结点 | [!DNL Oracle Eloqua]服务器的端点。 [!DNL Oracle Eloqua]支持多个数据中心。 要查找您的端点，请使用您的凭据登录到[[!DNL Oracle Eloqua] 接口](https://login.eloqua.com)，然后从重定向URL复制基本URL部分。 URL模式的格式为`xxx.xx.eloqua.com`，输入时应不带`http`或`https`。 |
| 用户名 | [!DNL Oracle Eloqua]服务器的用户名。 用户名必须设置为`siteName + \\ + username`格式，其中`siteName`是您用于登录到[!DNL Oracle Eloqua]的公司名称，`username`是您的用户名。 例如，您的登录用户名可以是： `Eloqua\Andy`。 **注意**：在使用UI时，必须使用单个反斜杠(`\`)，因为Experience PlatformUI在输入用户名时会自动添加一个额外的反斜杠(`\`)。 |
| 密码 | 与您的[!DNL Oracle Eloqua]用户名对应的密码。 |

有关[!DNL Oracle Eloqua]的身份验证凭据的详细信息，请参阅有关身份验证](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html)的[[!DNL Oracle Eloqua] 指南。

收集所需的凭据后，您可以按照以下步骤将您的[!DNL Oracle Eloqua]帐户关联到Platform。

## 连接您的[!DNL Oracle Eloqua]帐户

在Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在[!UICONTROL 营销自动化]类别下，选择&#x200B;**[!UICONTROL OracleEloqua]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![目录](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

出现&#x200B;**[!UICONTROL 连接OracleEloqua帐户]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

要使用现有帐户，请选择要用于创建新数据流的[!DNL Oracle Eloqua]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### 新帐户

如果要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后为[!DNL Oracle Eloqua]凭据提供名称、可选描述和相应的值。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

![新](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 后续步骤

通过学习本教程，您已验证并创建了[!DNL Oracle Eloqua]帐户和平台之间的源连接。 您现在可以继续下一教程，并[创建数据流以将营销自动化数据引入Platform](../../dataflow/marketing-automation.md)。
