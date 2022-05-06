---
description: 本页介绍如何验证和开始使用Adobe Experience Platform Destination SDK。 其中包含有关如何获取Adobe I/O身份验证凭据、沙盒名称和目标创作访问控制权限的说明。
title: Destination SDK入门
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 2%

---

# 快速入门

## 概述 {#overview}

本页介绍如何验证和开始使用Adobe Experience Platform Destination SDK。 其中包含有关如何获取Adobe I/O身份验证凭据、沙盒名称和目标创作访问控制权限的说明。

## 术语 {#terminology}

本指南使用特定于平台的概念，如IMS组织和沙箱。 请查阅 [Experience Platform术语表](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html) 的定义。

## 获取所需的身份验证凭据 {#obtain-authentication-credentials}

Destination SDK使用 [Adobe I/O](https://www.adobe.io/) 用于身份验证的网关。 要对Destination SDK端点进行API调用，您必须在API调用中提供特定标头。 与AdobeExchange团队合作，为您设置 [Adobe开发人员控制台](https://developer.adobe.com/console).

要成功调用Destination SDKAPI端点，请遵循 [Experience Platform身份验证教程](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html). 从“[生成API密钥、IMS组织ID和客户端密钥](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)“ ”步骤。 Adobe交换团队将为您处理前面的步骤。 完成身份验证教程将提供Destination SDKAPI调用中每个所需标头的值，如下所示：

* `x-api-key: {API_KEY}`，也称为客户端ID
* `x-gw-ims-org-id: {ORG_ID}`，也称为组织ID
* `Authorization: Bearer {ACCESS_TOKEN}`的问题。访问令牌的过期时间为24小时（以毫秒为单位），因此您必须刷新它。 要刷新访问令牌，请重复身份验证教程中概述的步骤。

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {ORG_ID}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## 目标所有权和沙箱 {#destination-ownership}

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 Destination SDK请求需要指定操作在中进行的沙盒名称的标头：

* `x-sandbox-name: {SANDBOX_NAME}`

AdobeExchange团队为您提供沙盒名称，您需要在Destination SDKAPI端点的调用中使用该名称。

## 基于角色的访问控制(RBAC) {#rbac}

使用中描述的Destination SDKAPI端点 [参考文档](./configuration-options.md)，您需要 **[!UICONTROL 目标创作]** 访问控制权限。 与AdobeExchange团队合作，在 [Adobe Admin Console](https://adminconsole.adobe.com/).

![目标创作权限](./assets/destination-authoring-permission.png)

有关更多信息，请阅读以下Experience Platform访问控制文档：

* [管理产品配置文件的权限](/help/access-control/ui/permissions.md)
* [可用的Experience Platform权限](/help/access-control/home.md#permissions)
* [Adobe Admin Console文档](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)

## 其他注意事项 {#additional-considerations}

* 您对目标配置所做的任何更改（无论您是创建还是编辑目标配置）都需要由Adobe审核和批准。 只有在审核完成后，您所做的更改才会反映在您的目标中。
* 只有属于同一组织且有权访问沙盒的用户才能编辑目标配置。

## 后续步骤 {#next-steps}

按照本文中的步骤，您将获得Adobe I/O的身份验证凭据、沙盒名称和目标创作访问控制权限。 接下来，您可以使用Destination SDK设置目标。

* 根据您的目标类型，阅读以下配置指南：

   * [使用Destination SDK配置流目标](./configure-destination-instructions.md)
   * [（测试版）使用Destination SDK配置基于文件的目标](./configure-file-based-destination-instructions.md)

* 有关所有操作，请参阅 [目标创作API文档](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
* 使用 [目标创作API Postman集合](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json) 使用Destination SDKAPI端点配置目标。 要开始使用Postman，请参阅 [导入环境和收藏集的步骤](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) 和 [创建Postman环境的视频指南](https://video.tv.adobe.com/v/28832).
