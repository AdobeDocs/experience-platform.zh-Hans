---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；源SDK；SDK
solution: Experience Platform
title: 使用Platform UI创建MailChimp成员源连接
description: 了解如何使用Platform UI将Adobe Experience Platform连接到MailChimp成员。
exl-id: dc620ef9-624d-4fc9-8475-bb475ea86eb7
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# 创建 [!DNL Mailchimp Members] 使用Platform UI的源连接

本教程提供了用于创建 [!DNL Mailchimp] 要摄取的源连接器 [!DNL Mailchimp Members] 使用用户界面将数据发送到Adobe Experience Platform。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)：Platform允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)：Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

## 收集所需的凭据

为了将您的 [!DNL Mailchimp Members] 数据到Platform时，您必须首先提供与 [!DNL Mailchimp] 帐户。

此 [!DNL Mailchimp Members] 源支持OAuth 2刷新代码和基本身份验证。 有关这些身份验证类型的详细信息，请参阅下表。

### OAuth 2刷新代码

| 凭据 | 描述 |
| --- | --- |
| Domain | 用于连接到MailChimp API的根URL。 根URL的格式为 `https://{DC}.api.mailchimp.com`，其中 `{DC}` 表示与您的帐户对应的数据中心。 |
| 授权测试URL | 授权测试URL用于在连接时验证凭据 [!DNL Mailchimp] 到Platform。 如果未提供，则在源连接创建步骤期间将自动检查凭据。 |
| 访问令牌 | 用于对源进行身份验证的相应访问令牌。 基于OAuth的身份验证需要此项。 |

有关使用OAuth 2对您的进行身份验证的更多信息 [!DNL Mailchimp] Platform帐户，请参阅此 [[!DNL Mailchimp] 关于使用OAuth 2的文档](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

### 基本身份验证

| 凭据 | 描述 |
| --- | --- |
| Domain | 用于连接到MailChimp API的根URL。 根URL的格式为 `https://{DC}.api.mailchimp.com`，其中 `{DC}` 表示与您的帐户对应的数据中心。 |
| 用户名 | 与您的MailChimp帐户对应的用户名。 这是基本身份验证所必需的。 |
| 密码 | 与您的MailChimp帐户对应的密码。 这是基本身份验证所必需的。 |

## 连接您的 [!DNL Mailchimp Members] 平台帐户

在Platform UI中，选择 **[!UICONTROL 源]** 以访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 [!UICONTROL 营销自动化] 类别，选择 **[!UICONTROL Mailchimp营销活动]**，然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/mailchimp-members/catalog.png)

此 **[!UICONTROL 连接Mailchimp营销活动帐户]** 页面。 在此页面上，您可以选择是访问现有帐户，还是选择创建新帐户。

### 现有帐户

要使用现有帐户，请选择 [!DNL Mailchimp Members] 要用于创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/mailchimp-members/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为提供名称和描述 [!DNL Mailchimp Members] 源连接详细信息。

![新](../../../../images/tutorials/create/mailchimp-members/new.png)


#### 使用OAuth 2进行身份验证

要使用OAuth 2，请选择 [!UICONTROL OAuth 2刷新代码]，为您的域、授权测试URL和访问令牌提供值，然后选择 **[!UICONTROL 连接到源]**. 请稍等片刻，让您的凭据进行验证，然后选择 **[!UICONTROL 下一个]** 以继续。

![OAuth 身份验证](../../../../images/tutorials/create/mailchimp-members/oauth.png)

#### 使用基本身份验证进行身份验证

要使用基本身份验证，请选择 [!UICONTROL 基本身份验证]，提供域、用户名和密码的值，然后选择 **[!UICONTROL 连接到源]**. 请稍等片刻，让您的凭据进行验证，然后选择 **[!UICONTROL 下一个]** 以继续。

![基本](../../../../images/tutorials/create/mailchimp-members/basic.png)

### 选择 [!DNL Mailchimp Members] 数据

在您的源进行身份验证后，您必须提供 `listId` 与您的 [!DNL Mailchimp Members] 帐户。

在 [!UICONTROL 选择数据] 页面，输入您的 `listId` 然后选择 **[!UICONTROL 探索]**.

![探索](../../../../images/tutorials/create/mailchimp-members/explore.png)

该页面将更新为交互式架构树，允许您浏览和检查数据的层次结构。 选择 **[!UICONTROL 下一个]** 以继续。

![select-data](../../../../images/tutorials/create/mailchimp-members/select-data.png)

## 后续步骤

通过您的 [!DNL Mailchimp] 经过身份验证的帐户以及 [!DNL Mailchimp Members] 选择的数据，您现在可以开始创建数据流以将您的数据传送到Platform。 有关如何创建数据流的详细步骤，请参阅此文档： [创建数据流以将营销自动化数据引入平台](../../dataflow/marketing-automation.md).
