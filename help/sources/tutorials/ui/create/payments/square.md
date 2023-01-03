---
keywords: Experience Platform；主页；热门主题；正方形；正方形
title: 在UI中创建正方形源连接
description: 了解如何使用Adobe Experience Platform UI创建正方形源连接。
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# 创建 [!DNL Square] UI中的源连接

本教程提供了创建 [!DNL Square] 源连接器。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

### 收集所需的凭据

为了访问 [!DNL Square] 帐户平台中，您必须提供以下值：

| 凭据 | 描述 |
| --- | --- |
| Host | 的URL [!DNL Square] 实例。 |
| 客户端ID | 与 [!DNL Square] 帐户。 |
| 客户端密钥 | 与 [!DNL Square] 帐户。 |
| 访问令牌 | 访问令牌用于验证您的 [!DNL Square] 具有OAuth 2.0身份验证的帐户。 访问令牌可从 [!DNL Square]. |
| 刷新令牌 | 当您的当前访问令牌过期时，刷新令牌将用于生成新的访问令牌。 可从获取刷新令牌 [!DNL Square]. |

有关这些凭据以及如何获取这些凭据的更多信息，请参阅 [[!DNL Square] oauth文档](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

收集所需的凭据后，您可以按照以下步骤链接 [!DNL Square] 帐户到平台。

## 连接 [!DNL Square] 帐户

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 [!UICONTROL 支付] 类别，选择 **[!UICONTROL 平方]**，然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/square/catalog.png)

的 **[!UICONTROL 连接到正方形]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL Square] 创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/square/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为您提供名称、可选描述和相应的值 [!DNL Square] 凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后，再留出一些时间建立新连接。

![新建](../../../../images/tutorials/create/square/new.png)

## 后续步骤

通过本教程，您已通过身份验证，并在 [!DNL Square] 帐户和平台。 您现在可以继续下一个教程和 [创建数据流以将支付数据引入平台](../../dataflow/payments.md).
