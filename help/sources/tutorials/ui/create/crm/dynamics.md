---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Microsoft Dynamics源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# 在UI [!DNL Microsoft Dynamics] 中创建源连接器

Adobe Experience Platform的源连接器提供按计划收集外部源CRM数据的能力。 本教程提供了使用用 [!DNL Microsoft Dynamics] 户界面创建(下[!DNL Dynamics]称“”)源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的 [!DNL Dynamics] 帐户，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/crm.md)。

### 收集所需的凭据

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUri` | 实例的服务 [!DNL Dynamics] URL。 |
| `username` | 您的用户帐户 [!DNL Dynamics] 的用户名。 |
| `password` | Dynamics帐户的密码。 |

有关快速入门的更多信息，请访 [问此Dynamics文档](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

## 连接帐 [!DNL Dynamics] 户

收集所需凭据后，您可以按照以下步骤创建要连 [!DNL Dynamics] 接的新帐户 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 *[!UICONTROL “源”以访问]* “源”工作区。 “目 *[!UICONTROL 录]* ”屏幕显示可为其创建入站帐户的各种源，每个源显示与它们关联的现有帐户和数据集流的数量。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 *[!UICONTROL 据库]* ”类别下，选 **[!UICONTROL 择]** Dynamics **[!UICONTROL ，然]** 后选择Add data [!DNL Dynamics] ，以创建新连接器。

![目录](../../../../images/tutorials/create/ms-dynamics/catalog.png)

此时 *[!UICONTROL 将显示“连接到]* Dynamics”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供连接的名称、可选说明和凭 [!DNL Dynamics] 据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新帐户。

![connect](../../../../images/tutorials/create/ms-dynamics/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL Dynamics] 要连接的帐户，然后选择右 **[!UICONTROL 上]** 角的“下一步”以继续。

![现有](../../../../images/tutorials/create/ms-dynamics/existing.png)

## 后续步骤

按照本教程，您已建立了与帐户的 [!DNL Dynamics] 连接。 您现在可以继续阅读下一个教程， [并配置数据流以将数据引入平台](../../dataflow/crm.md)。