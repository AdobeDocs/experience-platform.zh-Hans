---
keywords: Experience Platform;home;popular topics;ServiceNow;servicenow
solution: Experience Platform
title: 在UI中创建ServiceNow源连接器
topic: overview
description: 本教程提供了使用平台用户界面创建ServiceNow源连接器的步骤。
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---


# 在UI [!DNL ServiceNow] 中创建源连接器

>[!NOTE]
>
>连接 [!DNL ServiceNow] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用户界 [!DNL ServiceNow] 面创建源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有有效的连 [!DNL ServiceNow] 接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/customer-success.md)

### 收集所需的凭据

要访问您的帐 [!DNL ServiceNow] 户， [!DNL Platform]您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | The endpoint of the [!DNL ServiceNow] server. |
| `username` | 用于连接到服务器进行身 [!DNL ServiceNow] 份验证的用户名。 |
| `password` | 连接到服务器进行身 [!DNL ServiceNow] 份验证的口令。 |

有关快速入门的详细信息，请参 [ [!DNL ServiceNow] 阅本文档](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)。

## 连接帐 [!DNL ServiceNow] 户

收集所需凭据后，您可以按照以下步骤将帐户链 [!DNL ServiceNow] 接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“客户 **[!UICONTROL 成功类别]** ”下，选 **[!UICONTROL 择ServiceNow]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选 **[!UICONTROL 择Connect源]** ，创建新连 [!DNL ServiceNow] 接器。

![](../../../../images/tutorials/create/servicenow/catalog.png)

将显 **[!UICONTROL 示“连接到ServiceNow]** ”页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和凭 [!DNL ServiceNow] 据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![](../../../../images/tutorials/create/servicenow/new.png)

### 现有帐户

要连接现有帐户，请选 [!DNL ServiceNow] 择要连接的帐户，然后选择 **[!UICONTROL 下一]** 步以继续。

![](../../../../images/tutorials/create/servicenow/existing.png)

## 后续步骤

按照本教程，您已建立了与帐户的 [!DNL ServiceNow] 连接。 您现在可以继续学习下一个教程， [并配置一个数据流以将数据引入 [!DNL Platform]](../../dataflow/customer-success.md)。
