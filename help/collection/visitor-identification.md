---
title: 访客识别
description: 瞭解Adobe Experience Platform Edge Network Server API如何識別訪客
seo-description: Learn how Adobe Experience Platform Edge Network Server API identifies visitors
keywords: 邊緣網路；閘道；API；訪客；識別
exl-id: aa2f3b83-5cc8-4e02-9119-edfd5e212588
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 5%

---

# 访客识别

Edge Network Server API支援 [透過第一方ID識別訪客([!DNL FPID])](visitor-identification-fpid.md).

所有使用者身分識別應提供於 `identityMap` 欄位群組。 此欄位群組包含在AEP Web SDK中 `ExperienceEvent` mixin.

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"55613368189701342632255821452918751312",
            "authenticatedState":"ambiguous"
         }
      ],
      "CRM":[
         {
            "id":"2394509340-30453470347",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

## 裝置識別碼 {#identifiers}

在Edge Network中識別裝置有多種方式。 請參閱下表，瞭解支援的ID概述。

| ID名稱空間 | 管理者 | 描述 |
| --- | --- | --- |
| `FPID` | Customer | `FPID` 將自動編碼為 `ECID` 因此，需要具備以下條件的解決方案： `ECID` 也會運作。  <br><br> 為了取得一致的裝置識別，這些ID必須儲存在裝置上，並在每個請求時提供。 針對網頁互動，這涉及將其儲存為瀏覽器Cookie。 |
| `IDFA`/`GAID` | Experience Platform | 可以跨應用程式識別使用者，因此這些ID不會編碼為 `ECID` 由Edge Network提供。 |

<!--
| `ECID` | Adobe | `ECID` is required when leveraging and integrating with Adobe Analytics and Adobe Audience Manager. <br><br> For consistent device identification, these IDs must be persisted on the device and supplied on each request. For web interactions, this involves storing them as browser cookies. |
-->

<!--
## Experience Edge Identity Protocol {#experience-edge-identity-protocol}

Device identities like `ECID` must be persisted on the client device and supplied on each request in the session and across sessions. Having stable device identities across multiple sessions improves the accuracy levels in your reports and allows delivering a consistent experience to the visitors.

For all non-server interactions, the Edge Network will automatically perform the following actions:

* Generate a new `ECID` when none is found on the request. This will automatically enhance the collected event with the new identity.
* Return a `state:store` instruction to the caller with the `kndctr_{$IMS_ORG_ID|url-safe}_identity` entry, which contains:
  * The [ID value](#ee-identity-format)
  * A `maxAge` value, in seconds, indicating how long the client persist the ID for

For example, let's consider the following request:

```json
{
   "events":[
      {
         "xdm":{
            "eventType":"web.webpagedetails.pageViews",
            "eventMergeId":"0772675a-1e24-44ea-a92b-0138c1d03a38",
            "web":{
               "webPageDetails":{
                  "URL":"https://alloystore.dev/",
                  "name":"home-demo-Home Page",
                  "pageViews":{
                     "value":1
                  }
               }
            },
            "device":{
               "screenHeight":1120,
               "screenWidth":1792,
               "screenOrientation":"landscape"
            },
            "environment":{
               "type":"browser",
               "browserDetails":{
                  "viewportWidth":1792,
                  "viewportHeight":481
               }
            },
            "timestamp":"2021-08-09T14:09:20.859Z"
         }
      }
   ]
}
```

The Edge Network response includes a `state:store` handle, which, in turn, includes an entry with the following name format: `kndctr_{$IMS_ORG_ID|url-safe}_identity`.

```json
{
   "requestId":"f5abf988-15d1-4463-a3b8-59aa0709a808",
   "handle":[
      {
         "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
         "value":"CiYzOTMyMzQ5NzU1MDY0MzIxNzc3NDEzMjY2NDA4OTIzOTExNDgyMlIRCIbghtqyLxABGAEqBElSTDHwAYbghtqyLw==",
         "maxAge":34128000
      }
   ],
   "type":"state:store"
}
```

>[!NOTE]
>
>The `kndctr_{$IMS_ORG_ID|url-safe}_` prefix is also used for other entries stored on the client device, and enables state isolation for complex integrations, which could involve multiple/different organizations. While the Edge Network will filter the entries which can be used for a given datastream, in order to minimize the payload, the caller (SDK) should ideally ensure that only the relevant entries are sent.

The caller must:

* Store this value on the client device
* Supply it on subsequent calls from that device in the request `meta.state.entries[]`, as shown below:

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYzOTMyMzQ5NzU1MDY0MzIxNzc3NDEzMjY2NDA4OTIzOTExNDgyMlIRCIbghtqyLxABGAEqBElSTDHwAYbghtqyLw=="
            }
         ]
      }
   }
}
```

## Identity Protocol via cookies (web)

When using first-party domain CNAMEs for interacting with the Edge Network, the client state can be managed automatically via first-party cookies.

The caller must explicitly activate this functionality via the `meta.state.cookiesEnabled` flag:

```json
{
   "meta":{
      "state":{
         "domain":"alloystore.dev",
         "cookiesEnabled":true
      }
   }
}
```

>[!NOTE]
>
>The `meta.state.domain` is an optional value which a caller could supply, specifying the exact domain on which the cookies should be stored. When this is missing, Experience Edge can automatically infer the top-level domain from the request. Automatic client state management via browser cookies **should never be used** in a `server` interaction.

-->
