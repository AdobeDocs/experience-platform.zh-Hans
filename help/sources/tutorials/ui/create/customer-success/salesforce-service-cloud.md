---
keywords: Experience Platform；主页；热门主题；Salesforce服务云；Salesforce服务云
solution: Experience Platform
title: 在UI中创建Salesforce服务云源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Salesforce服务云源连接。
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---

# 创建 [!DNL Salesforce Service Cloud] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了创建 [!DNL Salesforce Service Cloud] （以下简称SSC）源连接器，使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有有效的SSC连接，则可以跳过本文档的其余部分，继续阅读上的教程 [配置数据流](../../dataflow/customer-success.md)

### 收集所需的凭据

要在 [!DNL Platform]，则必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `username` | 用户帐户的用户名。 |
| `password` | 用户帐户的密码。 |
| `securityToken` | 用户帐户的安全令牌。 |

有关入门的更多信息，请参阅 [此 [!DNL Salesforce Service Cloud] 文档](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## 连接 [!DNL Salesforce Service Cloud] 帐户

收集所需凭据后，您可以按照以下步骤将SSC帐户关联到 [!DNL Platform].

登录到 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问 **[!UICONTROL 源]** 工作区。 的 **[!UICONTROL 目录]** 屏幕会显示您可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 **[!UICONTROL 客户成功]** 类别，选择 **[!UICONTROL Salesforce服务云]**. 如果这是您首次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，请选择 **[!UICONTROL 添加数据]** 创建新的SSC连接器。

![目录](../../../../images/tutorials/create/ssc/catalog.png)

的 **[!UICONTROL 连接到Salesforce Service Cloud]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述和您的SSC凭据。 完成后，选择 **[!UICONTROL 连接]** 然后，再留出一些时间建立新连接。

![connect](../../../../images/tutorials/create/ssc/connect.png)

### 现有帐户

要连接现有帐户，请选择要连接的SSC帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/ssc/existing.png)

## 后续步骤

通过阅读本教程，您已建立与SSC帐户的连接。 您现在可以继续下一个教程和 [配置数据流以将客户成功数据引入 [!DNL Platform]](../../dataflow/customer-success.md).
