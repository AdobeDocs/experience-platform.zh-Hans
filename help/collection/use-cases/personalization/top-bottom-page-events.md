---
title: 在Web SDK中配置页面顶部和底部事件
description: 本文介绍了如何在Web SDK中使用页面顶部和底部事件。
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 8058ee470717b95d30269a8072b12385c920c85f
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 1%

---


# 在Web SDK中配置页面顶部和底部事件

在投放个性化体验时，网页的加载时间至关重要。 为了最大程度地缩短用户等待个性化内容的时间，Web SDK支持配置页面事件的顶部和底部。

页面事件的顶部和底部描述了一种方法，该方法以异步方式加载页面中的各种元素，同时保持页面加载时间最短：

* 页面顶部事件会在页面开始加载后立即请求进行个性化。
* 页面完成加载时，页面事件底部会记录一次页面查看。

Adobe Analytics会忽略页面事件的顶部，这有助于更准确地记录量度，因为仅记录一次页面点击（页面事件的底部）。

您可以通过两种方式配置页面顶部和底部事件：直接调用Web SDK JavaScript库(`alloy()`)，或在Adobe Experience Platform标记UI中使用Web SDK标记扩展。 标记扩展的[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)操作包括一个“[!UICONTROL Use guided events]”选项，该选项为“[!UICONTROL Request personalization]”（页面顶部）和“[!UICONTROL Collect analytics]”（页面底部）方案预配置字段值。 以下每个示例都显示了这两个实施。

## 页面顶部事件 {#top-of-page}

以下示例配置请求个性化的页面顶部事件，但为自动呈现建议隐藏[显示事件](display-events.md)。 这些显示事件将改为随页面底部事件一起发送。

>[!BEGINTABS]

>[!TAB JavaScript库]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| 参数 | 必需/可选 | 描述 |
| --- | --- | --- |
| `type` | 必需 | 将此参数设置为`decisioning.propositionFetch`。 此特殊事件类型告知Adobe Analytics删除此事件。 在使用Customer Journey Analytics时，您还可以设置过滤器以删除这些事件。 有关详细信息，请参阅Adobe Analytics中的[Edge Network事件类型](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/hit-types)。 |
| `renderDecisions` | 必需 | 将此参数设置为`true`。 此参数可告知Web SDK呈现由Edge Network返回的决策。 |
| `personalization.sendDisplayEvent` | 必需 | 将此参数设置为`false`。 此参数可停止发送显示事件。 |

>[!TAB Web SDK标记扩展]

在页面顶部触发的规则中配置[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)操作。 启用&#x200B;**[!UICONTROL Use guided events]**，然后选择&#x200B;**[!UICONTROL Request personalization]**。 此选项将“[!UICONTROL Type]”锁定到“[!UICONTROL Decisioning Proposition Fetch]”，将“[!UICONTROL Render visual personalization decisions]”锁定到“已启用”，将“[!UICONTROL Automatically send a display event]”锁定到“已禁用”。

要改为手动设置这些字段，请将&#x200B;**[!UICONTROL Use guided events]**&#x200B;保留为禁用状态并自行配置每个字段。

>[!ENDTABS]

## 页面底部事件示例 {#bottom-of-page}

### 自动渲染的建议 {#bottom-auto-rendered}

以下示例配置页面底部事件，该事件发送在页面上自动呈现但在页面[事件的](#top-of-page)顶部禁止显示的主张的显示事件。

>[!BEGINTABS]

>[!TAB JavaScript库]

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| 参数 | 必需/可选 | 描述 |
| --- | --- | --- |
| `personalization.includeRenderedPropositions` | 必需 | 将此参数设置为`true`。 此参数允许发送在页面事件顶部禁止显示的显示事件。 |
| `xdm` | 可选 | 使用此对象可以包含您要用于页面底部事件的所有数据。 |

>[!TAB Web SDK标记扩展]

在页面底部触发的规则中配置[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)操作。 启用&#x200B;**[!UICONTROL Use guided events]**，然后选择&#x200B;**[!UICONTROL Collect analytics]**。 此选项将“[!UICONTROL Include rendered propositions]”锁定为启用。

要改为手动设置此字段，请将&#x200B;**[!UICONTROL Use guided events]**&#x200B;保留为禁用状态并直接启用&#x200B;**[!UICONTROL Include rendered propositions]**。 或者，使用承载页面数据的&#x200B;**[!UICONTROL XDM]** XDM对象[数据元素填充](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)字段。

>[!ENDTABS]

### 手动渲染的建议 {#bottom-manually-rendered}

以下示例配置页面底部事件，该事件为在页面上手动呈现的建议（即自定义决策范围或表面）发送显示事件。

>[!NOTE]
>
>在此方案中，页面底部事件必须等待页面顶部事件完成，以便可以呈现和记录建议。

>[!BEGINTABS]

>[!TAB JavaScript库]

```js
alloy("sendEvent", {
  xdm: { 
    ... // Optional bottom of page event data
    _experience: {
      decisioning: {
        propositions: propositions.map(function(p) {
          return {
            id: p.id,
            scope: p.scope,
            scopeDetails: p.scopeDetails
          };
        }),
        propositionEventType: {
          display: 1
        }
      }
    }
  }
});
```

| 参数 | 必需/可选 | 描述 |
| --- | --- | --- |
| `xdm._experience.decisioning.propositions` | 必需 | 此部分定义手动呈现的建议。 必须包括建议`id`、`scope`和`scopeDetails`。 有关详细信息，请参阅[管理显示事件](display-events.md)。 手动呈现的个性化内容必须包含在页面事件的底部。 |
| `xdm._experience.decisioning.propositionEventType` | 必需 | 将此参数设置为`display: 1`。 |
| `xdm` | 可选 | 使用此对象可以包含您要用于页面底部事件的所有数据。 |

>[!TAB Web SDK标记扩展]

“[!UICONTROL Use guided events]”选项未涵盖此方案，因此请手动配置操作：

1. 创建使用每个呈现建议的[、](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)和[填充](/help/tags/extensions/client/web-sdk/data-element-types.md#variable)并将`_experience.decisioning.propositions`设置为`id`的`scope`XDM对象`scopeDetails`（或`_experience.decisioning.propositionEventType.display`变量`1`）数据元素。 有关详细信息，请参阅[管理显示事件](display-events.md)。
1. 在页面规则底部的[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)操作中，将&#x200B;**[!UICONTROL Use guided events]**&#x200B;保留为禁用状态并引用&#x200B;**[!UICONTROL XDM]**&#x200B;字段中的数据元素。

>[!ENDTABS]

## 具有页面顶部和底部事件的单页应用程序 {#spa-example}

在单页应用程序中，必须在每次视图更改时指定视图名称，以便Web SDK在页面顶部呈现正确的个性化并在页面底部记录正确的视图。

### 第一页查看 {#spa-first-view}

在此示例中，`home`是初始页面加载时加载的视图。

>[!BEGINTABS]

>[!TAB JavaScript库]

顶级调用请求对`home`视图进行个性化，而不记录Analytics点击或触发显示事件。 底部调用记录页面查看并触发禁止显示的显示事件。 在两次调用中包含相同的`viewName`，以便一致地记录该视图。

```js
// Top of page, render decisions for the "home" view.
alloy("sendEvent", {
    type: "decisioning.propositionFetch",
    renderDecisions: true,
    personalization: {
        sendDisplayEvent: false
    },
    xdm: {
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});

// Bottom of page, send display events for the items that were rendered.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});
```

>[!TAB Web SDK标记扩展]

1. 创建将[设置为视图名称（例如，](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)）的`web.webPageDetails.viewName`XDM对象`home`数据元素。
1. 配置页面[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)顶部的操作：启用&#x200B;**[!UICONTROL Use guided events]**，选择&#x200B;**[!UICONTROL Request personalization]**，并在&#x200B;**[!UICONTROL XDM]**&#x200B;字段中引用数据元素。
1. 配置页面&#x200B;**[!UICONTROL Send event]**&#x200B;底部的操作：启用&#x200B;**[!UICONTROL Use guided events]**，选择&#x200B;**[!UICONTROL Collect analytics]**，并在&#x200B;**[!UICONTROL XDM]**&#x200B;字段中引用相同的数据元素，以便`viewName`在两个事件中都匹配。

>[!ENDTABS]

### 第二页视图 — 选项1 {#spa-second-view-option-1}

在本例中，单个事件便已足够，因为已获取页面的个性化设置。

>[!BEGINTABS]

>[!TAB JavaScript库]

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    ...,
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

>[!TAB Web SDK标记扩展]

1. 创建将[设置为新视图名称（例如，](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)）的`web.webPageDetails.viewName`XDM对象`cart`数据元素。
1. 在视图更改时，配置单个[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)操作：保留&#x200B;**[!UICONTROL Use guided events]**&#x200B;处于禁用状态，启用&#x200B;**[!UICONTROL Render visual personalization decisions]**，并在&#x200B;**[!UICONTROL XDM]**&#x200B;字段中引用数据元素。

>[!ENDTABS]

### 第二页视图 — 选项2 {#spa-second-view-option-2}

在需要延迟页面事件的底部时（例如，当页面的分析数据在视图更改时未准备就绪时），使用此方法。 分两步处理视图更改：

1. 在页面顶部，渲染已获取的建议，而不进行Edge Network调用。
1. 分析数据准备就绪后，发送页面底部事件。

在两次调用中包含相同的`viewName`，以便一致地记录该视图。

>[!BEGINTABS]

>[!TAB JavaScript库]

在页面顶部调用[`applyPropositions`](/help/collection/js/commands/applypropositions.md)以呈现新视图的缓存建议。 然后使用`sendEvent`调用页面底部的`includeRenderedPropositions: true`，以便触发禁止显示的显示事件。

```js
// Top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// Bottom of page, send display events for the items that were rendered.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
});
```

>[!TAB Web SDK标记扩展]

1. 创建将[设置为新视图名称（例如，](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)）的`web.webPageDetails.viewName`XDM对象`cart`数据元素。
1. 对于页面顶部事件，请配置[[!UICONTROL Apply propositions]](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md)操作并将&#x200B;**[!UICONTROL View name]**&#x200B;字段设置为视图的名称（例如，`cart`）。 此操作渲染已获取的建议，而不联系Edge Network。
1. 对于页面事件的底部，配置[[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md)操作：启用&#x200B;**[!UICONTROL Use guided events]**，选择&#x200B;**[!UICONTROL Collect analytics]**，并在&#x200B;**[!UICONTROL XDM]**&#x200B;字段中引用数据元素。

>[!ENDTABS]

## GitHub示例 {#github-sample}

合金示例存储库[中的](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom)top-and-bottom示例演示如何在页面顶部请求个性化并在底部发送分析量度。 下载示例并在本地运行该示例以了解页面顶部和底部事件的工作方式。 此示例直接使用JavaScript库；当您在Web SDK标记扩展中配置等效规则时，同样的模式同样适用。
