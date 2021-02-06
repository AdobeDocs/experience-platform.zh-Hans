---
keywords: Experience Platform；主页；热门主题；Microsoft Dynamics;microsoft Dynamics;Dynamics;Dynamics
solution: Experience Platform
title: 在UI中创建Microsoft Dynamics源连接
topic: overview
type: Tutorial
description: 了解如何使用Adobe Experience PlatformUI创建Microsoft Dynamics源连接。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---


# 在UI中创建[!DNL Microsoft Dynamics]源连接

本教程提供了使用Adobe Experience PlatformUI创建[!DNL Microsoft Dynamics]（以下称“[!DNL Dynamics]”）源连接的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的[!DNL Dynamics]帐户，您可以跳过此文档的其余部分，继续学习有关为CRM源](../../dataflow/crm.md)配置数据流的教程。[

### 收集所需的凭据

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUri` | [!DNL Dynamics]实例的服务URL。 |
| `username` | [!DNL Dynamics]用户帐户的用户名。 |
| `password` | [!DNL Dynamics]帐户的口令。 |
| `servicePrincipalId` | [!DNL Dynamics]帐户的客户端ID。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `servicePrincipalKey` | 服务主密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |

有关入门的详细信息，请参阅[this [!DNL Dynamics] 文档](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

## 连接您的[!DNL Dynamics]帐户

收集所需凭据后，您可以按照以下步骤将[!DNL Dynamics]帐户链接到平台。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 **[!UICONTROL 目录]**&#x200B;屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在&#x200B;**[!UICONTROL CRM]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Microsoft Dynamics]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的[!DNL Dynamics]连接器。

![目录](../../../../images/tutorials/create/ms-dynamics/catalog.png)

将显示&#x200B;**[!UICONTROL 连接到Dynamics]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择&#x200B;**[!UICONTROL 新建帐户]**。 在显示的输入表单上，为新[!DNL Dynamics]帐户提供名称和可选说明。

[!DNL Dynamics]连接器为访问提供不同的身份验证类型。 在[!UICONTROL 帐户身份验证]下，选择&#x200B;**[!UICONTROL 基本身份验证]**&#x200B;以使用基于口令的凭据。

完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后为新帐户建立留出一些时间。

![基本身份验证](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

或者，您也可以选择&#x200B;**[!UICONTROL 服务主体和密钥身份验证]**，并使用[!UICONTROL 服务主体ID]和[!UICONTROL 服务主体密钥]的组合连接您的[!DNL Dynamics]帐户。

>[!IMPORTANT]
>
> [!DNL Dynamics]中的基本身份验证可能会被双因素身份验证阻止，平台当前不支持双因素身份验证。 在这种情况下，建议使用基于密钥的身份验证来创建使用[!DNL Dynamics]的源连接器。

![基于密钥的身份验证](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| 凭据 | 描述 |
| ---------- | ----------- |
| [!UICONTROL 服务主体ID] | [!DNL Dynamics]帐户的客户端ID。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| [!UICONTROL 服务主体密钥] | 服务主密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |

### 现有帐户

要连接现有帐户，请选择要连接的[!DNL Dynamics]帐户，然后选择右上角的&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/ms-dynamics/existing.png)

## 后续步骤

按照本教程，您已建立了与[!DNL Dynamics]帐户的连接。 您现在可以继续阅读下一个教程，并[配置数据流以将数据引入平台](../../dataflow/crm.md)。