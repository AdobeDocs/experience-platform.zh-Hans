---
title: Web擴充功能的事件型別
description: 瞭解如何在Adobe Experience Platform中為Web擴充功能定義事件型別程式庫模組。
exl-id: dbdd1c88-5c54-46be-9824-2f15cce3d160
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 30%

---

# Web擴充功能的事件型別

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

在標籤規則中，事件是指為了讓規則觸發而必須發生的活動。 例如，網頁擴充功能可提供「手勢」事件型別，用來監視特定滑鼠或觸控手勢的發生。 一旦该手势发生，事件逻辑就会触发规则。

事件型別程式庫模組的設計用途是偵測活動是否發生，然後呼叫函式以觸發相關規則。 偵測到的事件是可自訂的。 例如，可以偵測使用者何時做出特定手勢、快速捲動或互動某物。

本文介紹如何在Adobe Experience Platform中定義Web擴充功能的事件型別。

>[!NOTE]
>
>本檔案假設您熟悉程式庫模組，以及如何將這些模組整合在Web擴充功能中。 在返回到本指南之前，请参阅关于[库模块格式](./format.md)的概述，以了解实施概况。

事件型別由擴充功能定義，通常包含下列專案：

1. A [檢視](./views.md) 顯示在Experience PlatformUI和資料收集UI中，可讓使用者修改事件的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用於解譯設定並監視特定活動的發生。

`module.exports` 同時接受 `settings` 和 `trigger` 引數。 如此可讓您自訂事件型別。

```js
module.exports = function(settings, trigger) { … };
```

| 参数 | 描述 |
| --- | --- |
| `settings` | 一个对象，其中包含用户在事件类型视图中配置的任何设置。您对此对象中的内容拥有最终控制权。 |
| `trigger` | 每当应该触发规则时，模块应调用的函数。彼此之間有一對一的關係 `settings` 物件， a `trigger` 函式與規則。 這表示您針對一個規則收到的觸發程式函式，無法用來引發另一個規則。 |

>[!NOTE]
>
>对于每个已配置为使用您的事件类型的规则，都将调用一次导出函数。

以經過5秒的活動為例，經過5秒後，活動已發生並將觸發規則。 模組看起來會類似於此範例。

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

如果您想讓Adobe Experience Platform使用者能夠設定持續時間，則需要輸入持續時間並儲存至設定物件的選項。 该对象可能如下所示：

```js
{
  "duration": 25000
}
```

若要運用於使用者定義的持續時間，需要更新模組以包含此項。

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## 傳遞內容事件資料

觸發規則時，就發生的事件提供其他詳細資訊通常有其效用。 创建规则的用户会发现，该信息对于实现特定行为非常有用。例如，如果行銷人員想要建立每當使用者滑動畫面時就會傳送分析信標的規則。 擴充功能必須提供 `swipe` 事件型別，讓行銷人員可以使用此事件型別來觸發適當的規則。 假設行銷人員想要納入指標上發生撥動時的角度，這很難在不提供其他資訊的情況下完成。 要提供有关所发生事件的更多信息，请在调用 `trigger` 函数时传递一个对象。例如：

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

接下来，营销人员可通过在文本字段中指定值 `%event.swipeAngle%`，在分析信标中使用该值。另外，他们也可以从其他上下文（例如，自定义代码操作）中访问 `event.swipeAngle`。也有可能包含其他型別的選擇性事件資訊，這些資訊可能以相同的方式對行銷人員很有用。

### [!DNL nativeEvent]

如果您的事件型別以原生事件為基礎(例如，如果您的擴充功能提供 `click` 事件型別)，建議設定 `nativeEvent` 屬性，如下所示。

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

这对于尝试从本机事件中访问任何信息（例如，光标的坐标位置）的营销人员会非常有用。

### [!DNL element]

如果元素與發生的事件之間有強烈的關係，建議設定 `element` 屬性至元素的DOM節點。 例如，如果您的擴充功能提供 `click` 事件型別且您允許行銷人員加以設定，唯有當ID為的元素時才會觸發規則 `herobanner` 「 」已選取。 在此情況下，如果使用者選取主圖橫幅，建議呼叫 `trigger` 並設定 `element` 至主圖橫幅的DOM節點。

```js
trigger({
  element: element // the value would be the DOM node
});
```

## 遵守规则顺序

標籤讓使用者能夠排序規則。 例如，使用者可建立兩個規則，這兩個規則都使用orientation-change事件型別，並自訂規則引發的順序。 假設Adobe Experience Platform使用者指定的順序值為 `2` 規則A中的方向變更事件和順序值 `1` 規則B中的方向變更事件。這表示當行動裝置上的方向變更時，規則B應在規則A之前引發（具有低階值的規則會先引發）。

如前所述，对于每个已配置为使用我们的事件类型的规则，将调用一次我们事件模块中的导出函数。每次调用导出函数时，都会传递一个与特定规则绑定的唯一 `trigger` 函数。在剛才說明的案例中，匯出的函式將會使用呼叫一次 `trigger` 繫結至規則B的函式，然後使用 `trigger` 繫結至規則A的函式。規則B會先出現，因為使用者為其指定的順序值比規則A低。當程式庫模組偵測到方向變更時，請務必呼叫 `trigger` 函式會依照提供給程式庫模組的相同順序執行。

在下面的示例代码中，请注意当检测到方向更改时，将按照提供给导出函数的相同顺序来调用 trigger 函数：

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  triggers.forEach(function(trigger) {
    trigger();
  });
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

这可以确保遵守用户指定的顺序。

如果实施不当，则会导致以不同的顺序调用 trigger 函数：

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  for (var i = triggers.length - 1; i >= 0; i--) {
    triggers[i]();
  }
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

通常，自然的编程惯例可遵守正确的顺序，但是务必要了解其影响并相应地进行开发。
