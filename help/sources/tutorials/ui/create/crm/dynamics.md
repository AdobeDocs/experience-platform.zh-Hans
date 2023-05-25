---
keywords: Experience Platform；主页；热门主题；Microsoft Dynamics；Microsoft Dynamics；Dynamics；Dynamics
solution: Experience Platform
title: 在UI中创建Microsoft Dynamics源连接
type: Tutorial
description: 了解如何使用Microsoft UI创建Adobe Experience Platform Dynamics源连接。
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# 创建 [!DNL Microsoft Dynamics] UI中的源连接

本教程提供了用于创建 [!DNL Microsoft Dynamics] (以下简称“ ”[!DNL Dynamics]“)源连接(使用Adobe Experience Platform UI)。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Dynamics] 帐户，您可以跳过本文档的其余部分并继续阅读关于的教程 [为CRM源配置数据流](../../dataflow/crm.md).

### 收集所需的凭据

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUri` | 您的服务URL [!DNL Dynamics] 实例。 |
| `username` | 的用户名 [!DNL Dynamics] 用户帐户。 |
| `password` | 您的密码 [!DNL Dynamics] 帐户。 |
| `servicePrincipalId` | 您的客户端ID [!DNL Dynamics] 帐户。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `servicePrincipalKey` | 服务主体密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |

有关入门的更多信息，请参阅 [此 [!DNL Dynamics] 文档](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## 连接您的 [!DNL Dynamics] 帐户

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL Dynamics] Platform帐户。

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 以访问 [!UICONTROL 源] 工作区。 此 **[!UICONTROL 目录]** 屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 **[!UICONTROL CRM]** 类别，选择 **[!UICONTROL Microsoft Dynamics]**. 如果这是您第一次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，选择 **[!UICONTROL 添加数据]** 以新建 [!DNL Dynamics] 连接器。

![目录](../../../../images/tutorials/create/ms-dynamics/catalog.png)

此 **[!UICONTROL 连接到Dynamics]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入表单上，为新输入提供名称和可选描述 [!DNL Dynamics] 帐户。

此 [!DNL Dynamics] connector为您提供不同的身份验证类型以进行访问。 下 [!UICONTROL 帐户身份验证] 选择 **[!UICONTROL 基本身份验证]** 使用基于密码的凭据。

完成后，选择 **[!UICONTROL 连接到源]** 然后留出一些时间来建立新帐户。

![基本身份验证](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

或者，您可以选择 **[!UICONTROL 服务主体和密钥身份验证]** 并连接 [!DNL Dynamics] 帐户使用以下项的组合： [!UICONTROL 服务主体ID] 和 [!UICONTROL 服务主体密钥].

>[!IMPORTANT]
>
> 中的基本身份验证 [!DNL Dynamics] 可能被双重身份验证阻止，Platform当前不支持双重身份验证。 在这种情况下，建议使用基于密钥的身份验证创建源连接器，使用 [!DNL Dynamics].

![基于密钥的身份验证](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| 凭据 | 描述 |
| ---------- | ----------- |
| [!UICONTROL 服务主体ID] | 您的客户端ID [!DNL Dynamics] 帐户。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| [!UICONTROL 服务主体密钥] | 服务主体密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |

### 现有帐户

要连接现有帐户，请选择 [!DNL Dynamics] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/ms-dynamics/existing.png)

## 后续步骤

按照本教程，您已建立与的连接 [!DNL Dynamics] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据引入平台](../../dataflow/crm.md).
