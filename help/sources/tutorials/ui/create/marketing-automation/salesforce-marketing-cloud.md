---
title: 通过UI将您的Salesforce Marketing Cloud帐户连接到Experience Platform
description: 了解如何通过UI将您的Salesforce Marketing Cloud帐户连接到Experience Platform。
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 0c6a51d06e57eb6de063a350bd4b17022555a0b4
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# 通过UI将您的[!DNL Salesforce Marketing Cloud]帐户连接到Experience Platform

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud]源将于2026年1月被弃用。 作为替代方案，将在今年晚些时候发布新的信息源。 发布新源后，您必须计划在2026年1月底之前通过创建新帐户连接和数据流迁移到新源。

阅读本指南，了解如何使用Experience Platform用户界面中的源工作区将您的[!DNL Salesforce Marketing Cloud]帐户连接到Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有[!DNL Salesforce Marketing Cloud]帐户，则可以跳过本文档的其余部分，并继续学习关于使用UI[&#128279;](../../dataflow/marketing-automation.md)将营销自动化数据引入Experience Platform的教程。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Salesforce Marketing Cloud] 概述](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#prerequisites)。

## 导航源目录

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]源集成当前不支持自定义对象摄取。


在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;*[!UICONTROL 源]*&#x200B;工作区。 选择类别或使用搜索栏查找您的源。

要连接到[!DNL Salesforce Marketing Cloud]，请转到&#x200B;*[!UICONTROL 营销自动化]*&#x200B;类别，选择&#x200B;**[!UICONTROL Salesforce Marketing Cloud]**&#x200B;源卡，然后选择&#x200B;**[!UICONTROL 设置]**。

>[!TIP]
>
>当给定的源尚未具有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL 设置]**&#x200B;选项。 创建经过身份验证的帐户后，此选项将更改为&#x200B;**[!UICONTROL 添加数据]**。

![已选择Salesforce Marketing Cloud源卡的源目录。](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

## 使用现有帐户 {#existing}

若要使用现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后选择要使用的[!DNL Salesforce Marketing Cloud]帐户。

![源工作流中已选择“现有帐户”的现有帐户接口。](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 创建新帐户 {#new}

您可以使用[!DNL Salesforce Marketing Cloud]源连接到[!DNL Azure]或[!DNL Amazon Web Services]上的Experience Platform (AWS)。

### 连接到[!DNL Azure]上的Experience Platform {#azure}

要连接到[!DNL Azure]上的Experience Platform，请提供帐户名称、可选描述以及您的[帐户身份验证凭据](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#azure)。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，等待一段时间以建立连接。

![源工作流中用于连接到Azure上Experience Platform的新帐户接口。](../../../../images/tutorials/create/salesforce-marketing-cloud/new-azure.png)

### 连接到Amazon Web Services上的Experience Platform (AWS) {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../../../landing/multi-cloud.md)。

要连接到[!DNL AWS]上的Experience Platform，请确保您位于VA6沙盒中，并提供帐户名称、可选描述以及您的[帐户身份验证凭据](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#aws)。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，等待一段时间以建立连接。

![源工作流中用于连接到AWS上Experience Platform的新帐户接口](../../../../images/tutorials/create/salesforce-marketing-cloud/new-aws.png)

## 为[!DNL Salesforce Marketing Cloud]数据创建数据流

现在您已成功连接[!DNL Salesforce Marketing Cloud]，您现在可以[创建数据流并将营销自动化提供商中的数据摄取到Experience Platform](../../dataflow/marketing-automation.md)。
