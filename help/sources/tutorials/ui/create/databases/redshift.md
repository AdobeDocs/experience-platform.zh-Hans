---
title: 在UI中创建Amazon Redshift Source连接
description: 了解如何使用Adobe Experience Platform UI创建Amazon Redshift源连接。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 3%

---

# 使用源工作区连接您的[!DNL Amazon Redshift]帐户

>[!IMPORTANT]
>
>[!DNL Amazon Redshift]源在源目录中可供已购买Real-time Customer Data Platform Ultimate的用户使用。

本教程提供了有关如何使用用户界面将您的[!DNL Amazon Redshift]（以下称为“[!DNL Redshift]”）帐户连接到Adobe Experience Platform的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   - [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   - [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL Redshift]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

要在Experience Platform上访问您的[!DNL Redshift]帐户，必须提供以下值：

| **凭据** | **描述** |
| -------------- | --------------- |
| Server | 与您的[!DNL Redshift]帐户关联的服务器。 |
| 端口 | [!DNL Redshift]服务器用于侦听客户端连接的TCP端口。 |
| 用户名 | 与您的[!DNL Redshift]帐户关联的用户名。 |
| 密码 | 与您的[!DNL Redshift]帐户关联的密码。 |
| 数据库 | 您正在访问的[!DNL Redshift]数据库。 |

有关入门的详细信息，请参阅[此 [!DNL Redshift] 文档](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)。

收集所需的凭据后，您可以按照以下步骤将您的[!DNL Redshift]帐户关联到Experience Platform。

## 连接您的[!DNL Redshift]帐户

>[!NOTE]
>
>[!DNL Redshift]的默认编码标准为Unicode。 无法更改此设置。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;**[!UICONTROL 数据库]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Amazon Redshift]**。 如果这是您第一次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，请选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的[!DNL Redshift]连接器。

![](../../../../images/tutorials/create/redshift/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到Amazon Redshift]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入表单上，提供名称、可选描述和您的[!DNL Redshift]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后留出一些时间来建立新连接。

![](../../../../images/tutorials/create/redshift/new.png)

### 现有账户

若要连接现有帐户，请选择您要连接的[!DNL Redshift]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![](../../../../images/tutorials/create/redshift/existing.png)

## 后续步骤

通过学习本教程，您已建立与[!DNL Redshift]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入Experience Platform](../../dataflow/databases.md)。
