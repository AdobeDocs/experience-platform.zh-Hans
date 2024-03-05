---
title: 使用边缘网络服务器API进行服务器端个性化
description: 本文演示了如何使用边缘网络服务器API在Web资产上部署服务器端个性化。
keywords: 个性化；服务器api；边缘网络；服务器端；
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---


# 使用边缘网络服务器API进行服务器端个性化

## 概述 {#overview}

服务器端个性化涉及使用 [边缘网络服务器API](../../server-api/overview.md) 使客户在您的Web资产上获得个性化的体验。

在本文中描述的示例中，使用服务器API在服务器端检索个性化内容。 然后，基于检索到的个性化HTML在服务器端呈现内容。

下表显示了一个个性化内容和非个性化内容的示例。

| 不进行个性化的示例页面 | 具有个性化的示例页面 |
|---|---|
| ![没有个性化的网页示例](assets/plain.png) | ![具有个性化的网页示例](assets/personalized.png) |

## 注意事项 {#considerations}

### Cookie {#cookies}

Cookie用于保留用户标识和群集信息。  使用服务器端实施时，应用程序服务器在请求生命周期内处理这些Cookie的存储和发送。

| Cookie | 用途 | 存储者 | 发送者 |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | 包含用户身份详细信息。 | 应用程序服务器 | 应用程序服务器 |
| `kndctr_AdobeOrg_cluster` | 指示应使用哪个Edge Network群集来完成请求。 | 应用程序服务器 | 应用程序服务器 |

### 请求投放 {#request-placement}

需要个性化请求才能获取建议并发送显示通知。 使用服务器端实施时，应用程序服务器向Edge Network服务器API发出这些请求。

| 请求 | 创建者 |
|---|---|
| 用于检索建议的Interact请求 | 应用程序服务器调用Edge Network服务器API。 |
| Interact请求发送显示通知 | 应用程序服务器调用Edge Network服务器API。 |

## 示例应用程序 {#sample-app}

下面描述的流程使用一个示例应用程序，您可以将其用作试验以及了解有关此类个性化的更多信息的起点。

您可以下载此示例，并根据自己的需求对其进行自定义。 例如，您可以更改环境变量，以便示例应用程序从您自己的Experience Platform配置中提取选件。

为此，请打开 `.env` 文件，并根据您的配置修改变量。 重新启动示例应用程序，您就可以尝试使用自己的个性化内容了。

### 运行示例 {#running-sample}

请按照以下步骤运行示例应用程序。

1. 克隆 [此存储库](https://github.com/adobe/alloy-samples) 到您的本地计算机。
2. 打开终端并导航到 `personalization-server-side` 文件夹。
3. 运行 `npm install`.
4. 运行 `npm start`.
5. 打开Web浏览器并导航至 `http://localhost`.

## 流程概述 {#process}

此部分介绍了检索个性化内容时所使用的步骤。

1. [Express](https://expressjs.com/) 用于精益服务器端实施。 这将处理基本服务器请求和路由。
2. 浏览器请求该网页。 之前由浏览器存储的所有Cookie，带有前缀 `kndctr_`中。
3. 当从应用程序服务器请求该页面时，会将事件发送到 [交互式数据收集端点](../../../server-api/interactive-data-collection.md) 以获取个性化内容。 示例应用程序使用辅助方法简化构建请求并将请求发送到API的过程(请参阅 [aepEdgeClient.js](https://github.com/adobe/alloy-samples/blob/main/common/aepEdgeClient.js))。 此 `POST` 请求包含 `event` 和 `query`. 上一步的Cookie（如果可用）包含在 `meta>state>entries` 数组。

   ```js
   fetch(
   "https://edge.adobedc.net/ee/v2/interact?dataStreamId=abc&requestId=123",
   {
      headers: {
         accept: "*/*",
         "accept-language": "en-US,en;q=0.9",
         "cache-control": "no-cache",
         "content-type": "text/plain; charset=UTF-8",
         pragma: "no-cache",
         "sec-fetch-dest": "empty",
         "sec-fetch-mode": "cors",
         "sec-fetch-site": "cross-site",
         "sec-gpc": "1",
         "Referrer-Policy": "strict-origin-when-cross-origin",
         Referer: "http://localhost/",
      },
      body: JSON.stringify({
         event: {
         xdm: {
            web: {
               webPageDetails: {
               URL: "http://localhost/",
               },
               webReferrer: {
               URL: "",
               },
            },
            identityMap: {
               FPID: [
               {
                  id: "xyz",
                  authenticatedState: "ambiguous",
                  primary: true,
               },
               ],
            },
            timestamp: "2022-06-23T22:21:00.878Z",
         },
         data: {},
         },
         query: {
         identity: {
            fetch: ["ECID"],
         },
         personalization: {
            schemas: [
               "https://ns.adobe.com/personalization/default-content-item",
               "https://ns.adobe.com/personalization/html-content-item",
               "https://ns.adobe.com/personalization/json-content-item",
               "https://ns.adobe.com/personalization/redirect-item",
               "https://ns.adobe.com/personalization/dom-action",
            ],
            decisionScopes: ["__view__", "sample-json-offer"],
         },
         },
         meta: {
         state: {
            domain: "localhost",
            cookiesEnabled: true,
            entries: [
               {
               "key": "kndctr_XXX_AdobeOrg_identity",
               "value": "abc123"
               },
               {
               "key": "kndctr_XXX_AdobeOrg_cluster",
               "value": "or2"
               }
            ],
         },
         },
      }),
      method: "POST",
   }
   ).then((res) => res.json());
   ```

4. 从响应中读取基于表单的活动的Target选件，并在生成HTML响应时使用。
5. 对于基于表单的活动，必须在实施中手动发送显示事件以指示何时显示选件。 在此示例中，通知在请求生命周期期间在服务器端发送。

   ```js
   function sendDisplayEvent(aepEdgeClient, req, propositions, cookieEntries) {
   const address = getAddress(req);
   
   aepEdgeClient.interact(
      {
         event: {
         xdm: {
            web: {
               webPageDetails: { URL: address },
               webReferrer: { URL: "" },
            },
            timestamp: new Date().toISOString(),
            eventType: "decisioning.propositionDisplay",
            _experience: {
               decisioning: {
               propositions: propositions.map((proposition) => {
                  const { id, scope, scopeDetails } = proposition;
   
                  return {
                     id,
                     scope,
                     scopeDetails,
                  };
               }),
               },
            },
         },
         },
         query: { identity: { fetch: ["ECID"] } },
         meta: {
         state: {
            domain: "",
            cookiesEnabled: true,
            entries: [...cookieEntries],
         },
         },
      },
      {
         Referer: address,
      }
   );
   }
   ```

6. [!DNL Visual Experience Composer (VEC)] 选件将被忽略，因为它们只能通过Web SDK渲染。
7. 当返回HTML响应时，应用服务器将在响应中设置标识和群集Cookie。