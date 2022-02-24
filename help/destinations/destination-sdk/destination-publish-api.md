---
description: 本页列出并介绍了您可以使用“/authoring/destinations/publish” API端点执行的所有API操作。
title: 发布目标API端点操作
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 6ad556e3b7bf15f1d6ff522307ff232b8fd947d3
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 4%

---

# 发布目标端点API操作 {#publish-destination}

>[!IMPORTANT]
>
>**API端点**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

本页列出并介绍了您可以使用 `/authoring/destinations/publish` API端点。

配置并测试目标后，您可以将其提交到Adobe以进行审核和发布。

在以下情况下，使用发布目标API端点提交发布请求：

* 作为Destination SDK合作伙伴，您希望在所有Experience Platform组织中提供产品化目标，以供所有Experience Platform客户使用；
* 您希望在您自己的Experience Platform组织中，在所有沙箱中提供自定义目标。

## 目标发布API操作快速入门 {#get-started}

在继续之前，请查看 [入门指南](./getting-started.md) 有关成功调用API所需的重要信息，包括如何获取所需的目标创作权限和所需标头。

## 提交要发布的目标配置 {#create}

您可以通过向发布POST请求，提交要发布的目标配置 `/authoring/destinations/publish` 端点。

**API格式**

```http
POST /authoring/destinations/publish
```

**请求**

以下请求会提交一个目标，以便在有效负载中提供的参数配置的组织之间进行发布。 以下负载包括接受的所有参数 `/authoring/destinations/publish` 端点。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "xyz@AdobeOrg",
      "lmn@AdobeOrg"
   ]
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `destinationId` | 字符串 | 您要提交以进行发布的目标配置的目标ID。 使用 [目标配置API引用](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | 字符串 | `ALL` 或 `LIMITED`. 指定您希望所有Experience Platform客户或仅为特定组织在目录中显示目标。 <br> **注意**:如果您使用 `LIMITED`，则仅会为您的Experience Platform组织发布目标。 如果出于Experience Platform测试的目的要将目标发布到Adobe组织的子集，请联系客户支持。 |
| `allowedOrgs` | 字符串 | 如果您使用 `"destinationAccess":"LIMITED"`，指定目标可用的Experience Platform组织。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功响应会返回HTTP状态201，其中包含目标发布请求的详细信息。

## 列出目标发布请求 {#retrieve-list}

您可以通过向 `/authoring/destinations/publish` 端点。

**API格式**

```http
GET /authoring/destinations/publish
```

**请求**

以下请求将根据IMS组织和沙盒配置，检索您有权访问的用于发布的已提交目标列表。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

以下响应会根据您使用的IMS组织ID和沙盒名称，返回HTTP状态200，其中包含已提交以供发布的目标列表，您有权访问这些目标。 一个 `configId` 对应于一个目标的发布请求。

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"1630617746"
      }
   ]
}
```

| 参数 | 类型 | 描述 |
|---------|----------|------|
| `destinationId` | 字符串 | 您为发布而提交的目标配置的目标ID。 |
| `publishDetailsList.configId` | 字符串 | 您提交的目标的目标发布请求的唯一ID。 |
| `publishDetailsList.allowedOrgs` | 字符串 | 返回目标应可用的Experience Platform组织。 |
| `publishDetailsList.status` | 字符串 | 目标发布请求的状态。 可能的值为 `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. |
| `publishDetailsList.publishedDate` | 字符串 | 提交目标以进行发布的日期（以纪元时间表示）。 |

{style=&quot;table-layout:auto&quot;}

## 更新现有目标发布请求 {#update}

您可以通过向发布请求的 `/authoring/destinations/publish` 端点和提供要更新所允许组织的目标ID。 在调用正文中，提供更新的允许组织。

**API格式**

```http
PUT /authoring/destinations/publish/{DESTINATION_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 要更新发布请求的目标ID。 |

**请求**

以下请求会更新现有的目标发布请求，该请求由有效负载中提供的参数进行配置。 在以下示例调用中，我们正在更新允许的组织。

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "abc@AdobeOrg",
      "def@AdobeOrg"
   ]
}
```

## 获取特定目标发布请求的状态 {#get}

您可以通过向 `/authoring/destinations/publish` 端点和提供要检索发布状态的目标ID。

**API格式**

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 要检索其发布状态的目标ID。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关指定目标发布请求的详细信息。

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"string"
      }
   ]
}
```

## API错误处理

Destination SDKAPI端点遵循常规Experience PlatformAPI错误消息原则。 请参阅 [API状态代码](../../landing/troubleshooting.md#api-status-codes) 和 [请求标头错误](../../landing/troubleshooting.md#request-header-errors) 平台疑难解答指南中。

## 后续步骤

阅读本文档后，您现在知道如何提交目标的发布请求。 Adobe Experience Platform团队将审核您的发布请求，并在5个工作日内回复给您。
