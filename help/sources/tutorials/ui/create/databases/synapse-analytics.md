---
title: 在UI中创建Azure Synapse Analytics Source连接
description: 了解如何使用Adobe Experience Platform UI创建Azure Synapse Analytics（以下简称“Synapse”）源连接。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 1f1ce317-eaaf-4ad2-a5fb-236983220bd7
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# 在用户界面中创建[!DNL Azure Synapse Analytics]源连接

>[!IMPORTANT]
>
>[!DNL Azure Synapse Analytics]源在源目录中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。

阅读本指南，了解如何使用UI中的源工作区将您的[!DNL Azure Synapse Analytics]帐户连接到Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL Azure Synapse Analytics]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Azure Synapse Analytics] 概述](../../../../connectors/databases/synapse-analytics.md#prerequisites)。

## 导航源目录

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;*[!UICONTROL 源]*&#x200B;工作区。 选择类别或使用搜索栏查找您的源。

要连接到[!DNL Azure Synapse Analytics]，请转到&#x200B;*[!UICONTROL 数据库]*&#x200B;类别，选择&#x200B;**[!UICONTROL Azure Synapse analytics]**&#x200B;源卡，然后选择&#x200B;**[!UICONTROL 设置]**。

>[!TIP]
>
>当给定的源尚未具有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL 设置]**&#x200B;选项。 创建经过身份验证的帐户后，此选项将更改为&#x200B;**[!UICONTROL 添加数据]**。

![已选择“Azure Synapse Analytics”的源目录。](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

## 使用现有帐户 {#existing}

若要使用现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后选择要使用的[!DNL Azure Synapse Analytics]帐户。

![源工作流的现有帐户接口。](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## 创建新帐户 {#new}

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后提供名称并选择性地为您的帐户添加描述。

![源工作流的新帐户接口。](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### 连接到Experience Platform

您可以使用帐户密钥身份验证或服务主体和密钥身份验证将[!DNL Azure Synapse Analytics]帐户连接到Experience Platform。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

若要使用帐户密钥身份验证，请选择&#x200B;**[!UICONTROL 帐户密钥身份验证]**，提供您的[连接字符串](../../../../connectors/databases/synapse-analytics.md#prerequisites)，然后选择&#x200B;**[!UICONTROL 连接到源]**。

![源工作流中的“创建新帐户”步骤，其中选择了“帐户密钥身份验证”。](../../../../images/tutorials/create/azure-synapse-analytics/account-key-auth.png)

>[!TAB 服务主体和密钥身份验证]

或者，选择&#x200B;**[!UICONTROL 服务主体和密钥身份验证]**，提供[身份验证凭据](../../../../connectors/databases/synapse-analytics.md#prerequisites)的值，然后选择&#x200B;**[!UICONTROL 连接到源]**。

![源工作流中已选择“服务主体和密钥身份验证”的“创建新帐户”步骤。](../../../../images/tutorials/create/azure-synapse-analytics/service-principal.png)

>[!ENDTABS]

## 为[!DNL Azure Synapse Analytics]数据创建数据流

现在您已成功连接[!DNL Azure Synapse Analytics]数据库，您现在可以[创建数据流并将数据库中的数据摄取到Experience Platform](../../dataflow/databases.md)。
