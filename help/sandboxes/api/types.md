---
keywords: Experience Platform；首頁；熱門主題；清單沙箱
solution: Experience Platform
title: 沙箱型別API端點
description: 您可以向/sandboxTypes端點發出GET要求，以擷取貴組織支援的沙箱型別清單。
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 2%

---

# 沙箱型別端點

您可以透過向以下網站發出GET請求，為您的組織擷取受支援的沙箱型別清單： `/sandboxTypes` 端點。

## 快速入门

本指南中使用的API端點是 [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 擷取支援的沙箱型別清單

您可以透過向以下網站發出GET請求，為您的組織擷取受支援的沙箱型別清單： `/sandboxTypes` 端點。

**API格式**

```http
GET /sandboxTypes
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的回應會傳回貴組織支援的沙箱型別清單。

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
