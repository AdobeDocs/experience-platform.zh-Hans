---
keywords: Experience Platform；主页；热门主题；Microsoft Dynamics；Microsoft Dynamics；Dynamics；Dynamics
solution: Experience Platform
title: 在UI中创建Microsoft Dynamics源连接
type: Tutorial
description: 了解如何使用Microsoft UI创建Adobe Experience Platform Dynamics源连接。
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# 创建 [!DNL Microsoft Dynamics] UI中的源连接

本教程提供了创建 [!DNL Microsoft Dynamics] (以下简称“[!DNL Dynamics]“)使用Adobe Experience Platform UI建立源连接。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Dynamics] 帐户，您可以跳过本文档的其余部分，并继续阅读上的教程 [为CRM源配置数据流](../../dataflow/crm.md).

### 收集所需的凭据

为了验证您的 [!DNL Dynamics] 源，必须提供以下连接属性的值：

>[!BEGINTABS]

>[!TAB 基本身份验证]

| 凭据 | 描述 |
| --- | --- |
| `serviceUri` | 您的服务URL [!DNL Dynamics] 实例。 |
| `username` | 的用户名 [!DNL Dynamics] 用户帐户。 |
| `password` | 您的密码 [!DNL Dynamics] 帐户。 |

>[!TAB 服务主体和密钥身份验证]

| 凭据 | 描述 |
| --- | --- |
| `servicePrincipalId` | 您的客户端ID [!DNL Dynamics] 帐户。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `servicePrincipalKey` | 服务主体密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |

>[!ENDTABS]

有关入门的更多信息，请参阅 [此 [!DNL Dynamics] 文档](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## 连接您的 [!DNL Dynamics] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示了您可以用来创建帐户的各种来源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 [!UICONTROL CRM] 类别，选择 **[!UICONTROL Microsoft Dynamics]**，然后选择 **[!UICONTROL 添加数据]**.

![选择了Microsoft Dynamics的源目录。](../../../../images/tutorials/create/ms-dynamics/catalog.png)

此 **[!UICONTROL 连接Microsoft Dynamics帐户]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL Dynamics] 要使用的帐户，然后选择 **[!UICONTROL 下一个]** 继续操作。

![现有帐户界面。](../../../../images/tutorials/create/ms-dynamics/existing.png)

### 新帐户

>[!TIP]
>
>创建后，便无法更改的身份验证类型 [!DNL Dynamics] 基本连接。 要更改身份验证类型，必须创建新的基本连接。

要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为新页面提供名称和可选描述 [!DNL Dynamics] 帐户。

![新的帐户创建界面。](../../../../images/tutorials/create/ms-dynamics/new.png)

创建时，可以使用基本身份验证或服务主体和密钥身份验证 [!DNL Dynamics] 帐户。

>[!BEGINTABS]

>[!TAB 基本身份验证]

创建 [!DNL Dynamics] 具有基本身份验证的帐户，选择 [!UICONTROL 基本身份验证] 然后为提供值 [!UICONTROL 服务URI]， [!UICONTROL 用户名]、和 [!UICONTROL 密码]. **注意**：中的基本身份验证 [!DNL Dynamics] 可能被双重身份验证阻止，目前Platform不支持双重身份验证。 在这种情况下，建议使用基于密钥的身份验证来创建源连接器，使用 [!DNL Dynamics].

完成后，选择 **[!UICONTROL 连接到源]** 然后留出一些时间来建立新帐户。

![基本身份验证界面。](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB 服务主体和密钥身份验证]

创建 [!DNL Dynamics] 具有服务主体和密钥身份验证的帐户，选择 **[!UICONTROL 服务主体和密钥身份验证]** 然后为提供值 [!UICONTROL 服务主体Id] 和 [!UICONTROL 服务主体密钥].

完成后，选择 **[!UICONTROL 连接到源]** 然后留出一些时间来建立新帐户。

![服务主体密钥身份验证接口。](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与的连接 [!DNL Dynamics] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据引入Platform](../../dataflow/crm.md).
