---
title: 身份验证和访问Privacy ServiceAPI
description: 在文档中了解如何对Privacy ServiceAPI进行身份验证以及如何解释示例API调用。
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 2c8ac35e9bf72c91743714da1591c3414db5c5e9
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 1%

---

# 身份验证和访问Privacy ServiceAPI

本指南介绍了在尝试调用Adobe Experience Platform Privacy Service API之前必须了解的核心概念。

## 先决条件 {#prerequisites}

本指南要求您实际了解 [Privacy Service](../home.md) 以及它如何允许您跨Adobe Experience Cloud应用程序管理来自数据主体（客户）的访问和删除请求。

为了创建API的访问凭据，贵组织中的管理员之前必须已在Adobe Admin Console中设置用于Privacy Service的产品配置文件。 您分配给API集成的产品配置文件决定了集成在访问Privacy Service功能时具有的权限。 请参阅指南，网址为 [管理Privacy Service权限](../permissions.md) 了解更多信息。

## 收集所需标题的值 {#gather-values-required-headers}

要调用Privacy ServiceAPI，您必须首先收集要在所需标头中使用的访问凭据：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

使用以下方式生成这些值 [Adobe Developer控制台](https://developer.adobe.com/console). 您的 `{ORG_ID}` 和 `{API_KEY}` 只需生成一次，并可在以后的API调用中重复使用。 但是，您的 `{ACCESS_TOKEN}` 是临时的，必须每24小时重新生成一次。

下面详细介绍了生成这些值的步骤。

### 一次性设置 {#one-time-setup}

转到 [Adobe Developer控制台](https://developer.adobe.com/console) 然后使用您的Adobe ID登录。 接下来，按照教程中概述的以下步骤进行操作： [创建空项目](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在开发人员控制台文档中。

创建新项目后，选择 **[!UICONTROL 添加到项目]** 并选择 **[!UICONTROL API]** 下拉菜单中。

![正在从中选择的API选项 [!UICONTROL 添加到项目] 开发人员控制台中项目详细信息页面的下拉列表](../images/api/getting-started/add-api-button.png)

#### 选择Privacy ServiceAPI {#select-privacy-service-api}

此 **[!UICONTROL 添加API]** 屏幕。 选择 **[!UICONTROL Experience Cloud]** 要缩小可用API的列表，请选择卡以用于 **[!UICONTROL PRIVACY SERVICEAPI]** 选择之前 **[!UICONTROL 下一个]**.

![从可用API列表中选择的Privacy ServiceAPI卡](../images/api/getting-started/add-privacy-service-api.png)

>[!TIP]
>
>选择 **[!UICONTROL 查看文档]** 用于在单独的浏览器窗口中导航以完成操作的选项 [Privacy ServiceAPI参考文档](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

接下来，选择身份验证类型以生成访问令牌并访问Privacy ServiceAPI。

>[!IMPORTANT]
>
>选择 **[!UICONTROL OAuth服务器到服务器]** 方法，因为这将是向前移动时支持的唯一方法。 此 **[!UICONTROL 服务帐户(JWT)]** 方法已弃用。 虽然使用JWT身份验证方法的集成将继续工作到2025年1月1日，但Adobe强烈建议您在该日期之前将现有集成迁移到新的OAuth服务器到服务器方法。 在部分获取更多信息 [!BADGE 已弃用]{type=negative}[生成JSON Web令牌(JWT)](/help/landing/api-authentication.md#jwt).

![选择Oauth服务器到服务器的身份验证方法。](/help/privacy-service/images/api/getting-started/select-oauth-authentication.png)

#### 通过产品配置文件分配权限 {#product-profiles}

最终配置步骤是选择此集成将继承其权限的产品配置文件。 如果选择多个配置文件，则其权限集将针对集成进行合并。

>[!NOTE]
>
产品配置文件及其提供的粒度权限由管理员通过Adobe Admin Console创建和管理。 请参阅指南，网址为 [Privacy Service权限](../permissions.md) 了解更多信息。

完成后，选择 **[!UICONTROL 保存配置的API]**.

![在保存配置之前从列表中选择单个产品配置文件](../images/api/getting-started/select-product-profiles.png)

将API添加到项目后， **[!UICONTROL PRIVACY SERVICEAPI]** 项目页面显示所有Privacy ServiceAPI调用所需的以下凭据：

* `{API_KEY}` ([!UICONTROL 客户端ID])
* `{ORG_ID}` ([!UICONTROL 组织 ID])

![在开发人员控制台中添加API后的集成信息。](/help/privacy-service/images/api/getting-started/api-integration-information.png)

### 每个会话的身份验证 {#authentication-each-session}

您必须收集的最终必需凭据是 `{ACCESS_TOKEN}`，在Authorization标头中使用。 与的值不同 `{API_KEY}` 和 `{ORG_ID}`，必须每24小时生成一个新令牌才能继续使用API。

通常，有两种生成访问令牌的方法：

* [手动生成令牌](#manual-token) 用于测试和开发。
* [自动生成令牌](#auto-token) 用于API集成。

#### 手动生成令牌 {#manual-token}

要手动生成新的 `{ACCESS_TOKEN}`，导航到 **[!UICONTROL 凭据]** > **[!UICONTROL OAuth服务器到服务器]** 并选择 **[!UICONTROL 生成访问令牌]**，如下所示。

![如何在开发人员控制台UI中生成访问令牌的屏幕录制。](/help/privacy-service/images/api/getting-started/generate-access-token.gif)

将生成新的访问令牌，并提供用于将令牌复制到剪贴板的按钮。 此值用于必需的 [!DNL Authorization] 标头，并且必须以格式提供 `Bearer {ACCESS_TOKEN}`.

#### 自动生成令牌 {#auto-token}

您还可以使用Postman环境和集合来生成访问令牌。 有关更多信息，请阅读关于 [使用Postman验证和测试API调用](/help/landing/api-authentication.md#use-postman) 在Experience PlatformAPI身份验证指南中。

## 正在读取示例API调用 {#read-sample-api-calls}

每个端点指南都提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/api-guide.md#sample-api) 《平台API快速入门指南》中的。

## 后续步骤 {#next-steps}

现在，您已了解要使用哪些标头，可以开始调用Privacy ServiceAPI。 选择一个端点指南以开始：

* [隐私作业](./privacy-jobs.md)
* [同意](./consent.md)
