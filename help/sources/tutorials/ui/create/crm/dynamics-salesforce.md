---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Microsoft Dynamics或Salesforce源连接器
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# 在UI中创建Microsoft Dynamics或Salesforce源连接器

Adobe Experience Platform中的源连接器提供了按计划收集外部来源的CRM数据的能力。 本教程提供了使用平台用户界面创建Microsoft Dynamics（以下简称“Dynamics”）或Salesforce源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

如果您已有Microsoft Dynamics或Salesforce基本连接，则可以跳过本文档的其余部分，继续学习配置数据 [流的教程](../../dataflow/crm.md)。

### 收集所需的凭据

要在平台上访问您的Dynamics帐户，必须提供服 **务URI**、 **用户名**&#x200B;和密 **码**。

同样，在平台上访问您的Salesforce帐户需要您提供 **环境URL**、 **用户名**、 **密码******&#x200B;和安全令牌。

## 连接您的Dynamics或Salesforce帐户

在您的CRM系统凭据准备就绪后，您可以按照以下步骤创建新的入站基本连接，以将您的Dynamics或Salesforce帐户关联到平台。

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左侧导航栏 **中选择源** ，以访问源工作区。 “目 *录* ”屏幕显示各种来源，您可以为其创建入站基本连接，每个来源显示与这些来源关联的现有基本连接的数量。

在 *CRM类别下* ，选择 **Microsoft Dynamics** 或 **Salesforce** ，以在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短说明以及视图其文档或与源连接的选项。 要创建新的入站基本连接，请单击“ **Connect源”**。

![](../../../../images/tutorials/create/salesforce/sf_sources_catalog.png)

在输入表单中，为基本连接提供名称、可选说明以及动态或Salesforce凭据。 最后，单击 **Connect** ，然后为建立新的基本连接留出一些时间。

![](../../../../images/tutorials/create/salesforce/sf_credentials.png)

建立与CRM系统的基本连接后，您可以继续执行下一节，并配置数据流以将CRM数据引入平台。

## 后续步骤

通过遵循本教程，您已经建立了与Dynamics或Salesforce帐户的基本连接。 您现在可以继续阅读下一个教程，并 [配置一个数据流以将数据引入平台](../../dataflow/crm.md)。