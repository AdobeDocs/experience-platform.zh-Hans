---
title: 创建受众API端点
description: 了解如何使用API为外部受众创建元数据。
hide: true
hidefromtoc: true
exl-id: e841a5f6-f406-4e1d-9e8a-acb861ba6587
source-git-commit: bf90b09693c7b9b7d3ad6ccc6940d255bf7bf4cb
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 6%

---

# 创建受众端点

POST `/audiences`端点可用于为外部受众创建元数据，从而让受众在受众门户中可见。 如果受众摄取在单独的服务中进行管理（如批量摄取），则您应使用此端点。

## 快速入门

>[!IMPORTANT]
>
>本指南中的端点使用`/core/ais`作为前缀，而不是`/core/ups`。

要使用Experience Platform API，您必须已完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将为Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关在[!DNL Experience Platform]中使用沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

**API格式**

>[!IMPORTANT]
>
>您&#x200B;**必须**&#x200B;在请求中包含`createAudienceMetaOnly=true`查询参数。

```http
POST /audiences?createAudienceMetaOnly=true
```

**请求**

>[!IMPORTANT]
>
>您&#x200B;**必须**&#x200B;将`Accept: application/vnd.adobe.external.audiences+json; version=2`标头包含在API请求中。

```shell
curl -X POST https://platform.adobe.io/core/ais/audiences?createAudienceMetaOnly=true \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'\
 -H 'Accept: application/vnd.adobe.external.audiences+json; version=2'
 -d '{
    "name": "Sample audience name",
    "description" "A sample description for the audience.",
    "namespace": "agora",
    "originName": "Agora_Collaboration"
 }'
```

| 属性 | 类型 | 描述 |
| -------- | ---- | ----------- |
| `name` | 字符串 | 受众的名称。 |
| `description` | 字符串 | 受众的可选描述。 |
| `namespace` | 字符串 | 受众的命名空间。 |
| `originName` | 字符串 | 受众来源的名称。 |

**响应**

成功的响应返回HTTP状态200，其中包含有关新创建的受众的信息。

```json
{
    "name": "Sample audience name",
    "audienceId": "4a815904-f2f9-4237-82fb-55605bcc2ad7"
}
```

| 属性 | 类型 | 描述 |
| -------- | ---- | ----------- |
| `name` | 字符串 | 您创建的受众的名称。 |
| `audienceId` | 字符串 | 您创建的受众的ID。 |
