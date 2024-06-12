---
title: 文件夹端点
description: 了解如何使用Adobe Experience Platform API创建、更新、管理和删除文件夹。
role: Developer
source-git-commit: 8f9a2b5a2063b76518302eb9de38b628c87416e1
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 4%

---


# 文件夹端点

>[!IMPORTANT]
>
>这组端点的端点URL为 `https://experience.adobe.io`.

文件夹是一项功能，可让您更好地组织业务对象以便于导航和分类。

本指南提供的信息可帮助您更好地了解文件夹，并且包括用于使用API执行基本操作的示例API调用。

## 快速入门

在继续之前，请查看 [快速入门指南](./getting-started.md) 有关成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

## 检索文件夹列表 {#list}

您可以向以下网站发出GET请求，以检索属于您组织的文件夹列表： `/folder` 端点并指定文件夹类型和父文件夹ID。

**API格式**

```http
GET /folder/{FOLDER_TYPE}/{PARENT_FOLDER_ID}/subfolders
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 文件夹中包含的对象类型。 支持的值包括 `segment` 和 `dataset`. |
| `{PARENT_FOLDER_ID}` | 从中检索文件夹列表的父文件夹的ID。 要查看所有父文件夹的列表，请使用文件夹ID `root`. |

**请求**

+++列出所有顶级数据集文件夹的示例请求

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/root/subfolders
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应会返回HTTP状态200，其中包含组织中数据集的所有顶级文件夹的列表。

+++一个示例响应，其中包含贵组织中数据集的所有顶级文件夹的列表。

```json
{
    "id": "c626b4f7-223b-4486-8900-00c266e31dd1",
    "name": "ParentFolder",
    "noun": "Dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": null,
    "createdAt": "2023-01-12T03:31:00.118+00:00",
    "modifiedBy": null,
    "modifiedAt": "2023-01-13T05:47:06.718+00:00",
    "_links": null,
    "children": [
        {
            "id": "09d86b23-4819-471b-8a2a-05774ed268de",
            "name": "ChildFolder.1",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-12T12:51:39.284+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-12T12:51:39.284+00:00",
            "_links": null,
            "children": []
        },
        {
            "id": "fd2f6a68-ef65-470d-ab31-b02b7b2241ca",
            "name": "ChildFolder.2",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-13T03:38:40.006+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-13T03:38:40.006+00:00",
            "_links": null,
            "children": []
        }
    ]
}
```

+++

## 创建新文件夹 {#create}

您可以通过向以下网站发出POST请求来创建新文件夹： `/folder` 端点并指定文件夹类型。

**API格式**

```http
POST /folder/{FOLDER_TYPE}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 文件夹中包含的对象类型。 支持的值包括 `segment` 和 `dataset`. |

**请求**

+++创建新文件夹的示例请求。

```shell
curl -X POST https://experience.adobe.io/unifiedfolders/folder/dataset
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "name": "SampleFolder",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5"
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 要创建的文件夹的名称。 |
| `parentId` | 父文件夹的ID。 |

+++

**响应**

成功的响应返回HTTP状态200以及新创建文件夹的详细信息。

+++包含新创建文件夹详细信息的示例响应。

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": null
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 新创建的文件夹的ID。 |
| `createdBy` | 创建文件夹的用户的ID。 |
| `createdAt` | 文件夹创建时间的时间戳。 |
| `modifiedBy` | 上次修改文件夹的用户的标识。 |
| `modifiedAt` | 上次更新文件夹的时间戳。 |

+++

## 检索特定文件夹 {#get}

您可以通过向以下网站发出GET请求，检索属于您组织的特定文件夹： `/folder` 端点并指定文件夹类型和文件夹的ID。

**API格式**

```http
GET /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 文件夹中包含的对象类型。 支持的值包括 `segment` 和 `dataset`. |
| `{FOLDER_ID}` | 正在检索的文件夹的ID。 |

**请求**

+++检索特定文件夹的示例请求

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200，其中包含所请求文件夹的详细信息。

+++包含所请求文件夹详细信息的示例响应。

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 请求的文件夹的ID。 |
| `name` | 请求的文件夹的名称。 |
| `parentId` | 父文件夹的ID。 |
| `createdBy` | 创建文件夹的用户的ID。 |
| `createdAt` | 文件夹创建时间的时间戳。 |
| `modifiedBy` | 上次更新文件夹的用户的ID。 |
| `modifiedAt` | 上次更新文件夹的时间戳。 |
| `status` | 请求的文件夹的状态。 支持的值包括 `IN_USE` 和 `ARCHIVED`. |

+++

## 验证指定的文件夹 {#validate}

您可以通过对文件夹发出GET请求，验证文件夹是否有资格在其中包含对象。 `/folder/{FOLDER_TYPE}/{FOLDER_ID}/validate` 端点，并提供文件夹类型和ID。

**API格式**

```http
GET /folder/{FOLDER_TYPE}/{FOLDER_ID}/validate
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 文件夹中包含的对象类型。 支持的值包括 `segment` 和 `dataset`. |
| `{FOLDER_ID}` | 正在验证的文件夹的ID。 |

**请求**

+++用于验证特定文件夹的示例请求

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功状态会返回HTTP状态200以及正在验证的文件夹的详细信息。

+++示例响应包含已验证文件夹的详细信息

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

+++

## 更新特定文件夹 {#update}

您可以通过向以下网站发出PATCH请求，更新属于您组织的特定文件夹的详细信息： `/folder` 端点并指定文件夹类型和文件夹的ID。

**API格式**

```http
PATCH /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 文件夹中包含的对象类型。 支持的值包括 `segment` 和 `dataset`. |
| `{FOLDER_ID}` | 要更新的文件夹的ID。 |

**请求**

+++更新特定文件夹的示例请求

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '[{
    "op": "replace",
    "path": "/name",
    "value": "RenamedSampleFolder"
 }]'
```

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关新更新的文件夹的信息。

```json
{
    "id": "eafab5bf-3457-4b7f-b366-3c5399bd98f1",
    "name": "RenamedSampleFolder",
    "noun": "dataset",
    "parentFolderId": null,
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "183807A65A0F5D180A494004@AdobeID",
    "createdAt": "2024-03-05T01:42:36.910+00:00",
    "modifiedBy": "183807A65A0F5D180A494004@AdobeID",
    "modifiedAt": "2024-03-05T01:45:54.740+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/eafab5bf-3457-4b7f-b366-3c5399bd98f1"
        }
    },
    "namespace": null
}
```

## 删除特定文件夹 {#delete}

您可以通过对以下对象发出DELETE请求，删除属于您组织的特定文件夹： `/folder` 并指定文件夹类型和文件夹的ID。

***API格式**

```http
DELETE /folder/{FOLDER_TYPE}/{FOLDER_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FOLDER_TYPE}` | 文件夹中包含的对象类型。 支持的值包括 `segment` 和 `dataset`. |
| `{FOLDER_ID}` | 要删除的文件夹的ID。 |

**请求**

+++删除特定文件夹的示例请求

```shell
curl -X DELETE https://experience.adobe.io/unifiedfolders/folder/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200，并显示消息正文，通知您文件夹已被删除。

```json
{
    "message": "delete request accepted successfully"
}
```

## 后续步骤

阅读本指南后，您现在可以更好地了解如何使用Adobe Experience Platform API创建、管理和删除文件夹。
