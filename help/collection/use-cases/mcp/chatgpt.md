---
title: 在ChatGPT应用程序中收集分析并应用个性化（MCP数据收集）
description: 使用混合MCP服务器+ Web SDK applyResponse模式将事件发送到Adobe Experience Platform Edge Network，并在ChatGPT应用程序UI中渲染个性化。
keywords: Adobe Experience Platform， Web SDK， Edge Network， MCP， ChatGPT应用程序， applyResponse，交互端点，个性化，分析
source-git-commit: c848f821ea911c82531c6784a17df0116572cd86
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# 在ChatGPT应用程序中收集分析并应用个性化（MCP数据收集）

此用例展示了如何将ChatGPT应用程序（模型上下文协议服务器+可选UI组件）连接到Adobe Experience Platform Edge Network。 通过此类数据收集，您可以记录对会话交互的分析，这些会话交互会调用您的工具，并将个性化决策从Edge Network交付到由ChatGPT呈现的小部件中。

>[!NOTE]
>
>本文档基于Adobe数据收集团队的最新可用更新和OpenAI的最新技术更新进行维护。 因此，Adobe预计此文档将会随着时间的推移而不断变化，因此建议检查更新。

此用例偏好使用混合方法，即使用服务器端实施来收集数据，使用客户端实施来呈现个性化内容。 此方法非常理想，因为MCP工具调用是收集分析的最可靠时机。 构件在浏览器上下文中运行，是存储身份（在Cookie中）和应用个性化决策的正确位置。

此用例附带了一个完全可操作的代码示例。 有关示例代码和实施说明，请参阅GitHub上[存储库中的](https://github.com/adobe/alloy-samples/tree/main/chatgpt-app)ChatGPT应用程序+ Adobe Experience Platform Edge`alloy-samples`。

>[!IMPORTANT]
>
>此页概述了一个用于说明集成模式的参考实施。 在应用程序中使用此方法之前，请查看安全性、隐私、同意和生产要求。

## 架构

在高层面上，有五个移动部分：

1. **MCP主机(ChatGPT)**： ChatGPT调用MCP服务器公开的工具，并在请求元数据中提供稳定的假名用户标识符。
1. **MCP服务器（后端）**：由您的组织拥有。 它实施列项、获取详细信息或提交请求等工具。
1. **Adobe IMS**：您的MCP服务器用于调用Adobe数据收集API的访问令牌存在问题。
1. **Adobe Experience Platform Edge Network**：接收由MCP服务器发送的体验事件，并返回Analytics确认、状态更新（如标识）和个性化决策。
1. **嵌入式Web UI（由MCP主机呈现的前端小组件）**：显示结构化结果并应用从MCP服务器后端接收的Adobe元数据。

## 数据流

1. **用户**&#x200B;使用您的MCP服务器提示&#x200B;**ChatGPT**。
1. **ChatGPT**&#x200B;解释提示的意图并调用相应的&#x200B;**后端MCP工具**。
1. **后端MCP服务器**&#x200B;使用数据收集API （`interact`终结点）向&#x200B;**Edge Network**&#x200B;发送体验事件以进行分析收集和可选个性化。
1. **Edge Network**&#x200B;将响应句柄（包括状态更新和个性化决策）返回到&#x200B;**后端MCP工具**。
1. **后端MCP工具**&#x200B;将包含`structuredContent`中的业务数据和`_meta`中的Adobe元数据的工具结果返回到&#x200B;**ChatGPT**。
1. **ChatGPT**&#x200B;将工具结果交付给&#x200B;**前端构件**，该构件将渲染业务数据并使用Web SDK JavaScript库的`applyResponse`命令应用Adobe元数据。 此命令与客户端状态水合，并在UI中呈现符合条件的个性化决策。

以下部分将详细介绍每个步骤。

## 步骤1：用户使用MCP服务器提示ChatGPT

此步骤是工作流的入口点。 用户提供自然语言意图：

```text
"Use the Adobe Office Information Tool to show me details about which office that is the most pet-friendly."
```

有关详细信息，请参阅OpenAI开发人员文档中的[构建MCP服务器](https://developers.openai.com/apps-sdk/build/mcp-server/)。

## 步骤2：ChatGPT解释意图并调用MCP工具

ChatGPT根据MCP服务器的元数据解释意图并在MCP服务器上调用相应的工具处理程序。 此工具调用为交互创建与UI渲染成功无关的服务器端真实点。 您的工具之一可能具有以下元数据：

```json
{
  "name": "office_details",
  "description": "Fetch details for a single office by ID and return personalization handles for the UI.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "sessionId": { "type": "string", "description": "Server-issued session identifier." },
      "officeId": { "type": "string", "description": "Office identifier." }
    },
    "required": ["sessionId", "officeId"],
    "additionalProperties": false
  },
  "_meta": {
    "ui": {
      "visibility": ["model", "app"]
    }
  }
}
```

有关如何告知ChatGPT每个MCP工具功能的更多信息，请参阅OpenAI开发人员文档中的[定义工具](https://developers.openai.com/apps-sdk/plan/tools/)。

## 步骤3：您的MCP服务器向Edge Network发送体验事件

当您的MCP服务器收到请求时，它会触发对Adobe Experience Platform Edge Network的调用，以记录分析数据并可以选择请求决策/个性化。 由于此请求是服务器到服务器，因此请使用经过身份验证的[`interact`](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/)终结点作为[数据收集API](https://developer.adobe.com/data-collection-apis/docs/)的一部分。 Adobe建议使用[自定义命名空间](https://experienceleague.adobe.com/zh-hans/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities)来传递OpenAI唯一标识符。 确保在身份UI中创建的命名空间与在调用中定义的身份命名空间匹配（区分大小写）。

```sh
curl -X POST "https://server.adobedc.net/ee/v2/interact?datastreamId={DATASTREAM_ID}"
  -H "Authorization: Bearer {TOKEN}"
  -H "x-gw-ims-org-id: {ORG_ID}"
  -H "x-api-key: {API_KEY}"
  -H "Content-Type: application/json"
  -d '{
    "event": {
      "xdm": {
        "eventType": "office.details.view",
        "identityMap": {
          "{IDENTITY_NAMESPACE}": [
            { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
          ]
        },
        "timestamp": "YYYY-02-20T19:00:00.000Z"
      }
    },
    "query": {
      "personalization": {
        "decisionScopes": ["__view__"]
      }
    },
    "meta": {
      "state": {
        "entries": [
          { "key": "kndctr_orgid_cluster", "value": "{CLUSTER_HINT_IF_KNOWN}" },
          { "key": "kndctr_orgid_identity", "value": "{ECID_BLOB_IF_KNOWN}" }
        ]
      }
    }
  }'
```

## 步骤4：Edge Network返回句柄

当Edge Network收到您的`interact`调用时，它使用`handle`数组进行响应。 此数组可以包括身份和个性化决策，具体取决于您的数据流配置。 示例响应可能如下所示：

```json
{
  "requestId": "60a2f...2294d",
  "handle": [
    {
      "type": "locationHint:result",
      "payload": [
        { "scope": "EdgeNetwork", "hint": "or2", "ttlSeconds": 1800 }
      ]
    },
    {
      "type": "state:store",
      "payload": [
        { "key": "kndctr_..._identity", "value": "CiYzM...snTI=", "maxAge": 34128000 },
        { "key": "kndctr_..._cluster", "value": "or2", "maxAge": 1800 }
      ]
    }
  ]
}
```

然后，MCP服务器可以从Edge Network响应中提取信息以保留身份信息：

```ts
type EdgeHandle = { type: string; payload?: Array<{ key?: string; value?: string }> };

export function extractStateStore(handles: EdgeHandle[]) {
  const store = handles.find(h => h.type === "state:store");
  const entries = store?.payload ?? [];

  const identity = entries.find(e => e.key?.includes("_identity"))?.value;
  const cluster  = entries.find(e => e.key?.includes("_cluster"))?.value;

  return { identity, cluster };
}
```

## 步骤5： MCP服务器将结构化工具输出以及Adobe元数据返回到ChatGPT

您的MCP工具响应包括来自Edge Network的结构化工具输出和个性化。

* `structuredContent`对象包含ChatGPT可以安全读取和讲述的业务数据。
* `_meta`对象包含Adobe响应句柄和服务器计算的`identityMap`，以便构件可以读取它们，而无需将该数据公开给ChatGPT。 将此信息保留在`_meta.adobe`中允许您在数据所在的位置上保持一致。 向前传递相同的`identityMap`有助于该构件在任何以后的UI端事件中使用相同的自定义标识。

```json
{
  "content": "Displayed details for office seattle.",
  "structuredContent": {
    "office": {
      "id": "seattle",
      "name": "Seattle",
      "amenities": ["Pet Friendly", "Cafe", "Bike Storage"]
    }
  },
  "_meta": {
    "adobe": {
      "identityMap": {
        "{IDENTITY_NAMESPACE}": [
          { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
        ]
      },
      "handles": [
        {
          "type": "state:store",
          "payload": [
            { "key": "kndctr_..._identity", "value": "..." }
          ]
        },
        {
          "type": "personalization:decisions",
          "payload": [
            { "id": "..." }
          ]
        }
      ]
    }
  }
}
```

有关详细信息，请参阅OpenAI开发人员参考中的[工具结果](https://developers.openai.com/apps-sdk/reference/#tool-results)。

## 步骤6：构件渲染结果并使用`_adobe.handles`应用`applyResponse`

该构件呈现来自`structuredContent`的业务数据，然后从`_meta.adobe`读取Adobe元数据。 在ChatGPT中，构件通过兼容性层可获得相同的数据：

* `window.openai.toolOutput`包含`structuredContent`
* `window.openai.toolResponseMetadata`包含`_meta`

该构件使用Web SDK JavaScript库的[`applyResponse`](../../js/commands/applyresponse.md)命令对客户端状态进行水化并渲染服务器端`interact`调用返回的个性化决策。 确保在调用[`configure`](../../js/commands/configure/overview.md)之前调用`applyResponse`命令。 由于您的MCP服务器执行了`interact`调用，因此您不需要立即调用工具调用交互的[`sendEvent`](../../js/commands/sendevent/overview.md)命令。

```js
// Configure the Web SDK before any other commands.
alloy("configure", {
  datastreamId: "YOUR_DATASTREAM_ID",
  orgId: "YOUR_EXPERIENCE_CLOUD_ORG_ID"
});

// Business data exposed to ChatGPT and the widget.
const { office } = window.openai?.toolOutput ?? {};

// Adobe metadata available only to the widget.
const adobe = window.openai?.toolResponseMetadata?.adobe ?? {};
const { identityMap, handles } = adobe;

// Hydrate client-side state and render personalization decisions from the
// server-side interact response.
alloy("applyResponse", {
  renderDecisions: true,
  responseBody: { handle: handles ?? [] }
});
```

如果该小组件稍后发送其他用户界面端事件，则您可在这些调用中包含相同的`identityMap`：

```js
alloy("sendEvent", {
  xdm: {
    eventType: "office.details.widgetView",
    identityMap
  }
});
```

此模式保持服务器端和用户界面标识使用一致，同时仍允许服务器端`interact`调用保持分析收集和决策的真实来源。

## 验证

配置上述所有步骤后，您可以验证以下内容：

* **数据收集：**&#x200B;验证事件是否到达所需的数据集，以及每个事件是否按预期处理。
* **Personalization：**&#x200B;验证决策是否由Edge Network返回，以及这些决策是否由您的小组件渲染。

## 安全和隐私注意事项

* 将ChatGPT的标识符视为敏感标识符，即使它们以假名表示。
* 确保将贵组织的同意和数据治理实践应用于此工作流。
* Adobe建议使用OAuth 2.1工作流进行授权。
* 确保访问令牌和密钥绝不会到达客户端或UI。
