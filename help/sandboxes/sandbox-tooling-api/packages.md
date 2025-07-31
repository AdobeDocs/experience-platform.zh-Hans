---
title: 沙盒工具包API端点
description: 沙盒工具API中的/packages端点允许您以编程方式管理Adobe Experience Platform中的包。
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: 1d8c29178927c7ee3aceb0b68f97baeaefd9f695
workflow-type: tm+mt
source-wordcount: '2933'
ht-degree: 8%

---

# 包端点

沙盒工具允许您选择不同的工件（也称为对象）并将它们导出到包中。 资源包可以包含单个对象或多个对象（如数据集或架构）。 包中包含的任何工件都必须来自同一沙盒。

沙盒工具API中的`/packages`端点允许您以编程方式管理组织中的包，包括发布包并将包导入沙盒。

## 创建资源包 {#create}

您可以创建多工件包，方法是在为包名称和包类型提供值的同时，向`/packages`端点发出POST请求。

**API格式**

```http
POST /packages/
```

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "name": "acme",
      "description": "Acme Business Group",
      "packageType": "PARTIAL",    
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      },
      "expiry": "2023-05-20T20:05:10Z",
      "artifacts": [
        {
          "id": "27115daa-c92b-4f17-a077-d65ffeb0c525",
          "type": "PROFILE_SEGMENT",
          "title": "Acme Profile Segment"
        }      
      ]
  }'
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `name` | 程序包的名称。 | 字符串 | 是 |
| `description` | 用于提供有关包的更多信息的描述。 | 字符串 | 否 |
| `packageType` | 包类型为&#x200B;**PARTIAL**，表示您在包中包含特定项目。 | 字符串 | 是 |
| `sourceSandbox` | 包的源沙盒。 | 对象 | 否 |
| `expiry` | 定义包到期日期的时间戳。 默认值为自创建日期起90天。 响应到期字段将为纪元UTC时间。 | 字符串（UTC时间戳格式） | 否 |
| `artifacts` | 要导出到资源包中的项目列表。 当`artifacts`为&#x200B;**时，**&#x200B;值应为&#x200B;**null**&#x200B;或`packageType`empty`FULL`。 | 数组 | 否 |

**响应**

成功的响应将返回您新创建的包。 响应包括相应的程序包ID，以及有关其状态、到期和工件列表的信息。

```json
{
    "id": "209f886b00444eac9bb5836fe32e7681",
    "version": 0,
    "createdDate": 1684475012105,
    "modifiedDate": 1684475012105,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "requestId": "devxa54a6b56d04f46119d9e3cc006fcc1cb",
    "userId": "platform_exim",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "cjm-mr",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1684613110000,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## 更新包 {#update}

使用沙盒工具API中的`/packages`端点更新包。

### 将工件添加到资源包 {#add-artifacts}

要将项目添加到包，您必须提供`id`并包括&#x200B;**的** ADD`action`。

**API格式**

```http
PUT /packages/
```

**请求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "ADD",
      "expiry": "2023-05-20T20:05:10Z", 
      "artifacts": [
        {
         "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
         "type": "JOURNEY"
        }      
      ]
  }'
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `id` | 要更新的程序包的ID。 | 字符串 | 是 |
| `action` | 要将项目添加到包中，操作值应为&#x200B;**ADD**。 仅&#x200B;**PARTIAL**&#x200B;包类型支持此操作。 | 字符串 | 是 |
| `artifacts` | 要添加到包中的项目列表。 如果列表为&#x200B;**null**&#x200B;或&#x200B;**empty**，则不会更改包。 在将工件添加到资源包之前，会先对其进行重复数据删除。 请参阅下表，以查看支持的项目的完整列表。 | 数组 | 否 |
| `expiry` | 定义包到期日期的时间戳。 如果在有效负载中未指定过期，则默认值为从调用PUT API起90天。 响应到期字段将为纪元UTC时间。 | 字符串（UTC时间戳格式） | 否 |

当前支持以下工件类型。

| 工件 | 平台 | 对象 | 部分流量 | 完整沙盒 |
| --- | --- | --- | --- | --- |
| `JOURNEY` | Adobe Journey Optimizer | 历程 | 是 | 否 |
| `ID_NAMESPACE` | 客户数据平台 | 身份标识 | 是 | 是 |
| `REGISTRY_DATATYPE` | 客户数据平台 | 数据类型 | 是 | 是 |
| `REGISTRY_CLASS` | 客户数据平台 | 类 | 是 | 是 |
| `REGISTRY_MIXIN` | 客户数据平台 | 字段组 | 是 | 是 |
| `REGISTRY_SCHEMA` | 客户数据平台 | 架构 | 是 | 是 |
| `CATALOG_DATASET` | 客户数据平台 | 数据集 | 是 | 是 |
| `DULE_CONSENT_POLICY` | 客户数据平台 | 同意和治理政策 | 是 | 是 |
| `PROFILE_SEGMENT` | 客户数据平台 | 受众 | 是 | 是 |
| `FLOW` | 客户数据平台 | 源数据流 | 是 | 是 |

**响应**

成功的响应将返回您更新的包。 响应包括相应的程序包ID，以及有关其状态、到期和工件列表的信息。

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 4,
    "createdDate": 1684235842000,
    "modifiedDate": 1684475861366,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1692251861352,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### 从资源包中删除工件 {#delete-artifacts}

若要从包中删除项目，必须提供`id`并包含&#x200B;**的** DELETE`action`。

**API格式**

```http
PUT /packages/
```

**请求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "DELETE",
      "artifacts": [
        {
          "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
          "type": "JOURNEY"
        }      
      ]
  }'
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `id` | 要更新的程序包的ID。 | 字符串 | 是 |
| `action` | 若要从包中删除项目，操作值应为&#x200B;**DELETE**。 仅&#x200B;**PARTIAL**&#x200B;包类型支持此操作。 | 字符串 | 是 |
| `artifacts` | 将从资源包中删除的项目的列表。 如果列表为&#x200B;**null**&#x200B;或&#x200B;**empty**，则不会更改包。 | 数组 | 否 |

**响应**

成功的响应将返回您更新的包。 响应包括相应的程序包ID，以及有关其状态、到期和工件列表的信息。

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 5,
    "createdDate": 1684235842000,
    "modifiedDate": 1684478830416,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },      
    "packageType": "PARTIAL",
    "expiry": 1692254830403,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### 更新包中的元数据字段 {#update-metadata}

>[!NOTE]
>
>**UPDATE**&#x200B;操作用于更新包的包元数据字段，而&#x200B;**不能用于向包添加/删除项目。**

要更新包中的元数据字段，必须为`id`提供&#x200B;**并包括** UPDATE`action`。

**API格式**

```http
PUT /packages/
```

**请求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "UPDATE",
      "name": "acme",
      "description": "Acme Business Group",  
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      }
  }'
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `id` | 要更新的程序包的ID。 | 字符串 | 是 |
| `action` | 要更新包中的元数据字段，操作值应为&#x200B;**UPDATE**。 仅&#x200B;**PARTIAL**&#x200B;包类型支持此操作。 | 字符串 | 是 |
| `name` | 包的更新名称。 不允许重复包名称。 | 数组 | 是 |
| `sourceSandbox` | Source沙盒应属于在请求标头中指定的相同组织。 | 对象 | 是 |

**响应**

成功的响应将返回您更新的包。 响应包括相应的程序包ID，以及有关其描述、状态、到期和工件列表的信息。

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 6,
    "createdDate": 1684235842000,
    "modifiedDate": 1684479094129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",    
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "packageType": "PARTIAL",
    "expiry": 1692255094127,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## 删除资源包 {#delete}

要删除包，请向`/packages`端点发出DELETE请求，并指定要删除的包的ID。

**API格式**

```http
DELETE /packages/{PACKAGE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{PACKAGE_ID}` | 要删除的程序包的ID。 |

**请求**

以下请求删除ID为{PACKAGE_ID}的包。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回一个原因，其中显示已删除的包ID。

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## 发布包 {#publish}

为了能够将包导入沙盒，您必须发布它。 在指定要发布的包的ID时，向`/packages`端点发出GET请求。

**API格式**

```http
GET /packages/{PACKAGE_ID}/export
```

| 参数 | 描述 |
| --- | --- |
| `{PACKAGE_ID}` | 要发布的包的ID。 |

**请求**

以下请求发布了ID为{PACKAGE_ID}的包。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `expiryPeriod` | 此用户指定的时间段定义从包发布之时起的包到期日期（以天为单位）。 该值不应为负。<br>如果未指定值，则默认值将从发布日期算起90（天）。 | 整数 | 否 |

**响应**

成功的响应将返回已发布的包。

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
}
```

## 查找包 {#look-up-package}

您可以通过向`/packages`端点发出GET请求来查找单个包，该端点在请求路径中包含包的相应ID。

**API格式**

```http
GET /packages/{PACKAGE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{PACKAGE_ID}` | 要查找的程序包的ID。 |

**请求**

以下请求检索{PACKAGE_ID}的信息。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回查询的包ID的详细信息。 响应包括包的名称、描述、发布日期和到期日期、源沙盒以及工件列表。

```json
{
    "id": "8f585fad94d042cd82dbcba594108a41",
    "version": 2,
    "createdDate": 1685597784000,
    "modifiedDate": 1685597810000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
    "packageType": "PARTIAL",
    "expiry": 1693373810000,
    "publishDate": 1685597810000,
    "status": "PUBLISHED",
    "artifactsList": [
        {
            "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ],
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    }
}
```

## 列出包 {#list-packages}

您可以通过向`/packages`端点发出GET请求来列出组织中的所有包。

**API格式**

```http
GET /packages/?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMS}` | 用于筛选结果的可选查询参数。 有关详细信息，请参阅[查询参数](./appendix.md)上的部分。 |

**请求**

以下请求根据{QUERY_PARAMS}检索包的信息。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/?property=status==DRAFT,PUBLISHED&property=createdDate>=2023-05-11T18:29:59.999Z&property=createdDate<=2023-05-16T18:29:59.999Z&start=0&orderby=-createdDate&limit=20 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应将返回属于您组织的包列表，包括名称、状态、到期和工件列表等详细信息。

```json
{
    "totalElements": 109,
    "currentPage": 0,
    "totalPages": 6,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "8f585fad94d042cd82dbcba594108a41",
            "version": 2,
            "createdDate": 1685597784000,
            "modifiedDate": 1685597810000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "c875b077162b40409c1327b16da99c1b",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693373810000,
            "publishDate": 1685597810000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                },
                {
                    "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        },
        {
            "id": "0d7e427ce4cb4dc1b78e30ef61b125c1",
            "version": 2,
            "createdDate": 1685555213000,
            "modifiedDate": 1685555275000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "7d7d8bbe3c7c4a8ea701cc5e42c57aeb",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693331275000,
            "publishDate": 1685555275000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "626a9669a9f5b818db270e95",
                    "type": "CATALOG_DATASET",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        }
    ]
}
```

## 导入资源包 {#import}

此端点用于获取指定目标沙盒中的冲突对象。 冲突对象表示目标沙盒中已存在的类似对象。

**API格式**

```http
GET /packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName
```

| 参数 | 描述 |
| --- | --- |
| `{PACKAGE_ID}` | 要查找的程序包的ID。 |

**请求**

以下请求导入{PACKAGE_ID}。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

响应中返回冲突。 响应将原始包加上`alternatives`片段显示为按排名排序的数组。

+++查看响应

```json
[
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/176f33f6a8ff6542de1256f8dc01cce4be1b3a68fd5f5bc5",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686403052050"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/1b37c3403e4e12c7aa46ea9dfe380a9f2b72d4da9db62b46",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686218766627"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_SCHEMA::https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
    },
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
            "type": "REGISTRY_CLASS",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/1dd81d61cdaa89a89382d0a424db77494475bd1db3105feb",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686564843736"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/classes/2511fb5396a630b2cd3d5d9e9b69d42ce66a4289db8ac917",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686408152916"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_CLASS::https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
    },
    {
        "artifact": {
            "id": "4d4c874ec3344d64bf8b3160e60ac78b",
            "type": "MAPPING_SET",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: 4d4c874ec3344d64bf8b3160e60ac78b"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "6b49c959d77c48e9904f7616fe2e7848",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "7b363da9e6704afb9716f57193d5246f",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "93ca0b4f437c4eaf9f1986408679e965",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::MAPPING_SET::4d4c874ec3344d64bf8b3160e60ac78b"
    }
]
```

+++

## 提交导入 {#submit-import}

>[!NOTE]
>
>在解决冲突时，目标沙盒中已存在替代工件，这是固有的。

查看冲突并通过向`/packages`端点发出POST请求提供替换后，您可以提交包的导入。 结果作为有效负载提供，有效负载将启动在有效负载中指定的目标沙盒的导入作业。

有效负载还接受用户指定的导入作业的作业名称和描述。 如果用户指定的名称和说明不可用，则包名称和说明将用于作业名称和说明。

**API格式**

```http
POST /packages/import
```

**请求**

以下请求会检索要导入的包。 有效负载是一个替代映射，如果存在条目，则键是包提供的`artifactId`，而替代项是值。 如果映射或有效负载为&#x200B;**empty**，则不会执行替换。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/import/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
       "id": "09484a599f5f4a5faa43986643964615",
       "name": "acme",
       "description": "Acme Business Group",
       "destinationSandbox": {
         "name": "cjm-mr",
         "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
     },
     "alternatives": {
       "https://ns.adobe.com/cjmstage/schemas/ac33bbd22eb4ad6656e1c7e12e9f520261fb39fd28a902a9": {
         "id": "https://ns.adobe.com/cjmstage/schemas/a3b935344685afad4e52c753161cf673ec23d4fb1b3e9ce",
         "type": "REGISTRY_SCHEMA"
       }
     }
  }'
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `alternatives` | `alternatives`表示源沙盒项目到现有目标沙盒项目的映射。 由于它们已经存在，导入作业会避免在Target沙盒中创建这些工件。 | 字符串 | 否 |

**响应**

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "destinationSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
}
```

## 列出所有依赖对象 {#dependent-objects}

通过在指定包的ID时向`/packages`端点发出POST请求，列出包中导出对象的所有依赖对象。

**API格式**

```http
POST /packages/{PACKAGE_ID}/children
```

| 参数 | 描述 |
| --- | --- |
| `{PACKAGE_ID}` | 程序包的ID。 |

**请求**

以下请求列出了{PACKAGE_ID}的所有依赖对象。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/children \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'[
      {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "type": "REGISTRY_SCHEMA"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "type": "REGISTRY_CLASS"
      }
  ]'
```

**响应**

成功的响应将返回对象的子项列表。

```json
[
    {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "title": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
                "type": "REGISTRY_SCHEMA"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
        "type": "REGISTRY_SCHEMA",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
                "type": "REGISTRY_CLASS"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
        "type": "REGISTRY_CLASS",
        "children": []
    }
]
```

## 检查基于角色的权限以导入所有包对象 {#role-based-permissions}

您可以检查您是否有权导入包工件，方法是在指定包的ID和目标沙盒名称时，通过向`/packages`端点发出GET请求。

**API格式**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| 参数 | 描述 |
| --- | --- |
| `{PACKAGE_ID}` | 要导入的资源包的ID。 |

**请求**

以下请求检查您对{PACKAGE_ID}和沙盒的权限。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/preflight/{PACKAGE_ID}?targetSandbox=<sandbox_name> \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回目标沙盒的资源权限，包括所需的权限列表、缺少的权限、工件的类型以及是否允许创建的决定。

+++查看响应

```json
{
  "packageID": "b7bda68eb1214c86824f1d7204616e51",
  "targetSandboxName": "acme-sandbox",
  "permissionResponse": [
    {
      "artifactID": "4aca57b6-8b83-450b-a460-e8a07ca79a44",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "Schema",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "Segment",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Composition",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Query",
            "resourcePermissions": [
              "write"
            ]
          },
          {
            "palmResourceType": "SegmentDashboard",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": []
      },
      "artifactType": "PROFILE_SEGMENT",
      "creationAllowed": true
    },
    {
      "artifactID": "36bb82bc-a00d-4d6b-a598-227d43e027c1",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": [
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "artifactType": "PROFILE_MERGE",
      "creationAllowed": false
    }
  ]
}
```

+++

## 列出导出/导入作业 {#list-jobs}

您可以通过向`/packages`端点发出GET请求来列出当前的导出/导入作业。

**API格式**

```http
GET /packages/jobs?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMS}` | 用于筛选结果的可选查询参数。 有关详细信息，请参阅[查询参数](./appendix.md)上的部分。 |

**请求**

以下请求列出了所有成功的导入作业。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应将返回所有成功的导入作业。

```json
{
    "totalElements": 42,
    "currentPage": 0,
    "totalPages": 9,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "3c1b92cf47a246d7bfbe6fd507c5d543",
            "name": "acme",
            "updated": 1685973675401,
            "created": 1685973675401,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "ead59d21405f4184a94dd786a1bf040d",
            "name": "acme1",
            "updated": 1685986367198,
            "created": 1685986367198,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "85ddaa3c2f6c475088167cde7a9d4326",
            "name": "acme2",
            "updated": 1686147692568,
            "created": 1686147692568,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "c49a4fcb31954cbd828ece1da096c8f5",
            "name": "acme3",
            "updated": 1686148007586,
            "created": 1686148007586,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "a3669315baed4cf2af49bf9ce90b8158",
            "name": "acme4",
            "updated": 1686148651910,
            "created": 1686148651910,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        }
    ]
}
```

## 跨组织共享包 {#org-linking}

沙盒工具API中的`/handshake`端点允许您与其他组织合作以共享包。

### 发送共享请求 {#send-request}

通过向`/handshake/bulkCreate`端点发出POST请求，向目标合作伙伴组织发送共享批准请求。 在共享专用包之前，必须填写此字段。

**API格式**

```http
POST /handshake/bulkCreate
```

**请求**

以下请求将启动目标伙伴组织与来源组织之间的共享审批。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/handshake/bulkCreate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "targetIMSOrgIds":["acme@AdobeOrg"],
      "sourceIMSDetails":{
        "id":"acme@AdobeOrg",
        "name":"acme_org"
      } 
  }' 
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `targetIMSOrgIds` | 要向其发送共享请求的目标组织的列表。 | 数组 | 是 |
| `sourceIMSDetails` | 有关源组织的详细信息。 | 对象 | 是 |

**响应**

成功的响应将返回有关共享请求的详细信息。

```json
{
    "successfulRequests": {
        "acme@AdobeOrg": {
            "id": "{ID}",
            "version": 0,
            "createdDate": 1724938816798,
            "modifiedDate": 1724938816798,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va6",
            "sourceIMSOrgName": "{SOURCE_NAME}",
            "status": "APPROVAL_PENDING",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{ORG_ID}",
            "statusHistory": "[{\"actionTakenBy\":\"acme@98ff67fa661fdf6549420b.e\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724938816885}]",
            "linkingId": "{LINKING_ID}"
        }
    },
    "failedRequests": {}
}
```

### 批准已接收的共享请求 {#approve-requests}

通过向`/handshake/action`端点发出POST请求，批准来自目标合作伙伴组织的共享请求。 批准后，源合作伙伴组织可以共享私有包。

**API格式**

```http
POST /handshake/action
```

**请求**

以下请求批准来自目标合作伙伴组织的共享请求。

```shell
curl -X POST  \
  https://platform.adobe.io/data/foundation/exim/handshake/action \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "linkingID":"{LINKING_ID}",
      "status":"APPROVED",
      "reason":"Done",
      "targetIMSOrgDetails":{
          "id":"acme@AdobeOrg",
          "name":"acme",
          "region":"va7"
      }
  }'
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `linkingID` | 您正在响应的共享请求的ID。 | 字符串 | 是 |
| `status` | 对共享请求执行的操作。 可接受的值为`APPROVED`或`REJECTED`。 | 字符串 | 是 |
| `reason` | 执行操作的原因。 | 字符串 | 是 |
| `targetIMSOrgDetails` | 有关ID值应为目标组织的&#x200B;**ID**、名称值应为目标组织的&#x200B;**NAME**&#x200B;以及区域值应为目标组织&#x200B;**REGION**&#x200B;的目标组织的详细信息。 | 对象 | 是 |

**响应**

成功的响应将返回有关批准的共享请求的详细信息。

```json
{
    "id": "{ID}",
    "version": 1,
    "createdDate": 1726737474000,
    "modifiedDate": 1726737541731,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "sourceRegion": "va7",
    "targetRegion": "va7",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetOrgName": "{TARGET_ORG}",
    "status": "APPROVED",
    "createdByName": "{CREATED_BY}",
    "modifiedByIMSOrgId": "{MODIFIED_BY}",
    "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"acme@AdobeOrg\",\"action\":\"INITIATED\",\"actionTimeStamp\":1726737474450,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":null,\"actionTakenByImsOrgID\":\"745F37C35E4B776E0A49421B@AdobeOrg\",\"action\":\"APPROVED\",\"actionTimeStamp\":1726737541818,\"reason\":\"Done\"}]",
    "linkingId": "{LINKING_ID}"
}
```

### 列出传出/传入的共享请求 {#outgoing-and-incoming-requests}

通过向`handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING`端点发出GET请求，列出传出和传入的共享请求。

**API格式**

```http
GET handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING
```

| 参数 | 接受/默认值 |
| --- | --- |
| `property` | 指定要作为筛选依据的属性，如状态。 状态的可接受值为： `APPROVED`、`REJECTED`和`IN_PROGRESS`。 |
| `start` | start的默认值为`0`。 |
| `limit` | 限制的默认值为`20`。 |
| `orderBy` | 按升序或降序对记录进行排序。 |
| `requestType` | 接受`INCOMING`或`OUTGOING`。 |

**请求**

以下请求返回所有传出和传入的共享请求的列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id:{ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**响应**

成功的响应将返回传出和传入共享请求的列表及其详细信息。

```json
{
    "totalElements": 1,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "version": 1,
            "createdDate": 1724929446000,
            "modifiedDate": 1724929617000,
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va7",
            "targetRegion": "va6",
             "sourceOrgName": "{SOURCE_ORG}",
            "targetOrgName": "{TARGET_ORG}",
            "status": "APPROVED",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{MODIFIED_BY}",
            "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724929442467,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"APPROVED\",\"actionTimeStamp\":1724929617531,\"reason\":\"Done\"}]",
            "linkingId": "{LINKING_ID}"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

## 传输包

使用沙盒工具API中的`/transfer`端点获取和创建新的包共享请求。

### 新建共享请求 {#share-request}

获取已发布的源组织的包，并通过在提供包ID和目标组织的ID的同时向`/transfer`端点发出POST请求将其与目标组织共享。

**API格式**

```http
POST /transfer
```

**请求**

以下请求会获取一个源组织包并将其与目标组织共享。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "packageId": "{PACKAGE_ID}",
      "targets": [
          {
              "imsOrgId": "{TARGET_IMS_ORG}"
          }
      ]
  }'
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `packageId` | 要共享的包的ID。 | 字符串 | 是 |
| `targets` | 要与之共享的组织列表。 | 数组 | 是 |

**响应**

成功的响应会返回所请求资源包及其共享状态的详细信息。

```json
[
    {
        "id": "{ID}",
        "version": 0,
        "createdDate": 1726480559313,
        "modifiedDate": 1726480559313,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceIMSOrgId": "{ORG_ID}",
        "targetIMSOrgId": "{TARGET_ID}",
        "packageId": "{PACKAGE_ID}",
        "status": "PENDING",
        "initiatedBy": "acme@3ec9197a65a86f34494221.e",
        "requestType": "PRIVATE"
    }
]
```

### 按ID获取共享请求 {#fetch-transfer-by-id}

在提供传输ID的同时，通过向`/transfer/{TRANSFER_ID}`端点发出GET请求来获取共享请求的详细信息。

**API格式**

```http
GET /transfer/{TRANSFER_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{TRANSFER_ID}` | 要获取的传输的ID。 |

**请求**

以下请求获取ID为{TRANSFER_ID}的传输。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/0c843180a64c445ca1beece339abc04b \
  -H 'x-api-key: {API__KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**响应**

成功响应会返回共享请求的详细信息。

```json
{
    "id": "{ID}",
    "sourceIMSOrgId": "{ORG_ID}",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetIMSOrgId": "{TARGET_ID}",
    "targetOrgName": "{TARGET_ORG}",
    "packageId": "{PACKAGE_ID}",
    "packageName": "{PACKAGE_NAME}",
    "status": "COMPLETED",
    "initiatedBy": "{INITIATED_BY}",
    "createdDate": 1724442856000,
    "requestType": "PRIVATE"
}
```

### 获取共享列表 {#transfers-list}

通过对`/transfer/list?{QUERY_PARAMETERS}`端点发出GET请求并根据需要更改查询参数，获取传输请求列表。

**API格式**

```http
GET `/transfer/list?{QUERY_PARAMETERS}`
```

| 参数 | 接受/默认值 |
| --- | --- |
| `property` | 指定要作为筛选依据的属性，如状态。 状态的可接受值为： `COMPLETED`、`PENDING`、`IN_PROGRESS`、`FAILED`。 |
| `start` | start的默认值为`0`。 |
| `limit` | 限制的默认值为`20`。 |
| `orderBy` | 排序仅接受`createdDate`字段。 |

**请求**

以下请求从提供的搜索参数中获取传输请求的列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status==COMPLETED&start=0&limit=2&orderBy=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**响应**

成功的响应会从提供的搜索参数返回所有传输请求的列表。

```json
{
    "totalElements": 43,
    "currentPage": 0,
    "totalPages": 22,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726129077000,
            "createdDate": 1726129062000,
            "requestType": "PRIVATE"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726066046000,
            "createdDate": 1726065936000,
            "requestType": "PRIVATE"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

### 将程序包可用性从专用更新为公用 {#update-availability}

通过向`/packages/update`端点发出GET请求，将包从专用更改为公用。 默认情况下，将使用专用可用性创建包。

**API格式**

```http
PUT `/packages/update`
```

**请求**

以下请求将包的可用性从专用更改为公用。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
      "id":"{ID}",
      "action":"UPDATE",
      "packageVisibility":"PUBLIC"
  }'
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `id` | 要更新的程序包的ID。 | 字符串 | 是 |
| `action` | 若要将可见性更新为公开，操作值应为&#x200B;**UPDATE**。 | 字符串 | 是 |
| `packageVisbility` | 要更新可见性，packageVisibility值应为&#x200B;**PUBLIC**。 | 字符串 | 是 |

**响应**

成功的响应将返回有关包及其可见性的详细信息。

```json
{
    "id": "{ID}",
    "version": 7,
    "createdDate": 1729624618000,
    "modifiedDate": 1729658596340,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "name": "acme",
    "imsOrgId": "{ORG_ID}",
    "packageType": "PARTIAL",
    "expiry": 1737434596325,
    "status": "PUBLISH_FAILED",
    "packageVisibility": "PUBLIC",
    "artifactsList": [
        {
            "id": "{ID}",
            "type": "PROFILE_SEGMENT",
            "found": false,
            "count": 0,
            "title": "Acme Profile Segment"
        }
    ],
    "schemaMapping": {},
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    }
}
```

### 请求导入公共资源包 {#pull-public-package}

通过向`/transfer/pullRequest`端点发出POST请求，从具有公共可用性的源组织导入包。

**API格式**

```http
POST /transfer/pullRequest
```

**请求**

以下请求将导入资源包，并将它设置为对公众可用。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/pullRequest \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "imsOrgId": "{ORG_ID}",
      "packageId": "{PACKAGE_ID}"
  }'
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `imsOrgId` | 程序包源组织的ID。 | 字符串 | 是 |
| `packageId` | 要导入的资源包中的ID。 | 字符串 | 是 |

**响应**

成功响应将返回有关导入的公共包的详细信息。

```json
{
    "id": "{ID}",
    "version": 0,
    "createdDate": 1729658890425,
    "modifiedDate": 1729658890425,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "packageId": "{PACKAGE_ID}",
    "status": "PENDING",
    "initiatedBy": "{INITIATED_BY}",
    "pipelineMessageId": "{MESSAGE_ID}",
    "requestType": "PUBLIC"
}
```

### 列出公共包 {#list-public-packages}

通过对`/transfer/list?{QUERY_PARAMS}`端点发出GET请求获取具有公开可见性的包列表。

**API格式**

```http
GET /transfer/list?{QUERY_PARAMS}
```

| 参数 | 接受/默认值 |
| --- | --- |
| `property` | 指定要作为筛选依据的属性，如状态。 状态的可接受值为： `COMPLETED`和`FAILED`。 |
| `start` | start的默认值为`0`。 |
| `limit` | 限制的默认值为`20`。 |
| `orderBy` | 排序仅接受`createdDate`字段。 |
| `requestType` | 接受`PUBLIC`或`PRIVATE`。 |

**请求**

以下请求会获取具有公共可用性的包的列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status%3D%3DCOMPLETED%2CFAILED&requestType=PUBLIC&orderby=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**响应**

成功的响应将返回公共包及其详细信息的列表。

+++查看响应

```json
{
    "totalElements": 14,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359318000,
            "createdDate": 1729359316000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359284000,
            "createdDate": 1729359283000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Test Private Flow Final",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284462000,
            "createdDate": 1729275962000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOUCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Fest",
            "status": "FAILED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284104000,
            "createdDate": 1729253854000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284667000,
            "createdDate": 1729253421000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284957000,
            "createdDate": 1729253143000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284562000,
            "createdDate": 1729252975000,
            "requestType": "PUBLIC"
        },
        {
               "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Private Package Test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284262000,
            "createdDate": 1729229755000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Demo Package 1016",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284784000,
            "createdDate": 1729208888000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284934000,
            "createdDate": 1729153097000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284912000,
            "createdDate": 1729153043000,
            "requestType": "PUBLIC"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

+++

## 复制包有效负载(#package-payload)

通过向`/packages/payload`端点发出GET请求，您可以复制公共包的有效负载，该端点在请求路径中包含包的相应ID。

**API格式**

```http
GET /packages/payload/{PACKAGE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{PACKAGE_ID}` | 要复制的包的ID。 |

**请求**

以下请求提取ID为{PACKAGE_ID}的包的有效负载。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/payload/{PACKAGE_ID} \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `imsOrdId` | 包所属的组织的ID。 | 字符串 | 是 |
| `packageId` | 您请求的有效负载的程序包的ID。 | 字符串 | 是 |

**响应**

成功的响应将返回包的有效负载。

```json
{
    "imsOrgId": "{ORG_ID}",
    "packageId": "{PACKAGE_ID}"
}
```

## 迁移对象配置更新

使用沙盒工具API中的/packages端点迁移对象配置更新。

### 更新操作(#update-operations)

将指定的或最新版本的包快照与源沙盒的当前状态或以前使用的目标沙盒进行比较，其中通过提供包ID向`/packages/{packageId}/version/compare`端点发出POST请求来导入包。

***API格式***

```http
PATCH /packages/{packageId}/version/compare
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `packageId` | 程序包的ID。 | 字符串 | 是 |

**请求**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/version/compare/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
      "triggerNew": true,
      "targetSandbox": "{SANDBOX_NAME}"
  }'
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `triggerNew` | 用于触发新的差异计算作业的标志，即使已存在活动作业或完成的作业也是如此。 | 布尔值 | 否 |
| `targetSandbox` | 表示必须用来计算差异的目标沙盒的名称。 如果未指定，则源沙盒将用作目标沙盒。 | 字符串 | 否 |

**响应**

对以前完成的作业的成功响应将返回作业对象以及以前计算的差异结果。 新完成的作业将返回作业ID。

+++查看响应（已提交的作业）

```json
{
    "status": "OK",
    "type": "SUCCESS",
    "ajo": false,
    "message": "Job with ID: {JOB_ID}",
    "object": {
        "id": "c4b7d07ae4c646279e2070a31c50bd5c",
        "name": "Compute Job Package: {SNAPSHOT_ID}",
        "description": null,
        "visibility": "TENANT",
        "requestType": "VERSION",
        "expiry": 0,
        "snapshotId": "{SNAPSHOT_ID}",
        "packageVersion": 0,
        "createdTimestamp": 0,
        "modifiedTimestamp": 0,
        "type": "PARTIAL",
        "jobStatus": "SUCCESS",
        "jobType": "COMPUTE",
        "counter": 0,
        "imsOrgId": "{ORG_ID}",
        "sourceSandbox": {
            "name": "prod",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "destinationSandbox": {
            "name": "amanda-1",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "deltaPackageVersion": {
            "packageId": "{PACKAGE_ID}",
            "currentVersion": 0,
            "validated": false,
            "rootArtifacts": [
                {
                    "id": "https://ns.adobe.com/sandboxtoolingstage/schemas/355f461cbfb662fd0d12d06aeab34e206efcfa5d913604de",
                    "type": "REGISTRY_SCHEMA",
                    "found": false,
                    "count": 0
                }
            ],
            "eximGraphDelta": {
                "vertices": [],
                "pluginDeltas": [
                    {
                        "sourceArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/9fad8b185640a2db7daf9bb1295543ee8cb5965d80a21e8d",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 2"
                        },
                        "targetArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/b7fa3024777ef11b68c5121e937d8543677093f4f0e63a5f",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 2_1738766274074"
                        },
                        "changes": [
                            {
                                "op": "replace",
                                "path": "/title",
                                "oldValue": "Custom FieldGroup 2_1738766274074",
                                "newValue": "Custom FieldGroup 2"
                            },
                            {
                                "op": "replace",
                                "path": "/description",
                                "oldValue": "Description for furnished object",
                                "newValue": ""
                            }
                        ]
                    },
                    {
                        "sourceArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/304ac900943716c8bd99e6aaf6aa840aac91995729f1987f",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 4"
                        },
                        "targetArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/34c9add91cce4a40d68a0e715c9f0a16048871734f8c8b74",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 4_1738766274074"
                        },
                        "changes": [
                            {
                                "op": "replace",
                                "path": "/title",
                                "oldValue": "Custom FieldGroup 4_1738766274074",
                                "newValue": "Custom FieldGroup 4"
                            },
                            {
                                "op": "replace",
                                "path": "/description",
                                "oldValue": "Description for furnished object",
                                "newValue": ""
                            }
                        ]
                    }
                ]
            }
        },
        "importReplacementMap": {
            "https://ns.adobe.com/sandboxtoolingstage/mixins/9fad8b185640a2db7daf9bb1295543ee8cb5965d80a21e8d": "https://ns.adobe.com/sandboxtoolingstage/mixins/b7fa3024777ef11b68c5121e937d8543677093f4f0e63a5f",
            "5a45f8cd309d5ed5797be9a0af65e89152a51d57a6c74b52": "4ae041fa182d6faf2e7c56463399170d913138a7c5712909",
            "https://ns.adobe.com/sandboxtoolingstage/schemas/b2b7705e770a35341b8bc5ec5e3644d9c7387266777fe4ba": "https://ns.adobe.com/sandboxtoolingstage/schemas/838c4e21ad81543ac14238ac1756012f7f98f0e0bec6b425",
            "https://ns.adobe.com/sandboxtoolingstage/schemas/355f461cbfb662fd0d12d06aeab34e206efcfa5d913604de": "https://ns.adobe.com/sandboxtoolingstage/schemas/9a55692d527169d0239e126137a694ed9db2406c9bcbd06a",
            "8f45c79235c91e7f0c09af676a77d170a34b5ee0ad5de72c": "65d755cc3300674c3cfcec620c59876af07f046884afd359",
            "f04b8e461396ff426f8ba8dc5544f799bf287baa8e0fa5c": "b6fa821ada8cb97cac384f0b0354bbe74209ec97fb6a83a3",
            "https://ns.adobe.com/sandboxtoolingstage/mixins/304ac900943716c8bd99e6aaf6aa840aac91995729f1987f": "https://ns.adobe.com/sandboxtoolingstage/mixins/34c9add91cce4a40d68a0e715c9f0a16048871734f8c8b74",
            "c8304f3cb7986e8c9b613cd8d832125bd867fb4a5aedf67a": "4d21e9bf89ce0042b52d7d41ff177a7697d695e2617d1fc1"
        },
        "schemaFieldMappings": null
    }
}
```

+++

+++查看响应（新提交的作业）

```json
{
    "status": "OK",
    "type": "SUCCESS",
    "ajo": false,
    "message": "Job with ID: {JOB_ID}",
    "object": {
        "id": "aa5cfacf35a8478c8cf44a675fab1c30 ",
        "name": "Compute Job Package: {SNAPSHOT_ID}",
        "description": null,
        "visibility": "TENANT",
        "requestType": "VERSION",
        "expiry": 0,
        "snapshotId": "{SNAPSHOT_ID}",
        "packageVersion": 0,
        "createdTimestamp": 0,
        "modifiedTimestamp": 0,
        "type": "PARTIAL",
        "jobStatus": "IN_PROGRESS",
        "jobType": "COMPUTE",
        "counter": 0,
        "imsOrgId": "{ORG_ID}",
        "sourceSandbox": {
            "name": "prod",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "destinationSandbox": {
            "name": "amanda-1",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "schemaFieldMappings": null
    }
}
```

+++

### 更新包版本(#package-versioning)

通过提供包ID向`/packages/{packageId}/version/save`端点发出GET请求，使用每个对象的源沙盒中的最新快照将包升级到新版本。

***API格式***

```http
PATCH /packages/{packageId}/version/save
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `packageId` | 程序包的ID。 | 字符串 | 是 |

**请求**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/version/save/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
```

**响应**

成功响应将返回版本升级的作业状态。

```json
{
    "id": "3cec9bae662e43d9b9106fcbf7744a75",
    "name": "Version Job Package: {JOB_ID}",
    "description": null,
    "visibility": "TENANT",
    "requestType": "VERSION",
    "expiry": 0,
    "snapshotId": "{SNAPSHOT_ID}",
    "packageVersion": 2,
    "createdTimestamp": 0,
    "modifiedTimestamp": 0,
    "type": "PARTIAL",
    "jobStatus": "PENDING",
    "jobType": "UPGRADE",
    "counter": 0,
    "imsOrgId": "{ORG_ID}",
    "sourceSandbox": {
        "name": "prod",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "destinationSandbox": {
        "name": "prod",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "schemaFieldMappings": null
}
```

### 检索包版本历史记录(#package-version-history)

通过提供包ID向`/packages/{packageId}/history`端点发出GET请求，检索包的版本控制历史记录，包括时间戳和修饰符。

***API格式***

```http
PATCH /packages/{packageId}/history
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `packageId` | 程序包的ID。 | 字符串 | 是 |

**请求**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/history/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
```

**响应**

成功的响应将返回包的版本历史记录。

```json
[
    {
        "id": "cb68591a1ed941e191e7f52e33637a26",
        "version": 0,
        "createdDate": 1739516784000,
        "modifiedDate": 1739516784000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "imsOrgId": "{ORG_ID}",
        "packageVersion": 3
    },
    {
        "id": "e26189e6e4df476bb66c3fc3e66a1499",
        "version": 0,
        "createdDate": 1739343268000,
        "modifiedDate": 1739343268000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "imsOrgId": "{ORG_ID}",
        "packageVersion": 2
    },
    {
        "id": "11af34c0eee449ac84ef28c66d9383e3",
        "version": 0,
        "createdDate": 1739343073000,
        "modifiedDate": 1739343073000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "imsOrgId": "{ORG_ID}",
        "packageVersion": 1
    }
]
```

### 提交更新作业(#submit-update)

通过提供包ID，向`/packages/{packageId}/import`端点发出PATCH请求，将新更新推送到目标沙盒对象。

***API格式***

```http
PATCH /packages/{packageId}/import
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `packageId` | 程序包的ID。 | 字符串 | 是 |

**请求**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
      "id": "50fd94f8072b4f248737a2b57b41058f",
      "name": "Test Update",
      "destinationSandbox": {
        "name": "test-sandbox-sbt",
        "imsOrgId": "{ORG_ID}"
      },
      "overwriteMappings": {
        "https://ns.adobe.com/sandboxtoolingstage/schemas/327a48c83a5359f8160420a00d5a07f0ba8631a1fd466f9e" : {
            "id" : "https://ns.adobe.com/sandboxtoolingstage/schemas/e346bb2cd7b26576cb51920d214aebbd42940a9bf94a75cd",
            "type" : "REGISTRY_SCHEMA"
        }
      }
  }'
```

**响应**

成功的响应将返回更新的作业ID。

```json
{
    "id": "3cec9bae662e43d9b9106fcbf7744a75",
    "name": "Update Job Name",
    "description": "Update Job Description",
    "visibility": "TENANT",
    "requestType": "IMPORT",
    "expiry": 0,
    "snapshotId": "{SNAPSHOT_ID}",
    "packageVersion": 2,
    "createdTimestamp": 0,
    "modifiedTimestamp": 0,
    "type": "PARTIAL",
    "jobStatus": "PENDING",
    "jobType": "UPDATE",
    "counter": 0,
    "imsOrgId": "{ORG_ID}",
    "sourceSandbox": {
        "name": "prod",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "destinationSandbox": {
        "name": "amanda-1",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "schemaFieldMappings": null
}
```

### 禁用包的更新和覆盖(#disable-update)

通过提供包ID向`/packages/{packageId}/?{QUERY_PARAMS}`端点发出GET请求，禁用对不支持它们的包的更新和覆盖。

***API格式***

```http
PATCH /packages/{packageId}?{QUERY_PARAMS}
```

| 属性 | 描述 | 类型 | 必需 |
| --- | --- | --- | --- |
| `packageId` | 程序包的ID。 | 字符串 | 是 |
| {QUERY_PARAM} | getCapabilites查询参数。 应将此项设置为`true`或`false` | 布尔值 | 是 |

**请求**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}?getCapabilities=true'/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
```

**响应**

成功的响应将返回包功能的列表。

```json
{
    "id": "80230dde96574a828191144709bb9b51",
    "version": 3,
    "createdDate": 1749808582000,
    "modifiedDate": 1749808648000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "name": "Ankit_Primary_Descriptor_Test",
    "description": "RestPackage",
    "imsOrgId": "{ORG_ID}",
    "clientId": "usecasebuilder",
    "packageType": "PARTIAL",
    "expiry": 1757584598000,
    "publishDate": 1749808648000,
    "status": "PUBLISHED",
    "packageVisibility": "PRIVATE",
    "latestPackageVersion": 0,
    "packageAccessType": "TENANT",
    "artifactsList": [
        {
            "id": "https://ns.adobe.com/sandboxtoolingstage/schemas/1c767056056de64d8030380d1b9f570d26bc15501a1e0e95",
            "altId": null,
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0
        }
    ],
    "schemaMapping": {},
    "sourceSandbox": {
        "name": "atul-sandbox",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "packageCapabilities": {
        "capabilities": [
            "VERSIONABLE"
        ]
    }
}
```
