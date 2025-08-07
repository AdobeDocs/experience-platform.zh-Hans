---
title: 使用UI将Oracle DB连接到Experience Platform
description: 了解如何使用UI将Oracle数据库实例连接到Experience Platform。
exl-id: 4ca6ecc6-0382-4cee-acc5-1dec7eeb9443
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 在用户界面中创建[!DNL Oracle DB]源连接

阅读本指南，了解如何使用Experience Platform用户界面中的源工作区将您的[!DNL Oracle DB]实例连接到Adobe Experience Platform。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经有[!DNL Oracle DB]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Oracle DB] 概述](../../../../connectors/databases/oracle.md#prerequisites)。

## 导航源目录

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;*[!UICONTROL 源]*&#x200B;工作区。 选择类别或使用搜索栏查找您的源。

若要连接到[!DNL Oracle DB]，请转到&#x200B;*[!UICONTROL 数据库]*&#x200B;类别，选择&#x200B;**[!UICONTROL Oracle DB]**&#x200B;源卡，然后选择&#x200B;**[!UICONTROL 设置]**。

>[!TIP]
>
>源显示&#x200B;**[!UICONTROL 为新连接设置]**，如果帐户已存在，则显示&#x200B;**[!UICONTROL 添加数据]**。

![已选择“Oracle DB”的源目录。](../../../../images/tutorials/create/oracle/catalog.png)

## 使用现有帐户 {#existing}

若要使用现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后选择要使用的[!DNL Oracle DB]帐户。

![源工作流中已选择“现有帐户”的现有帐户接口。](../../../../images/tutorials/create/oracle/existing.png)

## 创建新帐户 {#new}

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后提供名称并选择性地为您的帐户添加描述。

### 连接到Azure上的Experience Platform {#azure}

您可以使用连接字符串将[!DNL Oracle DB]数据库连接到Azure上的Experience Platform。

若要使用连接字符串身份验证，请提供您的[连接字符串](../../../../connectors/databases/oracle.md#azure)并选择&#x200B;**[!UICONTROL 连接到源]**。

![源工作流中的新帐户接口已选中“连接字符串身份验证”。](../../../../images/tutorials/create/oracle/azure.png)

### 连接到Amazon Web Services上的Experience Platform (AWS) {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../../../landing/multi-cloud.md)。

要创建新的[!DNL Oracle DB]帐户并连接到AWS上的Experience Platform，请确保您处于VA6沙盒中，然后提供身份验证所需的[凭据](../../../../connectors/databases/oracle.md#aws)。

![源工作流中用于连接到AWS的新帐户接口。](../../../../images/tutorials/create/oracle/aws.png)

## 为[!DNL Oracle DB]数据创建数据流

现在您已成功连接[!DNL Oracle DB]数据库，您现在可以[创建数据流并将数据库中的数据摄取到Experience Platform](../../dataflow/databases.md)。
