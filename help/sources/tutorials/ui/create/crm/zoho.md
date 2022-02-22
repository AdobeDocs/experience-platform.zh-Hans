---
keywords: Experience Platform；主页；热门主题；Zoho CRM;Zoho CRM;Zoho;Zoho
solution: Experience Platform
title: 在UI中创建Zoho CRM源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Zoho CRM源连接。
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: 46b2fd6bc715bf1d8ccfeed576a2a2d193f92edd
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 创建 [!DNL Zoho CRM] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部源CRM数据的功能。 本教程提供了创建 [!DNL Zoho CRM] 源连接器使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有 [!DNL Zoho CRM] 帐户，您可以跳过本文档的其余部分，并继续阅读本教程 [配置数据流](../../dataflow/crm.md).

### 收集所需的凭据

为了连接 [!DNL Zoho CRM] 对于平台，必须为以下连接属性提供值：

| 凭据 | 描述 |
| --- | --- |
| 端点 | 的端点 [!DNL Zoho CRM] 服务器。 |
| 帐户URL | 帐户URL用于生成访问和刷新令牌。 URL必须特定于域。 |
| 客户端ID | 与 [!DNL Zoho CRM] 用户帐户。 |
| 客户端密钥 | 与 [!DNL Zoho CRM] 用户帐户。 |
| 访问令牌 | 访问令牌可授权您对 [!DNL Zoho CRM] 帐户。 |
| 刷新令牌 | 刷新令牌是用于在您的访问令牌过期后生成新访问令牌的令牌。 |

有关这些凭据的更多信息，请参阅 [[!DNL Zoho CRM] 身份验证](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## 连接 [!DNL Zoho CRM] 帐户

收集所需的凭据后，您可以按照以下步骤链接 [!DNL Zoho CRM] 帐户 [!DNL Platform].

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 [!UICONTROL CRM] 类别，选择 **[!UICONTROL Zoho CRM]**，然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/zoho/catalog.png)

的 **[!UICONTROL 连接Zoho CRM帐户]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL Zoho CRM] 创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/zoho/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后提供名称、可选描述以及 [!DNL Zoho CRM] 凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后，再留出一些时间建立新连接。

>[!TIP]
>
>您的帐户URL域必须与您相应的域位置相对应。 以下是各种域及其相应的帐户URL:<ul><li>美国：https://accounts.zoho.com</li><li>澳大利亚：https://accounts.zoho.com.au</li><li>欧洲：https://accounts.zoho.eu</li><li>印度：https://accounts.zoho.in</li><li>中国：https://accounts.zoho.com.cn</li></ul>

![新建](../../../../images/tutorials/create/zoho/new.png)

## 后续步骤

通过阅读本教程，您已经与 [!DNL Zoho CRM] 帐户。 您现在可以继续下一个教程和 [配置数据流以将数据导入平台](../../dataflow/crm.md).
