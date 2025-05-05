---
title: 在Web SDK中配置页面顶部和底部事件
description: 本文介绍了如何在Web SDK中使用页面顶部和底部事件。
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 4d0895c6ad38523f5527c9630931c3c0b8ef83c0
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 1%

---


# 在Web SDK中配置页面顶部和底部事件

当您希望向客户提供个性化体验时，网页的加载时间至关重要。

为了优化加载时间并尽快提供个性化，Web SDK支持配置页面事件的顶部和底部。

页面事件的顶部和底部描述了一种方法，该方法以异步方式加载页面中的各种元素，同时保持页面加载时间最短。

此配置可将用户加载个性化内容之前必须等待的时间减至最少。

在量度准确性方面，Adobe Analytics可以忽略页面事件的顶部，因为仅记录一次页面点击（页面事件的底部），因此可以更准确地记录量度。

## 用例 {#use-cases}

一家体育服装零售商希望为其购物者提供个性化体验，同时最大限度地减少用户访问其网站时的摩擦，同时能够准确收集访客量度。

通过使用Web SDK中的页面顶部事件和页面底部事件，营销团队能够以最佳方式配置其个性化投放：

* Web SDK会发送个性化请求，该请求会在页面开始加载后立即加载。 这是页面顶部事件。
* 当页面完成加载时，将记录一个页面查看事件。 在页面加载过程的稍后阶段，将发生这种情况。 这是页面底部事件。

## 页面顶部事件示例 {#top-of-page}

以下代码示例展示了页面顶部事件配置，该配置请求个性化但未[为自动呈现的建议](../personalization/display-events.md#send-sendEvent-calls)发送显示事件。 [显示事件](../personalization/display-events.md#send-sendEvent-calls)将作为页面底部事件的一部分发送。

>[!BEGINTABS]

>[!TAB 页面顶部事件]

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
|---|---|---|
| `type` | 必需 | 将此参数设置为`decisioning.propositionFetch`。 此特殊事件类型告知Adobe Analytics删除此事件。 使用Customer Journey Analytics时，您还可以设置过滤器以删除这些事件。 |
| `renderDecisions` | 必需 | 将此参数设置为`true`。 此参数可告知Web SDK呈现由Edge Network返回的决策。 |
| `personalization.sendDisplayEvent` | 必需 | 将此参数设置为`false`。 这将停止发送显示事件。 |

>[!ENDTABS]

## 页面底部事件示例 {#bottom-of-page}

>[!BEGINTABS]

>[!TAB 自动呈现的建议]

以下代码示例展示了页面底部事件配置，该配置为自动在页面上呈现，但在页面[&#128279;](#top-of-page)事件的顶部禁止显示的主张发送显示事件。

>[!NOTE]
>
>在此方案中，必须调用页面顶部的页面底部事件&#x200B;_after_。 但是，页面底部事件不需要等待第一页顶部完成。

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| 参数 | 必需/可选 | 描述 |
|---|---|---|
| `personalization.includeRenderedPropositions` | 必需 | 将此参数设置为`true`。 这将允许发送在页面事件顶部禁止显示的显示事件。 |
| `xdm` | 可选 | 使用此部分可包含页面底部事件所需的所有数据。 |

>[!TAB 手动呈现建议]

以下代码示例展示了页面底部事件配置，该配置为在页面上手动呈现的建议（即，对于自定义决策范围或表面）发送显示事件。

>[!NOTE]
>
>在此方案中，页面底部事件必须等到页面顶部事件完成后才能呈现建议并记录页面底部事件。

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
|---|---|---|
| `xdm._experience.decisioning.propositions` | 必需 | 此部分定义手动呈现的建议。 必须包括建议`ID`、`scope`和`scopeDetails`。 请参阅有关如何[手动渲染个性化](../personalization/rendering-personalization-content.md#manually)的文档，以了解有关如何记录手动渲染内容的显示事件的更多信息。 手动呈现的个性化内容必须包含在页面点击的底部。 |
| `xdm._experience.decisioning.propositionEventType` | 必需 | 将此参数设置为`display: 1`。 |
| `xdm` | 可选 | 使用此部分可包含页面底部事件所需的所有数据。 |

>[!ENDTABS]


## 具有顶部和底部页面点击量的单页应用程序 {#spa-example}


>[!BEGINTABS]

>[!TAB 第一页查看次数]

以下示例包括所需`xdm.web.webPageDetails.viewName`参数的相加。 这就是它成为单页应用程序的原因。 此示例中的`viewName`是页面加载时加载的视图。

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
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.

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

>[!TAB 第二次页面查看（选项1）]

在此示例中，无需执行页面拆分的顶部/底部，因为已获取页面的个性化设置。

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


>[!TAB 第二次页面查看（选项2）]

如果您仍需要延迟页面点击的底部，则可以使用`applyPropositions`作为页面点击的顶部。 由于无需获取任何个性化设置且无需记录Analytics数据，因此无需向Edge Network发出请求。

```js
// top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// bottom of page, send display events for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.
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

>[!ENDTABS]

## GitHub示例 {#github-sample}

在[此地址](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom)找到的示例演示了如何使用Experience Platform和Web SDK在页面顶部请求个性化，并在底部发送分析指标。 您可以下载示例并在本地运行它以了解页面顶部和底部事件的工作原理。
