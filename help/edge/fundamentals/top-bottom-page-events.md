---
title: 使用页面顶部和底部事件
description: 本文介绍了如何在Web SDK中使用页面顶部和底部事件。
source-git-commit: 5cd77f78c9617a16f6ee59a7c029dfffac7740e9
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 2%

---


# 在Web SDK中使用页面顶部和底部事件

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

以下代码示例展示了页面顶部事件配置，该配置请求个性化，但不会为自动呈现的建议发送显示通知。 显示通知将作为页面底部事件的一部分发送。

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

| 参数 | 必填/可选 | 描述 |
|---|---|---|
| `type` | 必需 | 将此参数设置为 `decisioning.propositionFetch`. 此特殊事件类型告知Adobe Analytics删除此事件。 使用Customer Journey Analytics时，您还可以设置过滤器以删除这些事件。 |
| `renderDecisions` | 必需 | 将此参数设置为 `true`. 此参数可告知Web SDK呈现边缘网络返回的决策。 |
| `personalization.sendDisplayEvent` | 必需 | 将此参数设置为 `false`. 这将停止发送显示通知。 |

>[!ENDTABS]

## 页面底部事件示例 {#bottom-of-page}

>[!BEGINTABS]

>[!TAB 自动渲染的建议]

以下代码示例展示了页面事件配置的底部，该配置发送建议显示通知，这些建议在页面上自动呈现，但在中已禁止显示通知 [页面顶部](#top-of-page) 事件。

>[!NOTE]
>
>在此方案中，必须调用页面底部事件 _之后_ 第一页顶部。 但是，页面底部事件不需要等待第一页顶部完成。

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| 参数 | 必填/可选 | 描述 |
|---|---|---|
| `personalization.includeRenderedPropositions` | 必需 | 将此参数设置为 `true`. 这将启用显示通知的发送，该通知在页面事件顶部被禁止。 |
| `xdm` | 可选 | 使用此部分可包含页面底部事件所需的所有数据。 |

>[!TAB 手动渲染的建议]

以下代码示例展示了页面底部事件配置，该配置为在页面上手动呈现的建议（即，对于自定义决策范围或表面）发送显示通知。

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



| 参数 | 必填/可选 | 描述 |
|---|---|---|
| `xdm._experience.decisioning.propositions` | 必需 | 此部分定义手动呈现的建议。 您必须包含建议 `ID`， `scope`、和 `scopeDetails`. 请参阅有关如何执行操作的文档 [手动渲染个性化](../personalization/rendering-personalization-content.md#manually) 有关如何记录手动呈现内容的显示通知的更多信息。 手动呈现的个性化内容必须包含在页面点击的底部。 |
| `xdm._experience.decisioning.propositionEventType` | 必需 | 将此参数设置为 `display: 1`. |
| `xdm` | 可选 | 使用此部分可包含页面底部事件所需的所有数据。 |

>[!ENDTABS]


## 具有顶部和底部页面点击量的单页应用程序 {#spa-example}


>[!BEGINTABS]

>[!TAB 第一页查看]

以下示例包括添加所需的 `xdm.web.webPageDetails.viewName` 参数。 这就是它成为单页应用程序的原因。 此 `viewName` 在此示例中，是在页面加载时加载的视图。

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

// Bottom of page, send display notifications for the items that were rendered.
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

如果您仍需要延迟页面点击的底部，则可以使用 `applyPropositions` ，表示页面点击的顶部。 由于无需获取个性化设置且无需记录Analytics数据，因此无需向Edge Network发出请求。

```js
// top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// bottom of page, send display notifications for the items that were rendered.
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
