---
keywords: Experience Platform；主页；热门主题；Microsoft Dynamics;microsoft Dynamics;Dynamics;Dynamics
solution: Experience Platform
title: 在UI中创建Microsoft Dynamics源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Microsoft Dynamics源连接。
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# 在UI中创建[!DNL Microsoft Dynamics]源连接

本教程提供了使用Adobe Experience Platform UI创建[!DNL Microsoft Dynamics]（以下称“[!DNL Dynamics]”）源连接的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成的基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

如果您已经有有效的[!DNL Dynamics]帐户，则可以跳过此文档的其余部分，继续学习有关[为CRM源](../../dataflow/crm.md)配置数据流的教程。

### 收集所需凭据

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUri` | [!DNL Dynamics]实例的服务URL。 |
| `username` | [!DNL Dynamics]用户帐户的用户名。 |
| `password` | [!DNL Dynamics]帐户的密码。 |
| `servicePrincipalId` | [!DNL Dynamics]帐户的客户端ID。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `servicePrincipalKey` | 服务主密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |

有关快速入门的详细信息，请参阅[this [!DNL Dynamics] 文档](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

## 连接您的[!DNL Dynamics]帐户

收集所需凭据后，您可以按照以下步骤将您的[!DNL Dynamics]帐户链接到平台。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示了可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在&#x200B;**[!UICONTROL CRM]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Microsoft Dynamics]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL Configure]**。 否则，选择&#x200B;**[!UICONTROL Add data]**&#x200B;以创建新[!DNL Dynamics]连接器。

![目录](../../../../images/tutorials/create/ms-dynamics/catalog.png)

将显示&#x200B;**[!UICONTROL Connect to Dynamics]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择&#x200B;**[!UICONTROL New account]**。 在显示的输入表单上，为新[!DNL Dynamics]帐户提供名称和可选说明。

[!DNL Dynamics]连接器为您提供了不同的访问身份验证类型。 在[!UICONTROL Account authentication]下，选择&#x200B;**[!UICONTROL Basic authentication]**&#x200B;以使用基于密码的凭据。

完成后，选择&#x200B;**[!UICONTROL Connect to source]**，然后为新帐户建立留出一些时间。

![基本身份验证](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

或者，您也可以选择&#x200B;**[!UICONTROL Service-principal and key authentication]**&#x200B;并使用[!UICONTROL Service principal ID]和[!UICONTROL Service principal key]的组合连接您的[!DNL Dynamics]帐户。

>[!IMPORTANT]
>
> [!DNL Dynamics]中的基本身份验证可能会被双因素身份验证阻止，而平台当前不支持双因素身份验证。 在这种情况下，建议使用基于密钥的身份验证来创建使用[!DNL Dynamics]的源连接器。

![基于密钥的身份验证](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| 凭据 | 描述 |
| ---------- | ----------- |
| [!UICONTROL Service principal ID] | [!DNL Dynamics]帐户的客户端ID。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| [!UICONTROL Service principal key] | 服务主密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |

### 现有帐户

要连接现有帐户，请选择要连接的[!DNL Dynamics]帐户，然后选择右上角的&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/ms-dynamics/existing.png)

## 后续步骤

按照本教程，您已建立了与[!DNL Dynamics]帐户的连接。 您现在可以继续下一个教程，并[配置一个数据流以将数据导入Platform](../../dataflow/crm.md)。
