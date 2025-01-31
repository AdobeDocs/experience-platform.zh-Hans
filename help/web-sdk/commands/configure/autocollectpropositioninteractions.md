---
title: autoCollectPropositionInteractions
description: 了解如何配置Experience PlatformWeb SDK以自动收集链接数据。
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: 55c656e7fd08e98b75c20f0688a6697baf533291
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# `autoCollectPropositionInteractions`

`autoCollectPropositionInteractions`属性是一个可选设置，用于确定Web SDK是否应自动收集建议交互。

该值是一个决策提供程序的映射，其中每个提供程序都具有指示应如何处理自动建议交互的值。

## 支持的值 {#supported-values}

默认情况下，自动建议交互是&#x200B;_始终_&#x200B;为Adobe Journey Optimizer (`AJO`)收集的，以及&#x200B;_从不_&#x200B;为Adobe Target (`TGT`)收集的。

默认值`autoTrackPropositionInteractions`显示如下。

```json
{
  "AJO": "always",
  "TGT": "never"
}
```

有关每个决策提供程序支持的配置值，请参阅下表。

| 值 | 描述 |
| --- | --- |
| `always` | [!DNL Web SDK]将始终自动收集与建议关联的任何元素的`interact`事件。 |
| `never` | [!DNL Web SDK]永远不会自动收集与建议关联的元素的`interact`事件。 |
| `decoratedElementsOnly` | [!DNL Web SDK]将自动收集与建议关联的元素的`interact`事件，但前提是元素包含指定标签或令牌的数据属性。 |

## 自动建议交互跟踪 {#logic}

启用自动建议交互跟踪时，[!DNL Web SDK]将自动收集呈现给DOM的建议元素中的任何点击。 这包括由[!DNL Web SDK]自动渲染到DOM的任何体验以及使用[`applyPropositions`](../applypropositions.md)命令渲染到DOM的体验。

### 数据属性 {#data-attributes}

您可以使用元素上的数据属性来添加交互的特定性。

| 名称 | 数据属性 | 描述 |
| --- | --- | --- |
| [!DNL Label] | `data-aep-click-label` | 当点击的元素上存在标签数据属性时，它将包含在发送到[!DNL Edge Network]的交互详细信息中。 [!DNL Web SDK]查找以单击元素并向DOM树上走开的label数据属性。 [!DNL Web SDK]使用它找到的第一个标签。 |
| [!DNL Token] | `data-aep-click-token` | 在[Adobe Journey Optimizer基于代码的营销活动](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based)中利用决策策略时，请使用此令牌。 您可以使用令牌区分点击了哪个决策策略项目。 当点击的元素上存在令牌数据属性时，它会包含在发送到Edge Network的交互详细信息中。 [!DNL Web SDK]查找以单击元素并向DOM树上走开开头的令牌数据属性。 [!DNL Web SDK]使用它找到的第一个令牌。 |
| [!DNL Interact ID] | `data-aep-interact-id` | 在呈现建议时，[!DNL Web SDK]会自动将此唯一ID添加到容器元素。 Web SDK使用此ID将[!DNL DOM]元素与建议关联。 由于这是[!DNL Web SDK]所需的ID，因此您不应以任何方式更改它。 您可以放心地忽略它。 |

**示例**

请参阅下面的代码片段以查看使用数据属性的示例。

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/walle.jpg" class="poster" />
    <h2>WALL·E</h2>
    <p class="description"> In a distant, but not so unrealistic, future where mankind has abandoned earth because it has become covered with trash from products sold by the powerful multi-national Buy N Large corporation, WALL-E, a garbage collecting robot has been left to clean up the mess. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-WALL·E"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/ratatouille.jpg" class="poster" />
    <h2>Ratatouille</h2>
    <p class="description"> A rat named Remy dreams of becoming a great French chef despite his family's wishes and the obvious problem of being a rat in a decidedly rodent-phobic profession. When fate places Remy in the sewers of Paris, he finds himself ideally situated beneath a restaurant made famous by his culinary hero, Auguste Gusteau. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Ratatouille"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/coco.jpg" class="poster" />
    <h2>Coco</h2>
    <p class="description"> Despite his family's baffling generations-old ban on music, Miguel dreams of becoming an accomplished musician like his idol, Ernesto de la Cruz. Desperate to prove his talent, Miguel finds himself in the stunning and colorful Land of the Dead following a mysterious chain of events. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Coco"> View details >> </button>
    </p>
  </div>
</div>
```

### `applyPropositions`命令 {#apply-propositions}

请参阅[`applyPropositions`](../applypropositions.md)文档以了解此命令的工作方式。

`applyPropositions`命令是一种向[!DNL DOM]呈现建议的便捷方式。 但是，在具有`JSON`的基于代码的营销活动中，您可以使用此命令将现有[!DNL DOM]元素（或您的应用程序代码基于`JSON`值呈现到屏幕的元素）与建议关联。

此关联将为该元素激活自动交互跟踪，并为该元素分配适当的建议。 要实现此目的，请将`actionType`设置为`track`。

**示例**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://mywebsite.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://mywebsite.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## 通过Web SDK标记扩展启用自动建议和交互点击跟踪 {#tag-extension}

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**数据收集** > **标记**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**扩展**，然后在Adobe Experience Platform Web SDK卡片中选择&#x200B;**配置**。
1. 向下滚动到&#x200B;**[!UICONTROL 数据收集]**&#x200B;部分，然后选中复选框&#x200B;**启用建议和交互链接跟踪**。
1. 选择&#x200B;**保存**，然后发布更改。

## 通过Web SDK JavaScript库启用自动建议和交互链接跟踪 {#library}

在[!DNL Web SDK]中默认启用建议跟踪。 但是，您可以在运行[`configure`](../configure/overview.md)命令时使用`autoCollectPropositionInteractions`值进一步配置它。

如果在配置Web SDK时省略此属性，则默认设置为`{"AJO": "always", "TGT": "never"}`。 如果您不希望自动跟踪建议交互，请将值设置为`{"AJO": "never", "TGT": "never"}`。

```javascript
alloy("configure", {
   "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
   "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
   "autoCollectPropositionInteractions": {"AJO": "always", "TGT": "never"}
});
```
