---
keywords: Experience Platform；主页；热门主题；Zoho CRM；zoho crm；Zoho；Zoho
solution: Experience Platform
title: 在UI中创建Zoho CRM Source连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Zoho CRM源连接。
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 2%

---

# 在用户界面中创建[!DNL Zoho CRM]源连接

>[!WARNING]
>
>[!DNL Zoho CRM]源将于2025年6月底弃用。

Adobe Experience Platform中的Source连接器可按计划摄取外部源CRM数据。 本教程提供了使用[!DNL Experience Platform]用户界面创建[!DNL Zoho CRM]源连接器的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL Zoho CRM]帐户，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/crm.md)的教程。

### 收集所需的凭据

为了将[!DNL Zoho CRM]连接到Experience Platform，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| --- | --- |
| 终结点 | 您向其发出请求的[!DNL Zoho CRM]服务器的端点。 |
| 帐户URL | 帐户URL用于生成访问和刷新令牌。 URL必须特定于域。 |
| 客户端 ID | 与您的[!DNL Zoho CRM]用户帐户对应的客户端ID。 |
| 客户端密码 | 与您的[!DNL Zoho CRM]用户帐户对应的客户端密钥。 |
| 访问令牌 | 访问令牌授权您对您的[!DNL Zoho CRM]帐户的安全临时访问。 |
| 刷新令牌 | 刷新令牌是在您的访问令牌过期后用于生成新的访问令牌的令牌。 |

有关这些凭据的详细信息，请参阅有关[[!DNL Zoho CRM] 身份验证](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html)的文档。

## 连接您的[!DNL Zoho CRM]帐户

收集所需的凭据后，您可以按照以下步骤将您的[!DNL Zoho CRM]帐户关联到[!DNL Experience Platform]。

在Experience Platform UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在[!UICONTROL CRM]类别下，选择&#x200B;**[!UICONTROL Zoho CRM]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![目录](../../../../images/tutorials/create/zoho/catalog.png)

出现&#x200B;**[!UICONTROL Connect Zoho CRM帐户]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

要使用现有帐户，请选择要用于创建新数据流的[!DNL Zoho CRM]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/zoho/existing.png)

### 新帐户

如果您正在创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后提供名称、可选描述和您的[!DNL Zoho CRM]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

>[!TIP]
>
>您的帐户URL域必须与适当的域位置相对应。 以下是各个域及其相应的帐户URL：<ul><li>美国： https://accounts.zoho.com</li><li>澳大利亚：https://accounts.zoho.com.au</li><li>欧洲：https://accounts.zoho.eu</li><li>印度：https://accounts.zoho.in</li><li>中国： https://accounts.zoho.com.cn</li></ul>

![新](../../../../images/tutorials/create/zoho/new.png)

## 后续步骤

通过学习本教程，您已建立与[!DNL Zoho CRM]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入Experience Platform](../../dataflow/crm.md)。
