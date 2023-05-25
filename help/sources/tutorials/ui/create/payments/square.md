---
keywords: Experience Platform；主页；热门主题；方形；方形
title: 在UI中创建正方形源连接
description: 了解如何使用Adobe Experience Platform UI创建正方形源连接。
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# 创建 [!DNL Square] UI中的源连接

本教程提供了用于创建 [!DNL Square] 源连接器，使用平台用户界面。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

### 收集所需的凭据

要访问您的 [!DNL Square] 帐户平台，您必须提供以下值：

| 凭据 | 描述 |
| --- | --- |
| Host | 的URL [!DNL Square] 实例。 |
| 客户端ID | 与您的关联的客户端ID [!DNL Square] 帐户。 |
| 客户端密码 | 与您的关联的客户端密钥 [!DNL Square] 帐户。 |
| 访问令牌 | 访问令牌用于验证您的 [!DNL Square] 具有OAuth 2.0身份验证的帐户。 访问令牌可从获取 [!DNL Square]. |
| 刷新令牌 | 刷新令牌用于在当前访问令牌过期后生成新的访问令牌。 可以从获取刷新令牌 [!DNL Square]. |

有关这些凭据以及如何获取这些凭据的更多信息，请参阅 [[!DNL Square] oauth上的文档](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL Square] Platform帐户。

## 连接您的 [!DNL Square] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 [!UICONTROL 支付] 类别，选择 **[!UICONTROL 方形]**，然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/square/catalog.png)

此 **[!UICONTROL 连接到方形]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL Square] 要用于创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/square/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为提供名称、可选描述和相应的值 [!DNL Square] 凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后留出一些时间来建立新连接。

![新](../../../../images/tutorials/create/square/new.png)

## 后续步骤

按照本教程，您已验证并创建了源连接，该连接位于 [!DNL Square] 帐户和平台。 您现在可以继续下一教程和 [创建数据流以将支付数据引入Platform](../../dataflow/payments.md).
