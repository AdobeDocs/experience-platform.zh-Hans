---
title: 验证并访问 Privacy Service API
description: 在文档中了解如何对Privacy Service API进行身份验证以及如何解释示例API调用。
role: Developer
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 5%

---

# 验证并访问 Privacy Service API

本指南介绍了在尝试调用Adobe Experience Platform Privacy Service API之前必须了解的核心概念。

## 先决条件 {#prerequisites}

本指南需要您对[Privacy Service](../home.md)以及它如何允许您跨Adobe Experience Cloud应用程序管理来自数据主体（客户）的访问和删除请求有一定的了解。

要创建API的访问凭据，贵组织中的管理员之前必须在Adobe Admin Console中为Privacy Service设置产品配置文件。 您分配给API集成的产品配置文件决定了集成在访问Privacy Service功能时具有的权限。 有关详细信息，请参阅[管理Privacy Service权限](../permissions.md)指南。

## 收集所需标头的值 {#gather-values-required-headers}

要调用Privacy Service API，您必须首先收集要在所需标头中使用的访问凭据：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

这些值是使用[Adobe Developer Console](https://developer.adobe.com/console)生成的。 您的`{ORG_ID}`和`{API_KEY}`只需生成一次，可在以后的API调用中重复使用。 但是，您的`{ACCESS_TOKEN}`是临时的，必须每24小时重新生成一次。

下面详细介绍了生成这些值的步骤。

### 一次性设置 {#one-time-setup}

转到[Adobe Developer Console](https://developer.adobe.com/console)并使用您的Adobe ID登录。 接下来，按照Developer Console文档中有关[创建空项目](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/)的教程中概述的步骤进行操作。

创建新项目后，选择&#x200B;**[!UICONTROL 添加到项目]**，然后从下拉菜单中选择&#x200B;**[!UICONTROL API]**。

![从Developer Console中项目详细信息页面的[!UICONTROL 添加到项目]下拉列表中选择API选项](../images/api/getting-started/add-api-button.png)

#### 选择Privacy Service API {#select-privacy-service-api}

出现&#x200B;**[!UICONTROL 添加API]**&#x200B;屏幕。 选择&#x200B;**[!UICONTROL Experience Cloud]**&#x200B;以缩小可用API的列表，然后选择&#x200B;**[!UICONTROL Privacy Service API]**&#x200B;的卡，然后再选择&#x200B;**[!UICONTROL 下一步]**。

![从可用API列表中选择的Privacy Service API卡](../images/api/getting-started/add-privacy-service-api.png)

>[!TIP]
>
>选择&#x200B;**[!UICONTROL 查看文档]**&#x200B;选项可在单独的浏览器窗口中导航到完整的[Privacy Service API参考文档](https://developer.adobe.com/experience-platform-apis/references/privacy-service/)。

接下来，选择身份验证类型以生成访问令牌并访问Privacy Service API。

>[!IMPORTANT]
>
>选择&#x200B;**[!UICONTROL OAuth服务器到服务器]**&#x200B;方法，因为这将是今后唯一支持的方法。 已弃用&#x200B;**[!UICONTROL 服务帐户(JWT)]**&#x200B;方法。 虽然使用JWT身份验证方法的集成将继续工作到2025年1月1日，但Adobe强烈建议您在该日期之前将现有集成迁移到新的OAuth服务器到服务器方法。 在[!BADGE Deprecated]部分获取更多信息{type=negative}[生成JSON Web令牌(JWT)](/help/landing/api-authentication.md#jwt)。

![选择Oauth服务器到服务器身份验证方法。](/help/privacy-service/images/api/getting-started/select-oauth-authentication.png)

#### 通过产品配置文件分配权限 {#product-profiles}

最终配置步骤是选择此集成将继承其权限的产品配置文件。 如果选择多个配置文件，则其权限集将针对集成进行组合。

>[!NOTE]
>
产品配置文件及其提供的粒度权限由管理员通过Adobe Admin Console创建和管理。 有关详细信息，请参阅[Privacy Service权限](../permissions.md)指南。

完成后，选择&#x200B;**[!UICONTROL 保存配置的API]**。

![在保存配置之前，将从列表中选择单个产品配置文件](../images/api/getting-started/select-product-profiles.png)

将API添加到项目后，项目的&#x200B;**[!UICONTROL Privacy Service API]**&#x200B;页面将显示所有调用Privacy Service API所需的以下凭据：

* `{API_KEY}` （[!UICONTROL 客户端ID]）
* `{ORG_ID}` （[!UICONTROL 组织ID]）

在Developer Console中添加API后的![集成信息。](/help/privacy-service/images/api/getting-started/api-integration-information.png)

### 每个会话的身份验证 {#authentication-each-session}

必须收集的最终必需凭据是授权标头中使用的`{ACCESS_TOKEN}`。 与`{API_KEY}`和`{ORG_ID}`的值不同，必须每24小时生成一个新令牌才能继续使用API。

通常，有两种生成访问令牌的方法：

* [手动生成令牌](#manual-token)以进行测试和开发。
* [自动生成API集成的令牌](#auto-token)。

#### 手动生成令牌 {#manual-token}

要手动生成新`{ACCESS_TOKEN}`，请导航到&#x200B;**[!UICONTROL 凭据]** > **[!UICONTROL OAuth服务器到服务器]**，然后选择&#x200B;**[!UICONTROL 生成访问令牌]**，如下所示。

![如何在Developer Console UI中生成访问令牌的屏幕录制。](/help/privacy-service/images/api/getting-started/generate-access-token.gif)

将生成新的访问令牌，并会提供一个按钮以将令牌复制到剪贴板。 此值用于所需的[!DNL Authorization]标头，必须以`Bearer {ACCESS_TOKEN}`格式提供。

#### 自动生成令牌 {#auto-token}

您还可以使用Postman环境和收藏集来生成访问令牌。 有关详细信息，请阅读Experience Platform API身份验证指南中有关[使用Postman进行身份验证和测试API调用](/help/landing/api-authentication.md#use-postman)的部分。

## 正在读取示例 API 调用 {#read-sample-api-calls}

每个端点指南都提供了示例API调用，以演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅Experience Platform API快速入门指南中有关[如何读取示例API调用](../../landing/api-guide.md#sample-api)的部分。

## 后续步骤 {#next-steps}

现在，您已了解要使用哪些标头，可以开始调用Privacy Service API了。 选择其中一个端点指南以开始：

* [隐私任务](./privacy-jobs.md)
* [同意](./consent.md)
