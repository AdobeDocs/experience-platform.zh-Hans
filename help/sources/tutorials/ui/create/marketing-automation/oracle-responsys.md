---
keywords: Experience Platform；主页；热门主题；源；连接器；oracle；
title: (Beta)使用平台UI创建OracleResponsys源连接
description: 了解如何使用Platform UI将Adobe Experience Platform连接到OracleResponsys。
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 2%

---

# (Beta)使用平台UI创建[!DNL Oracle Responsys]源连接

>[!NOTE]
>
>[!DNL Oracle Responsys]源为测试版。 有关使用带有Beta标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

本教程提供了使用Adobe Experience Platform用户界面创建[[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md)源连接的步骤。

## 快速入门

本指南要求您对Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Platform允许从各种源摄取数据，同时允许您使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Platform提供了将单个Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

如果您在Platform上已经拥有经过身份验证的[!DNL Oracle Responsys]帐户，则可以跳过本文档的其余部分，并继续阅读有关[创建数据流以将营销自动化数据引入Platform](../../dataflow/marketing-automation.md)的教程。

### 收集所需的凭据

为了将[!DNL Oracle Responsys]连接到Platform，您必须提供以下身份验证属性的值：

| 凭据 | 描述 |
| --- | --- |
| 终结点 | [!DNL Oracle Responsys]实例的REST身份验证终结点URL。 |
| 客户端 ID | [!DNL Oracle Responsys]实例的客户端ID。 |
| 客户端密码 | [!DNL Oracle Responsys]实例的客户端密钥。 |

有关[!DNL Oracle Responsys]的身份验证凭据的详细信息，请参阅有关身份验证](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm)的[[!DNL Oracle Responsys] 指南。

收集所需的凭据后，您可以按照以下步骤将您的[!DNL Oracle Responsys]帐户关联到Platform。

## 连接您的[!DNL Oracle Responsys]帐户

在Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在[!UICONTROL 营销自动化]类别下，选择&#x200B;**[!UICONTROL OracleResponsys]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![Oracle为Responsys源的Adobe Experience Platform源目录突出显示。](../../../../images/tutorials/create/oracle-responsys/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接OracleResponsys帐户]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

要使用现有帐户，请选择要用于创建新数据流的[!DNL Oracle Responsys]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![OracleResponsys的现有帐户身份验证屏幕。](../../../../images/tutorials/create/oracle-responsys/existing.png)

### 新帐户

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后为[!DNL Oracle Responsys]凭据提供名称、可选描述和相应的值。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

![OracleResponsys的新帐户身份验证屏幕。](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 后续步骤

通过学习本教程，您已验证并创建了[!DNL Oracle Responsys]帐户和平台之间的源连接。 您现在可以继续下一教程，并[创建数据流以将营销自动化数据引入Platform](../../dataflow/marketing-automation.md)。
