---
description: 本页是用于通过Adobe Experience Platform Destination SDK检索有关目标发布请求详细信息的API调用的示例。
title: 检索目标发布请求
exl-id: fceef12d-a52c-4259-a91e-7af88b132800
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 2%

---

# 检索目标发布请求

>[!IMPORTANT]
>
>只有在提交由其他Experience Platform客户使用的生产（公共）目标时，才需要使用此API端点。 如果您正在创建供自己使用的专用目标，则无需使用发布API正式提交目标。

>[!IMPORTANT]
>
>**API终结点**： `platform.adobe.io/data/core/activation/authoring/destinations/publish`

配置和测试目标后，可将其提交到Adobe进行审查和发布。 请阅读[在Destination SDK](../guides/submit-destination.md)中编写的目标提交以进行审核，了解作为目标提交流程的一部分而必须执行的所有其他步骤。

在以下情况下，使用发布目标API端点提交发布请求：

* 作为Destination SDK合作伙伴，您希望使您的产品化目标在所有Experience Platform组织中均可用，以供所有Experience Platform客户使用；
* 您对配置进行了&#x200B;*任何更新*。 只有在提交新的发布请求(经Experience Platform团队批准)后，配置更新才会反映在目标中。

>[!IMPORTANT]
>
>Destination SDK支持的所有参数名称和值均区分大小写&#x200B;****。 为避免出现区分大小写错误，请完全按照文档中的说明使用参数名称和值。

## 目标发布API操作快速入门 {#get-started}

在继续之前，请查看[入门指南](../getting-started.md)以了解成功调用API所需了解的重要信息，包括如何获取所需的目标创作权限和所需的标头。

## 列出目标发布请求 {#retrieve-list}

您可以通过向`/authoring/destinations/publish`端点发出GET请求，检索为发布IMS组织而提交的所有目标的列表。

**API格式**

使用以下API格式检索您帐户的所有发布请求。

```http
GET /authoring/destinations/publish
```

使用以下API格式检索由`{DESTINATION_ID}`参数定义的特定发布请求。

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**请求**

以下两个请求检索您的IMS组织的所有发布请求或特定发布请求，具体取决于您在请求中是否传递`DESTINATION_ID`参数。

选择下面的每个选项卡以查看相应的有效负载。

>[!BEGINTABS]

>[!TAB 检索所有发布请求]

+++请求

以下请求将根据[!DNL IMS Org ID]和沙盒配置检索您提交的发布请求列表。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++响应

以下响应返回HTTP状态200，其中包含基于您使用的IMS组织ID和沙盒名称提交以进行发布且您有权访问的所有目标的列表。 一个`configId`对应于一个目标的发布请求。

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
| `destinationId` | 字符串 | 已提交进行发布的目标配置的目标ID。 |
| `publishDetailsList.configId` | 字符串 | 已提交目标的目标发布请求的唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字符串 | 返回目标适用的Experience Platform组织。<br> <ul><li> 对于`"destinationType": "PUBLIC"`，此参数返回`"*"`，这意味着目标适用于所有Experience Platform组织。</li><li> 对于`"destinationType": "DEV"`，此参数返回您用于创作和测试目标的组织的组织ID。</li></ul> |
| `publishDetailsList.status` | 字符串 | 目标发布请求的状态。 可能的值为`TEST`、`REVIEW`、`APPROVED`、`PUBLISHED`、`DENIED`、`REVOKED`、`DEPRECATED`。 值为`PUBLISHED`的目标已上线，可供Experience Platform客户使用。 |
| `publishDetailsList.destinationType` | 字符串 | 目标的类型。 值可以是`DEV`和`PUBLIC`。 `DEV`对应于Experience Platform组织中的目标。 `PUBLIC`对应于您已提交发布的目标。 以Git术语来考虑这两个选项，其中`DEV`版本代表您的本地创作分支，`PUBLIC`版本代表远程主分支。 |
| `publishDetailsList.publishedDate` | 字符串 | 提交目标以供发布的日期（以纪元时间表示）。 |

{style="table-layout:auto"}

+++

>[!TAB 检索特定发布请求]

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

如果您在API调用中传递了`DESTINATION_ID`，响应将返回HTTP状态200，其中包含有关指定目标发布请求的详细信息。

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
| `destinationId` | 字符串 | 已提交进行发布的目标配置的目标ID。 |
| `publishDetailsList.configId` | 字符串 | 已提交目标的目标发布请求的唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字符串 | 返回目标适用的Experience Platform组织。<br> <ul><li> 对于`"destinationType": "PUBLIC"`，此参数返回`"*"`，这意味着目标适用于所有Experience Platform组织。</li><li> 对于`"destinationType": "DEV"`，此参数返回您用于创作和测试目标的组织的组织ID。</li></ul> |
| `publishDetailsList.status` | 字符串 | 目标发布请求的状态。 可能的值为`TEST`、`REVIEW`、`APPROVED`、`PUBLISHED`、`DENIED`、`REVOKED`、`DEPRECATED`。 值为`PUBLISHED`的目标已上线，可供Experience Platform客户使用。 |
| `publishDetailsList.destinationType` | 字符串 | 目标的类型。 值可以是`DEV`和`PUBLIC`。 `DEV`对应于Experience Platform组织中的目标。 `PUBLIC`对应于您已提交发布的目标。 以Git术语来考虑这两个选项，其中`DEV`版本代表您的本地创作分支，`PUBLIC`版本代表远程主分支。 |
| `publishDetailsList.publishedDate` | 字符串 | 提交目标以供发布的日期（以纪元时间表示）。 |

{style="table-layout:auto"}

+++

>[!ENDTABS]

## API错误处理

Destination SDK API端点遵循常规Experience Platform API错误消息原则。 请参阅Experience Platform疑难解答指南中的[API状态代码](../../../landing/troubleshooting.md#api-status-codes)和[请求标头错误](../../../landing/troubleshooting.md#request-header-errors)。
