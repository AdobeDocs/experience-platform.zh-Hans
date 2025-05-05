---
title: 访客识别
description: 了解Adobe Experience Platform Edge Network API如何识别访客
seo-description: Learn how Adobe Experience Platform Edge Network API identifies visitors
keywords: 边缘网络；网关；API；访客；标识
exl-id: aa2f3b83-5cc8-4e02-9119-edfd5e212588
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 4%

---

# 访客识别

Edge Network API支持通过第一方ID ([!DNL FPID]) [&#128279;](visitor-identification-fpid.md)进行访客识别。

所有用户标识都应在`identityMap`字段组中提供。 此字段组包含在AEP Web SDK `ExperienceEvent` mixin中。

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

## 设备标识符 {#identifiers}

在Edge Network中，可以通过多种方法来识别设备。 有关支持的ID的概述，请参阅下表。

| ID 命名空间 | 管理者 | 描述 |
| --- | --- | --- |
| `FPID` | 客户 | `FPID`将由Edge Network自动编码为`ECID`，因此需要`ECID`的解决方案也将正常工作。  <br><br>要获得一致的设备标识，这些ID必须保留在设备上并在每个请求中提供。 对于Web交互，这涉及将它们存储为浏览器Cookie。 |
| `IDFA`/`GAID` | Experience Platform | 可以跨应用程序识别用户，因此Edge Network不会将这些ID编码为`ECID`。 |

<!--
| `ECID` | Adobe | `ECID` is required when leveraging and integrating with Adobe Analytics and Adobe Audience Manager. <br><br> For consistent device identification, these IDs must be persisted on the device and supplied on each request. For web interactions, this involves storing them as browser cookies. |
-->

<!--
## Edge Network Identity Protocol {#experience-edge-identity-protocol}

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
>The `meta.state.domain` is an optional value which a caller could supply, specifying the exact domain on which the cookies should be stored. When this is missing, the Edge Network can automatically infer the top-level domain from the request. Automatic client state management via browser cookies **should never be used** in a `server` interaction.

-->
