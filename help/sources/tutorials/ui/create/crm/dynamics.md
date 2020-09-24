---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: 在UI中创建Microsoft Dynamics源连接器
topic: overview
type: Tutorial
description: 本教程提供了使用平台用户界面创建Microsoft Dynamics（以下称“Dynamics”）源连接器的步骤。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---


# 在UI [!DNL Microsoft Dynamics] 中创建源连接器

Adobe Experience Platform的源连接器提供按计划收集外部源CRM数据的能力。 本教程提供了使用用 [!DNL Microsoft Dynamics] 户界面创建(下[!DNL Dynamics]称“”)源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的 [!DNL Dynamics] 帐户，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/crm.md)。

### 收集所需的凭据

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUri` | 实例的服务 [!DNL Dynamics] URL。 |
| `username` | 您的用户帐户 [!DNL Dynamics] 的用户名。 |
| `password` | 帐户的密 [!DNL Dynamics] 码。 |

有关快速入门的详细信息，请参 [ [!DNL Dynamics] 阅本文档](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

## 连接帐 [!DNL Dynamics] 户

收集所需凭据后，您可以按照以下步骤将帐户链 [!DNL Dynamics] 接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数据 **[!UICONTROL 库]** ”类别下，选 **[!UICONTROL 择Dynamics]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选择 **[!UICONTROL 添加数据]** ，以创建新连 [!DNL Dynamics] 接器。

![目录](../../../../images/tutorials/create/ms-dynamics/catalog.png)

此时 **[!UICONTROL 将显示“连接到]** Dynamics”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和凭 [!DNL Dynamics] 据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![connect](../../../../images/tutorials/create/ms-dynamics/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL Dynamics] 要连接的帐户，然后选择右 **[!UICONTROL 上]** 角的“下一步”以继续。

![现有](../../../../images/tutorials/create/ms-dynamics/existing.png)

## 后续步骤

按照本教程，您已建立了与帐户的 [!DNL Dynamics] 连接。 您现在可以继续学习下一个教程， [并配置一个数据流以将数据引入 [!DNL Platform]](../../dataflow/crm.md)。