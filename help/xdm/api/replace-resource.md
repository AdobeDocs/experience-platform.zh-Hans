---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 替换资源
topic: developer guide
translation-type: tm+mt
source-git-commit: 67826f838951b3202a6a04321c28daa8ee883d20

---


# 替换资源

模式注册表允许您通过PUT操作替换整个资源。 此操作实质上重写了资源，因此请求主体必须包含使用POST请求创建新资源时所需的所有字段。

如果要同时更新资源中的大量信息，此方法特别有用。

>[!NOTE] 如果只想更新部分资源而不是完全替换它，请参阅使用PATCH [操作更新资源的文档](update-resource.md)。

**API格式**

PUT请求只能针对您在租户容器中定义的资源执行。

```http
PUT /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{RESOURCE_TYPE}` | 要从模式库更新的资源类型。 有效类 `datatypes`型有 `mixins`、 `schemas`和 `classes`。 |
| `{RESOURCE_ID}` | 资源的URL编 `$id` 码的URI `meta:altId` 或URI。 |

**请求**

此示例请求替换在上一个示例中创建的“属性构造”数据类型。 请求主体的外观与用于创建数据类型的POST请求类似，只是它现在包含一组更新的字段，这些字段包含新值，替换了先前定义的值。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the construction of the property.",
        "type":"object",
        "properties": {
          "dateOpened": {
            "type":"string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "standAlone",
              "highRise",
              "stripMall"
            ],
            "meta:enum": {
              "standAlone": "Stand-Alone Building",
              "highRise": "High Rise Building",
              "stripMall": "Strip Mall"
            }
          },
          "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property."
          },
          "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property."
          }
        } 
      }'
```

**响应**

成功的响应会返回数据类型的详细信息，其中显示请求中提供的更新字段和值。

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the construction of the property.",
    "type": "object",
    "properties": {
        "dateOpened": {
            "type": "string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened.",
            "meta:xdmType": "date"
        },
        "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "standAlone",
                "highRise",
                "stripMall"
            ],
            "meta:enum": {
                "standAlone": "Stand-Alone Building",
                "highRise": "High Rise Building",
                "stripMall": "Strip Mall"
            },
            "meta:xdmType": "string"
        },
        "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property.",
            "meta:xdmType": "string"
        },
        "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property.",
            "meta:xdmType": "int"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.2",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552090569013,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
