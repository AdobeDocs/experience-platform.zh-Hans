---
title: 审核事件导出API端点
description: 了解如何使用审计查询API以Experience Platform导出审计事件。
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: c7887391481def872c40dd6ed1193bf562b9d0cf
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 5%

---

# 导出审核事件列表

您可以通过向以下网站发出GET请求来检索事件数据： `/audit/export` 端点，指定要在有效负载中检索的事件。

**API格式**

```http
GET /audit/export
```

| 参数 | 描述 |
| --------- | ----------- |
| `timestamp` | 按时间戳过滤时，最佳做法是使用>和&lt;运算符来使用范围，而不是使用确切的值。 <br/>示例: `?property=timestamp<2020-02-08T02:46:48.610862Z&property=timestamp>2020-01-01T02:46:48.610862Z`. |
| `status` | 操作的状态。 状态可以是以下任一状态： </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul><br/>示例: `?property=status==Deny`. |
| `action` | 为事件记录的操作类型。 操作可以是以下任一操作： <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`Remove` </li><li>`Reset` </li><li>`Segment Activate` </li><li>`Segment remove` </li><li>`Update` </li></ul> 示例：`?property=action==Create`。 |
| `user` | 执行事件的用户。 |
| `assetType` | 执行操作的平台资源的类型。 <br/>示例: `?property=assetType==<an asset type>`. |

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**响应**

结果将生成到CSV文件中以供导出。 成功的响应返回不带响应正文的HTTP 307。 导出文件的链接提供在 `Location` 响应标头。
