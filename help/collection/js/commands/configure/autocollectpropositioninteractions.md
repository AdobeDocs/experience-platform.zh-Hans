---
title: autoCollectPropositionInteractions
description: 在单击链接时自动收集数据。
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# `autoCollectPropositionInteractions`

`autoCollectPropositionInteractions`属性是一个可选设置，用于确定Web SDK是否自动收集建议交互。 该值是一个决策提供程序的映射，其中每个提供程序都具有指示应如何处理自动建议交互的值。

启用自动建议交互跟踪后，呈现给DOM的建议元素中的任何点击都将由Web SDK自动收集。 此收藏集包括通过Web SDK自动呈现到DOM的任何体验以及使用[`applyPropositions`](../applypropositions.md)命令呈现到DOM的体验。

如果在配置Web SDK时省略此属性，则默认设置为`{"AJO": "always", "TGT": "never"}`。 如果您不希望自动跟踪建议交互，请将值设置为`{"AJO": "never", "TGT": "never"}`。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "autoCollectPropositionInteractions": {
    "AJO": "always",
    "TGT": "never"
  }
});
```

此对象中支持的属性包括：

| 属性 | 描述 |
| --- | --- |
| **`AJO`** | Adobe Journey Optimizer。 |
| **`TGT`** | Adobe Target。 |

每个属性的可能值包括：

| 值 | 描述 |
| --- | --- |
| **`always`** | 始终自动收集与建议关联的任何元素的`interact`事件。 |
| **`never`** | 从不自动收集与建议关联的元素的`interact`事件。 |
| **`decoratedElementsOnly`** | 如果元素包含指定标签或令牌的数据属性，则自动收集与建议关联的元素的`interact`事件。 |

## 数据属性 {#data-attributes}

您可以使用元素上的数据属性来添加交互的特定性。

| 名称 | 数据属性 | 描述 |
| --- | --- | --- |
| **[!UICONTROL Label]** | `data-aep-click-label` | 如果点击的元素上存在label数据属性，则该属性将包含在发送到Edge Network的交互详细信息中。 Web SDK会查找以单击元素并向DOM树上走开的label数据属性。 Web SDK使用它找到的第一个标签。 |
| **[!UICONTROL Token]** | `data-aep-click-token` | 在[Adobe Journey Optimizer基于代码的营销活动](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/code-based-experience/get-started-code-based)中利用决策策略时，请使用此令牌。 您可以使用令牌区分点击了哪个决策策略项目。 当点击的元素上存在令牌数据属性时，它会包含在发送到Edge Network的交互详细信息中。 Web SDK会查找以单击元素并向DOM树上走开始的令牌数据属性。 Web SDK使用它找到的第一个令牌。 |
| **[!UICONTROL Interact ID]** | `data-aep-interact-id` | 呈现建议时，Web SDK会自动将此唯一ID添加到容器元素。 Web SDK使用此ID将DOM元素与建议关联。 由于这是Web SDK所需的ID，因此您不应以任何方式对其进行更改。 您可以放心地忽略它。 |

## 示例

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/alpha.jpg" class="poster" />
    <h2>Example Movie Alpha</h2>
    <p class="description"> A lighthearted story about exploration and friendship set on a distant world. Follow a curious rover who discovers that small actions can lead to big changes.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Alpha">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/bravo.jpg" class="poster" />
    <h2>Example Movie Bravo</h2>
    <p class="description">An uplifting tale of a determined chef who overcomes unlikely odds to create culinary masterpieces in a bustling city bistro.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Bravo">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/charlie.jpg" class="poster" />
    <h2>Example Movie Charlie</h2>
    <p class="description">A vibrant adventure following a young musician who journeys into a fantastical realm to find the true meaning of family and tradition.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Charlie">View details</button>
    </p>
  </div>
</div>
```

### 将`autoCollectPropositionInteractions`与`applyPropositions`命令一起使用 {#apply-propositions}

[`applyPropositions`](../applypropositions.md)命令是一种将建议呈现到DOM的便捷方法。 但是，对于基于JSON的代码营销活动，您可以使用此命令将现有DOM元素（或您的应用程序代码根据JSON值呈现到屏幕的元素）与建议关联。

此关联将为该元素激活自动交互跟踪，并为该元素分配适当的建议。 要实现此目的，请将`actionType`设置为`track`。

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://example.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://example.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## 为Web SDK标记扩展配置自动建议交互

配置Web SDK标记扩展时，以下两个下拉菜单是此对象的等效标记：

* [[!UICONTROL Auto click collection for Adobe Journey Optimizer]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-journey-optimizer)
* [[!UICONTROL Auto click collection for Adobe Target]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-target)
