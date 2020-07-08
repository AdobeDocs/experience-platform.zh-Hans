---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建沙箱
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 2%

---


# 创建沙箱

可以通过向端点发出POST请求来创建新沙 `/sandboxes` 箱。

**API格式**

```http
POST /sandboxes
```

**请求**

以下请求将创建一个名为“dev-3”的新开发沙箱。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 将来请求中用于访问沙箱的标识符。 此值必须是唯一的，最佳实践是使其尽可能具有描述性。 不能包含任何空格或大写字母。 |
| `title` | 用于平台用户界面中显示目的的可读名称。 |
| `type` | 要创建的沙箱类型。 目前，组织只能创建“开发”类型沙箱。 |

**响应**

成功的响应会返回新创建的沙箱的详细信息，显示其 `state` 正在“创建”。

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>沙箱需要大约15分钟时间才能由系统进行配置，之后 `state` 沙箱将变为“活动”或“失败”。
