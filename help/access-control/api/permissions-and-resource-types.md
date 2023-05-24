---
keywords: Experience Platform；首頁；熱門主題；存取控制許可權；存取控制資源型別；存取控制api
solution: Experience Platform
title: 參考API端點
description: 存取控制API中的參考端點可讓您檢視可用許可權和資源型別的名稱，然後可以使用這些名稱來檢視目前使用者的有效存取控制原則。
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# 參考端點

>[!NOTE]
>
>如果傳遞的是使用者權杖，則權杖的使用者必須具有請求組織的「組織管理員」角色。

您可以透過向以下專案發出GET請求，列出所有許可權和資源型別的名稱： `/acl/reference` 端點。 這些名稱隨後可用於對發出的API呼叫 [檢視有效的存取控制原則](./effective-policies.md) （目前使用者）。

許可權是透過Adobe Admin Console管理的原則，並對應至零個或多個資源型別原則。 資源型別是啟用特定型別之讀取、寫入和/或刪除功能的原則 [!DNL Platform] 資源（例如資料集或結構描述）。

**API格式**

```http
GET /acl/reference
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功的回應會傳回 `permissions` 物件和 `resource-types` 物件，分別包含存取許可權或資源型別的完整名稱清單。

```json
{
  "permissions": {
    "export-audience-for-segment": {
      "segments": [
        "read"
      ]
    },
    "manage-datasets": {
      "connection": [
        "read",
        "write",
        "delete"
      ],
      "datasets": [
        "read",
        "write",
        "delete"
      ]
    }
    {"..."}
  },
  "resource-types": {
    "classes": [
      "read",
      "write",
      "delete"
    ],
    "connection": [
      "read",
      "write",
      "delete"
    ],
    "data-types": [
      "read",
      "write",
      "delete"
    ],
    "...": [
      "..."
    ]
  }
}
```
