---
description: 本页说明了用于通过Adobe Experience Platform Destination SDK检索有关目标发布请求的详细信息的API调用。
title: 检索目标发布请求
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 2%

---


# 检索目标发布请求

>[!IMPORTANT]
>
>仅当您提交的是要供其他Experience Platform客户使用的产品化（公共）目标时，才需要使用此API端点。 如果您创建供自己使用的专用目标，则无需使用发布API正式提交该目标。

>[!IMPORTANT]
>
>**API端点**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

配置并测试目标后，您可以将其提交到Adobe以进行审核和发布。 读取 [提交以供审核在Destination SDK中创作的目标](../guides/submit-destination.md) 在目标提交流程中，您必须执行所有其他步骤。

在以下情况下，使用发布目标API端点提交发布请求：

* 作为Destination SDK合作伙伴，您希望在所有Experience Platform组织中提供产品化目标，以供所有Experience Platform客户使用；
* 你做 *任何更新* 到您的配置。 只有在您提交新的发布请求(该请求已获得Experience Platform团队批准)后，配置更新才会反映在目标中。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均为 **区分大小写**. 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 目标发布API操作快速入门 {#get-started}

在继续之前，请查看 [入门指南](../getting-started.md) 有关成功调用API所需的重要信息，包括如何获取所需的目标创作权限和所需标头。

## 列出目标发布请求 {#retrieve-list}

您可以通过向 `/authoring/destinations/publish` 端点。

**API格式**

使用以下API格式检索您帐户的所有发布请求。

```http
GET /authoring/destinations/publish
```

使用以下API格式检索由 `{DESTINATION_ID}` 参数。

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**请求**

以下两个请求将检索您的IMS组织或特定发布请求的所有发布请求，具体取决于您是否传递 `DESTINATION_ID` 参数。

选择下面的每个选项卡，以查看相应的有效负荷。

>[!BEGINTABS]

>[!TAB 检索所有发布请求]

+++请求

以下请求将根据 [!DNL IMS Org ID] 和沙盒配置。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++响应

以下响应会根据您使用的IMS组织ID和沙盒名称，返回HTTP状态200，其中包含您有权访问的所有已提交发布目标的列表。 一个 `configId` 对应于一个目标的发布请求。

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"ab41387c0-4772-4709-a3ce-6d5fee654520",
         "allowedOrgs":[
            "716543205DB85F7F0A495E5B@AdobeOrg"
         ],
         "status":"TEST",
         "destinationType":"DEV"
      },
      {
         "configId":"cd568c67-f25e-47e4-b9a2-d79297a20b27",
         "allowedOrgs":[
            "*"
         ],
         "status":"DEPRECATED",
         "destinationType":"PUBLIC",
         "publishedDate":1630525501009
      },
      {
         "configId":"ef6f07154-09bc-4bee-8baf-828ea9c92fba",
         "allowedOrgs":[
            "*"
         ],
         "status":"PUBLISHED",
         "destinationType":"PUBLIC",
         "publishedDate":1630531586002
      }
   ]
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `destinationId` | 字符串 | 您为发布而提交的目标配置的目标ID。 |
| `publishDetailsList.configId` | 字符串 | 您提交的目标的目标发布请求的唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字符串 | 返回目标可用的Experience Platform组织。 <br> <ul><li> 对于 `"destinationType": "PUBLIC"`，此参数返回 `"*"`，这表示目标可用于所有Experience Platform组织。</li><li> 对于 `"destinationType": "DEV"`，此参数会返回用于创作和测试目标的组织的组织ID。</li></ul> |
| `publishDetailsList.status` | 字符串 | 目标发布请求的状态。 可能的值为 `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. 具有值的目标 `PUBLISHED` 是实时的，可供Experience Platform客户使用。 |
| `publishDetailsList.destinationType` | 字符串 | 目标的类型。 值可以是 `DEV` 和 `PUBLIC`. `DEV` 对应于您的Experience Platform组织中的目标。 `PUBLIC` 对应于您提交以进行发布的目标。 请用Git术语来考虑这两个选项，其中 `DEV` 版本表示您的本地创作分支，并且 `PUBLIC` 版本表示远程主分支。 |
| `publishDetailsList.publishedDate` | 字符串 | 提交目标以进行发布的日期（以纪元时间表示）。 |

{style="table-layout:auto"}

+++

>[!TAB 检索特定的发布请求]

+++请求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/{DESTINATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 要检索其发布状态的目标ID。 |

+++

+++响应

如果您通过 `DESTINATION_ID` 在API调用中，响应会返回HTTP状态200，其中包含有关指定目标发布请求的详细信息。

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"123cs780-ce29-434f-921e-4ed6ec2a6c35",
         "allowedOrgs": [
            "*"
         ],    
         "status":"PUBLISHED",
         "destinationType": "PUBLIC",
         "publishedDate":"1630617746"
      }
   ]
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `destinationId` | 字符串 | 您为发布而提交的目标配置的目标ID。 |
| `publishDetailsList.configId` | 字符串 | 您提交的目标的目标发布请求的唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字符串 | 返回目标可用的Experience Platform组织。 <br> <ul><li> 对于 `"destinationType": "PUBLIC"`，此参数返回 `"*"`，这表示目标可用于所有Experience Platform组织。</li><li> 对于 `"destinationType": "DEV"`，此参数会返回用于创作和测试目标的组织的组织ID。</li></ul> |
| `publishDetailsList.status` | 字符串 | 目标发布请求的状态。 可能的值为 `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. 具有值的目标 `PUBLISHED` 是实时的，可供Experience Platform客户使用。 |
| `publishDetailsList.destinationType` | 字符串 | 目标的类型。 值可以是 `DEV` 和 `PUBLIC`. `DEV` 对应于您的Experience Platform组织中的目标。 `PUBLIC` 对应于您提交以进行发布的目标。 请用Git术语来考虑这两个选项，其中 `DEV` 版本表示您的本地创作分支，并且 `PUBLIC` 版本表示远程主分支。 |
| `publishDetailsList.publishedDate` | 字符串 | 提交目标以进行发布的日期（以纪元时间表示）。 |

{style="table-layout:auto"}

+++

>[!ENDTABS]

## API错误处理

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。