---
description: 本页举例说明了用于通过Adobe Experience Platform Destination SDK检索有关目标发布请求详细信息的API调用。
title: 检索目标发布请求
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 2%

---


# 检索目标发布请求

>[!IMPORTANT]
>
>只有在提交要由其他Experience Platform客户使用的生产（公共）目标时，才需要使用此API端点。 如果要创建供自己使用的专用目标，则无需使用发布API正式提交目标。

>[!IMPORTANT]
>
>**API端点**： `platform.adobe.io/data/core/activation/authoring/destinations/publish`

配置并测试目标后，可将其提交到Adobe进行审查和发布。 读取 [提交供审核在Destination SDK中创作的目标](../guides/submit-destination.md) 对于所有其他步骤，您必须在目标提交流程中执行。

在以下情况下，使用发布目标API端点提交发布请求：

* 作为Destination SDK合作伙伴，您希望使您的产品化目标在所有Experience Platform组织中都可供所有Experience Platform客户使用；
* 您制作 *任何更新* 到您的配置。 只有在提交新发布请求(经Experience Platform团队批准)后，配置更新才会反映在目标中。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值包括 **区分大小写**. 为避免区分大小写错误，请完全按照文档中所示使用参数名称和值。

## 目标发布API操作快速入门 {#get-started}

在继续之前，请查看 [快速入门指南](../getting-started.md) 要成功调用API需要了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 列出目标发布请求 {#retrieve-list}

GET您可以通过对 `/authoring/destinations/publish` 端点。

**API格式**

使用以下API格式检索您帐户的所有发布请求。

```http
GET /authoring/destinations/publish
```

使用以下API格式检索由定义的特定发布请求 `{DESTINATION_ID}` 参数。

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**请求**

以下两个请求检索您的IMS组织的所有发布请求或特定发布请求，具体取决于您是否传递 `DESTINATION_ID` 请求中的参数。

选择下面的每个选项卡以查看相应的有效负载。

>[!BEGINTABS]

>[!TAB 检索所有发布请求]

+++请求

以下请求将基于以下条件检索您提交的发布请求列表 [!DNL IMS Org ID] 和沙盒配置。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++响应

以下响应返回HTTP状态200，其中包含基于您使用的IMS组织ID和沙盒名称提交以进行发布且您有权访问的所有目标的列表。 一个 `configId` 对应于一个目标的发布请求。

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
| `destinationId` | 字符串 | 您已提交以进行发布的目标配置的目标ID。 |
| `publishDetailsList.configId` | 字符串 | 已提交目标的目标发布请求的唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字符串 | 返回目标可用的组织Experience Platform。 <br> <ul><li> 对象 `"destinationType": "PUBLIC"`，此参数会返回 `"*"`，这意味着目标对于所有Experience Platform组织都可用。</li><li> 对象 `"destinationType": "DEV"`，此参数会返回您用于创作和测试目标的组织的组织ID。</li></ul> |
| `publishDetailsList.status` | 字符串 | 目标发布请求的状态。 可能的值包括 `TEST`， `REVIEW`， `APPROVED`， `PUBLISHED`， `DENIED`， `REVOKED`， `DEPRECATED`. 具有值的目标 `PUBLISHED` 是实时的，可供Experience Platform客户使用。 |
| `publishDetailsList.destinationType` | 字符串 | 目标的类型。 值可以是 `DEV` 和 `PUBLIC`. `DEV` 对应于Experience Platform组织中的目标。 `PUBLIC` 对应于您已提交以进行发布的目标。 以Git术语来考虑这两个选项，其中 `DEV` version表示您的本地创作分支，并且 `PUBLIC` version表示远程主分支。 |
| `publishDetailsList.publishedDate` | 字符串 | 提交目标以进行发布的日期（以纪元时间计）。 |

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
| `{DESTINATION_ID}` | 要检索其发布状态的目标的ID。 |

+++

+++响应

如果您通过 `DESTINATION_ID` 在API调用中，响应返回HTTP状态200，其中包含有关指定目标发布请求的详细信息。

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
| `destinationId` | 字符串 | 您已提交以进行发布的目标配置的目标ID。 |
| `publishDetailsList.configId` | 字符串 | 已提交目标的目标发布请求的唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字符串 | 返回目标可用的组织Experience Platform。 <br> <ul><li> 对象 `"destinationType": "PUBLIC"`，此参数会返回 `"*"`，这意味着目标对于所有Experience Platform组织都可用。</li><li> 对象 `"destinationType": "DEV"`，此参数会返回您用于创作和测试目标的组织的组织ID。</li></ul> |
| `publishDetailsList.status` | 字符串 | 目标发布请求的状态。 可能的值包括 `TEST`， `REVIEW`， `APPROVED`， `PUBLISHED`， `DENIED`， `REVOKED`， `DEPRECATED`. 具有值的目标 `PUBLISHED` 是实时的，可供Experience Platform客户使用。 |
| `publishDetailsList.destinationType` | 字符串 | 目标的类型。 值可以是 `DEV` 和 `PUBLIC`. `DEV` 对应于Experience Platform组织中的目标。 `PUBLIC` 对应于您已提交以进行发布的目标。 以Git术语来考虑这两个选项，其中 `DEV` version表示您的本地创作分支，并且 `PUBLIC` version表示远程主分支。 |
| `publishDetailsList.publishedDate` | 字符串 | 提交目标以进行发布的日期（以纪元时间计）。 |

{style="table-layout:auto"}

+++

>[!ENDTABS]

## API错误处理

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中的。