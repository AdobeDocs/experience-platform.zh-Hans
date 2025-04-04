---
title: 使用UI将AWS Redshift连接到Experience Platform
description: 了解如何使用源UI将AWS Redshift帐户连接到Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 2%

---

# 使用UI将[!DNL AWS Redshift]连接到Experience Platform

>[!IMPORTANT]
>
>[!DNL AWS Redshift]源在源目录中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。

阅读本指南，了解如何使用UI中的源工作区将您的[!DNL AWS Redshift]帐户连接到Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   - [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   - [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL AWS Redshift]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/databases.md)的教程。

## 导航源目录

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;*[!UICONTROL 数据库]*&#x200B;类别下选择&#x200B;**[!DNL AWS Redshift]**，然后选择&#x200B;**[!UICONTROL 设置]**。

>[!TIP]
>
>当给定的源尚未具有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL 设置]**&#x200B;选项。 一旦存在经过身份验证的帐户，此选项将更改为&#x200B;**[!UICONTROL 添加数据]**。

![已选择AWS Redshift源卡的源目录。](../../../../images/tutorials/create/redshift/catalog.png)

## 使用现有帐户 {#existing}

接下来，您将进入源工作流的身份验证步骤。 在此，您可以使用现有帐户或创建新帐户。

若要使用现有帐户，请从帐户目录中选择[!DNL AWS Redshift]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![此处列出了源工作流中现有帐户的帐户目录。](../../../../images/tutorials/create/redshift/existing.png)

## 创建新帐户 {#create}

如果您没有现有帐户，则必须通过提供与您的源对应的必需身份验证凭据来创建新帐户。

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后提供名称并选择性地为您的帐户添加描述。

### 连接到Azure上的Experience Platform {#azure}

若要将你的[!DNL AWS Redshift]帐户连接到Azure上的Experience Platform，请在输入表单中提供你的身份验证凭据，然后选择&#x200B;**（[!UICONTROL 连接到源]）**。

![用于将AWS Redshift连接到Azure上的Experience Platform的新帐户接口。](../../../../images/tutorials/create/redshift/new.png)

| 凭据 | 描述 |
| --- | --- |
| Server | [!DNL AWS Redshift]实例的服务器名称。 |
| 端口 | [!DNL AWS Redshift]服务器用于侦听客户端连接的TCP端口。 |
| 用户名 | 要授予访问权限的帐户的用户名。 |
| 密码 | 与用户帐户对应的密码。 |
| 数据库 | 从中获取数据的[!DNL AWS Redshift]数据库。 |

有关入门的详细信息，请参阅[此 [!DNL AWS Redshift] 文档](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html)。

### 连接到AWS上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本节适用于在AWS Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../../../landing/multi-cloud.md)。

若要创建新[!DNL AWS Redshift]帐户并连接到AWS上的Experience Platform，请确保您位于VA6沙盒中，提供身份验证所需的凭据，然后选择&#x200B;**[!UICONTROL 连接到源]**。

![用于将AWS Redshift连接到AWS上的Experience Platform的新帐户界面。](../../../../images/tutorials/create/redshift/aws-auth.png)

| 凭据 | 描述 |
| --- | --- |
| Server | [!DNL AWS Redshift]实例的服务器名称。 |
| 端口 | [!DNL AWS Redshift]服务器用于侦听客户端连接的TCP端口。 |
| 用户名 | 要授予访问权限的帐户的用户名。 |
| 密码 | 与用户帐户对应的密码。 |
| 数据库 | 从中获取数据的[!DNL AWS Redshift]数据库。 |
| 架构 | 与您的[!DNL AWS Redshift]数据库关联的架构的名称。 您必须确保要为其授予数据库访问权限的用户也具有此架构的访问权限。 |

有关入门的详细信息，请参阅[此 [!DNL AWS Redshift] 文档](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html)。

## 后续步骤

通过学习本教程，您已在[!DNL AWS Redshift]数据库与Experience Platform之间建立连接。 您现在可以继续下一教程，并[创建数据流以将数据从数据库摄取到Experience Platform](../../dataflow/databases.md)。