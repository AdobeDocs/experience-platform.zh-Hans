---
title: 在UI中创建Amazon Redshift源连接
description: 了解如何使用Adobe Experience Platform UI创建Amazon Redshift源连接。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 2%

---

# 连接您的 [!DNL Amazon Redshift] 使用源工作区的帐户

>[!IMPORTANT]
>
>此 [!DNL Amazon Redshift] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

本教程提供了有关如何连接 [!DNL Amazon Redshift] (以下简称“[!DNL Redshift]&quot;)帐户登录到Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   - [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   - [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Redshift] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/databases.md).

### 收集所需的凭据

要访问 [!DNL Redshift] account on account(Experience Platform帐户)，您必须提供以下值：

| **凭据** | **描述** |
| -------------- | --------------- |
| Server | 与您的关联的服务器 [!DNL Redshift] 帐户。 |
| 端口 | TCP端口 [!DNL Redshift] 服务器使用来侦听客户端连接。 |
| 用户名 | 与您的关联的用户名 [!DNL Redshift] 帐户。 |
| 密码 | 与您的关联的密码 [!DNL Redshift] 帐户。 |
| 数据库 | 此 [!DNL Redshift] 正在访问的数据库。 |

有关入门的更多信息，请参阅 [此 [!DNL Redshift] 文档](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL Redshift] 帐户到Experience Platform。

## 连接您的 [!DNL Redshift] 帐户

>[!NOTE]
>
>的默认编码标准 [!DNL Redshift] 是Unicode。 无法更改此设置。

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问 **[!UICONTROL 源]** 工作区。 此 **[!UICONTROL 目录]** 屏幕显示了多种来源，您可以使用这些来源创建帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 **[!UICONTROL 数据库]** 类别，选择 **[!UICONTROL Amazon Redshift]**. 如果这是您第一次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，选择 **[!UICONTROL 添加数据]** 以新建 [!DNL Redshift] 连接器。

![](../../../../images/tutorials/create/redshift/catalog.png)

此 **[!UICONTROL 连接到Amazon Redshift]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在出现的输入表单上，提供名称、可选描述以及 [!DNL Redshift] 凭据。 完成后，选择 **[!UICONTROL 连接]** 然后等待一段时间以建立新连接。

![](../../../../images/tutorials/create/redshift/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL Redshift] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/redshift/existing.png)

## 后续步骤

通过学习本教程，您已建立与的连接 [!DNL Redshift] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据引入Experience Platform](../../dataflow/databases.md).
