---
description: 本页介绍如何验证和开始使用Adobe Experience Platform Destination SDK。 其中包括有关如何获取Adobe I/O身份验证凭据、沙盒名称和目标创作访问控制权限的说明。
title: Destination SDK快速入门
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---

# 快速入门

## 概述 {#overview}

本页介绍如何验证和开始使用Adobe Experience Platform Destination SDK。 其中包括有关如何获取Adobe I/O身份验证凭据、沙盒名称和目标创作访问控制权限的说明。

## 术语 {#terminology}

本指南使用特定于Experience Platform的概念，例如组织和沙盒。 有关这些术语的定义，请参阅[Experience Platform术语表](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html)。 请参阅[Destination SDK术语表](/help/destinations/destination-sdk/glossary.md)以了解与此功能直接相关的术语。

## 获取所需的身份验证凭据 {#obtain-authentication-credentials}

Destination SDK使用[Adobe I/O](https://www.adobe.io/)网关进行身份验证。 要对Destination SDK端点进行API调用，必须在API调用中提供某些标头。 与Adobe Exchange团队合作，为您设置对[Adobe Developer Console](https://developer.adobe.com/console)的身份验证。

要成功调用Destination SDK API端点，请按照[Experience Platform身份验证教程](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=zh-Hans)操作。 从“[生成API密钥、组织ID和客户端密钥](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)”步骤启动教程。 Adobe Exchange团队将为您处理上述步骤。 完成身份验证教程将为Destination SDK API调用中的每个所需标头提供值，如下所示：

* `x-api-key: {API_KEY}`，也称为客户端ID
* `x-gw-ims-org-id: {ORG_ID}`，也称为组织ID
* `Authorization: Bearer {ACCESS_TOKEN}`的问题。访问令牌的过期时间为24小时（以毫秒为单位），因此您必须刷新它。 要刷新访问令牌，请重复身份验证教程中所述的步骤。

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

## 目标所有权和沙盒 {#destination-ownership}

Experience Platform中的所有资源都被隔离到特定的虚拟沙盒中。 对Destination SDK的请求需要标头，这些标头应指定执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

Adobe Exchange团队为您提供沙盒名称，您需要将其用于对Destination SDK API端点的调用。

## 基于角色的访问控制(RBAC) {#rbac}

要使用[参考文档](functionality/configuration-options.md)中描述的Destination SDK API端点，您需要&#x200B;**[!UICONTROL 目标创作]**&#x200B;访问控制权限。 与Adobe Exchange团队合作，在[Adobe Admin Console](https://adminconsole.adobe.com/)中为您分配此权限。

![目标创作权限](./assets/destination-authoring-permission.png)

有关更多信息，请阅读以下Experience Platform访问控制文档：

* [管理产品配置文件的权限](/help/access-control/ui/permissions.md)
* [Experience Platform的可用权限](/help/access-control/home.md#permissions)
* [Adobe Admin Console文档](https://helpx.adobe.com/enterprise/using/admin-console.html)

## 其他注意事项 {#additional-considerations}

* 对于产品化/公共目标，您对目标配置所做的任何更改，无论您是创建或编辑目标配置，都需要Adobe审核和批准。 只有在完成审阅后，您的更改才会反映在您的目标中。 这不适用于仅供您使用的专用目标。
* 只有属于同一组织且具有沙盒访问权限的用户才能编辑目标配置。

## 后续步骤 {#next-steps}

按照本文中的步骤，您获取了Adobe I/O的身份验证凭据、沙盒名称和目标创作访问控制权限。 接下来，您可以使用Destination SDK设置目标。

* 根据您的目标类型，阅读以下配置指南：

   * [使用Destination SDK配置流目标](guides/configure-destination-instructions.md)
   * [使用Destination SDK配置基于文件的目标](guides/configure-file-based-destination-instructions.md)

* 有关所有操作，请参阅[目标创作API文档](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)。
* 使用[目标创作API Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json)通过Destination SDK API端点配置您的目标。 要开始使用Postman，请参阅导入环境和收藏集的[步骤](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/)以及创建Postman环境的[视频指南](https://video.tv.adobe.com/v/28832)。
