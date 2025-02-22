---
title: 内容API端点
description: 了解如何使用Privacy ServiceAPI检索您的访问数据。
role: Developer
exl-id: b3b7ea0f-957d-4e51-bf92-121e9ae795f5
source-git-commit: ac54398ae8e9e06ea3581baf867ab1cf650042a2
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# 内容端点

使用`/content`端点安全地检索您客户的&#x200B;*访问信息*（隐私主体可以合法请求访问的信息）。 在响应`/jobs/{JOB_ID}`GET请求时提供的下载URL指向Adobe服务端点。 然后，您可以向`/jobs/:JOB_ID/content`发出GET请求，以JSON格式返回您的客户数据。 该接入方法实现了多层的认证和访问控制，增强了安全性。

在使用本指南之前，请参阅[快速入门指南](./getting-started.md)，了解有关以下示例API调用中提供的所需身份验证标头的信息。

>[!TIP]
>
>如果您当前不知道所需访问信息的作业ID，请调用`/jobs`端点并使用额外的查询参数筛选结果。 可在[隐私作业终结点指南](./privacy-jobs.md)中找到可用查询参数的完整列表。

## 检索隐私作业信息

要检索有关特定作业的信息（如其当前处理状态），请将该作业的`jobId`包含在`/jobs`终结点的GET请求路径中。

**API格式**

```http
GET /jobs/{JOB_ID}
```

**请求**

以下请求检索在请求路径中提供了`jobId`的作业的详细信息。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的响应将返回指定作业的详细信息。

>[!NOTE]
>
>隐私作业必须具有`complete`状态才能包含`downloadUrl`。

```json
{
    "jobId":"dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5",
    "requestId":"17129380910360540RX-753",
    "userKey":"1234",
    "action":"access",
    "status":"complete",
    "submittedBy":"jsnow@adobe.com",
    "createdDate":"04/12/2024 04:08 PM GMT",
    "lastModifiedDate":"04/12/2024 04:08 PM GMT",
    "userIds":[{
        "namespace":"ECID",
        "value":"1234",
        "type":"standard",
        "namespaceId":4,
        "isDeletedClientSide":false
        }],
    "productResponses":[{
        "product":"Identity",
        "retryCount":0,
        "processedDate":"04/12/2024 04:08 PM GMT",
        "productStatusResponse":{"status":"submitted"
        }}],
    "downloadUrl":"https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5/content",
    "regulation":"gdpr"
}
```

| 属性 | 描述 |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| `jobId` | 隐私作业的唯一标识符。 |
| `requestId` | 向Privacy Service发出的特定请求的唯一标识符。 |
| `userKey` | `userKey`是您在提交隐私请求时提供的`key`值。 `key`值是您为有意义的数据主体提供标识符的机会。 它通常是系统为跟踪数据主体而创建的唯一标识符。 提示：您可以列出所有活动的隐私作业，并将您的`key`与每个作业进行比较。 |
| `action` | 请求的操作的类型。 接受的值为`access`和`delete`。 |
| `status` | 隐私作业的当前状态。 |
| `submittedBy` | 提交隐私作业的人员的电子邮件地址。 |
| `createdDate` | 隐私作业的创建日期和时间。 |
| `lastModifiedDate` | 上次修改隐私作业的日期和时间。 |
| `userIds` | 包含用户标识符和相关信息的数组。 |
| `userIds.namespace` | 用于用户标识符的命名空间。 |
| `userIds.value` | 用户标识符的实际值。 |
| `userIds.type` | 标识符的类型（例如`standard`或`custom`）。 |
| `userIds.namespaceId` | 用于对用户身份进行分类和管理时使用的命名空间的标识符。 |
| `userIds.isDeletedClientSide` | 布尔值，指示标识符是否在客户端被删除。 |
| `productResponses` | 一个数组，其中包含来自与隐私作业相关的不同产品或服务的响应。 |
| `productResponses.product` | 用于获取有关数据主体的信息的产品或服务的名称。 |
| `productResponses.retryCount` | 重试请求的次数。 |
| `productResponses.processedDate` | 处理产品响应的日期和时间。 |
| `productResponses.productStatusResponse` | 包含产品响应状态的对象。 |
| `productResponses.productStatusResponse.status` | 产品响应的状态。 |
| `downloadURL` | 此属性提供了一个端点，可在作业完成后的60天内调用该端点。 作业的状态必须为`complete`，`action`必须为`access`。 否则，此字段不存在。 |
| `regulation` | 正在处理隐私请求的监管框架，如`gdpr`、`ccpa`、`lgpd_bra`、`pdpa_tha`等。 |

{style="table-layout:auto"}

## 检索客户访问信息 {#retrieve-access-data}

要获取响应数据主体的查询生成的“访问信息”，请向`/jobs/{JOB_ID}/content`端点发出GET请求。 响应是一个zip文件(*.zip)，它包含一个文件夹，其中包含每个产品的子文件夹，每个产品包含数据主体的数据。

>[!TIP]
>
>发出此请求需要特定的作业ID。 如果需要检索特定的作业ID，请首先向`/jobs`端点发出GET请求，并使用额外的查询参数来筛选结果。 可以在[隐私作业终结点指南](./privacy-jobs.md)中找到包括允许的查询参数的详细信息。

**API格式**

```http
GET /jobs/{JOB_ID}/content
```

**请求**

以下请求返回在请求中提供的作业ID的“访问信息”。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/32d429b1-f7f4-11ee-a365-574bcf5a525d/content \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'Accept: application/json`
```

**响应**

响应为zip文件(*.zip)。 虽然无法保证这一点，但通常以JSON格式返回信息。 提取的数据可以任何格式返回。

