---
keywords: Experience Platform；主页；热门主题；Microsoft Dynamics；microsoft dynamics；Dynamics；Dynamics
solution: Experience Platform
title: 在UI中创建Microsoft Dynamics Source连接
type: Tutorial
description: 了解如何使用Microsoft Dynamics UI创建Adobe Experience Platform源连接。
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 1%

---

# 在用户界面中创建[!DNL Microsoft Dynamics]源连接

本教程提供了使用Adobe Experience Platform UI创建[!DNL Microsoft Dynamics]（以下称为“[!DNL Dynamics]”）源连接的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL Dynamics]帐户，则可以跳过本文档的其余部分，并转到有关[为CRM源配置数据流](../../dataflow/crm.md)的教程。

### 收集所需的凭据

为了验证您的[!DNL Dynamics]源，您必须提供以下连接属性的值：

>[!BEGINTABS]

>[!TAB 基本身份验证]

| 凭据 | 描述 |
| --- | --- |
| `serviceUri` | [!DNL Dynamics]实例的服务URL。 |
| `username` | [!DNL Dynamics]用户帐户的用户名。 |
| `password` | [!DNL Dynamics]帐户的密码。 |

>[!TAB 服务主体和密钥身份验证]

| 凭据 | 描述 |
| --- | --- |
| `servicePrincipalId` | [!DNL Dynamics]帐户的客户端ID。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `servicePrincipalKey` | 服务主体密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |

>[!ENDTABS]

有关入门的详细信息，请参阅[此 [!DNL Dynamics] 文档](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

## 连接您的[!DNL Dynamics]帐户

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL 目录]屏幕显示您可以用来创建帐户的各种来源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在[!UICONTROL CRM]类别下，选择&#x200B;**[!UICONTROL Microsoft Dynamics]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![已选择Microsoft Dynamics的源目录。](../../../../images/tutorials/create/ms-dynamics/catalog.png)

此时会显示&#x200B;**[!UICONTROL Connect Microsoft Dynamics帐户]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

若要使用现有帐户，请选择要使用的[!DNL Dynamics]帐户，然后选择右上角的&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有帐户接口。](../../../../images/tutorials/create/ms-dynamics/existing.png)

### 新帐户

>[!TIP]
>
>创建后，无法更改[!DNL Dynamics]基本连接的身份验证类型。 要更改身份验证类型，必须创建新的基本连接。

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后为您的新[!DNL Dynamics]帐户提供名称和可选描述。

![新帐户创建界面。](../../../../images/tutorials/create/ms-dynamics/new.png)

创建[!DNL Dynamics]帐户时，您可以使用基本身份验证或服务主体和密钥身份验证。

>[!BEGINTABS]

>[!TAB 基本身份验证]

若要创建具有基本身份验证的[!DNL Dynamics]帐户，请选择[!UICONTROL 基本身份验证]，然后为您的[!UICONTROL 服务URI]、[!UICONTROL 用户名]和[!UICONTROL 密码]提供值。 **注意**： [!DNL Dynamics]中的基本身份验证可能被Experience Platform当前不支持的双重身份验证阻止。 在这种情况下，建议使用基于密钥的身份验证来创建使用[!DNL Dynamics]的源连接器。

完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新帐户。

![基本身份验证接口。](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB 服务主体和密钥身份验证]

若要创建具有服务主体和密钥身份验证的[!DNL Dynamics]帐户，请选择&#x200B;**[!UICONTROL 服务主体和密钥身份验证]**，然后提供您的[!UICONTROL 服务主体ID]和[!UICONTROL 服务主体密钥]的值。

完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新帐户。

![服务主体密钥身份验证接口。](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与[!DNL Dynamics]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入Experience Platform](../../dataflow/crm.md)。
