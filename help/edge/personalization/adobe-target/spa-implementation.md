---
title: Adobe Experience Platform Web SDK的单页应用程序实施
description: 了解如何使用Adobe Target创建Adobe Experience Platform Web SDK的单页应用程序(SPA)实施。
keywords: 目标;adobe目标;xdm视图;视图；单页应用程序；SPA;SPA生命周期；客户端；AB测试；AB；体验定位；XT;VEC
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 12%

---


# 单页应用程序实现

Adobe Experience Platform Web SDK提供丰富的功能，使您的企业能够使用单页应用程序(SPA)等下一代客户端技术进行个性化。

传统网站使用的是“页面到页面”导航模型，也称为多页应用程序，其中网站设计与 URL 紧密耦合，并且从一个网页转换到另一个网页时，需要页面加载。

现代的Web应用程序（如单页应用程序）已采用一种模型，该模型可推动浏览器UI渲染的快速使用，这通常与页面重新加载无关。 客户互动（如滚动、点击和光标移动）可触发这些体验。 随着现代Web的范式的发展，传统通用事件（如页面加载）与部署个性化和实验的相关性不再有效。

![](assets/spa-vs-traditional-lifecycle.png)

## Platform Web SDK for SPA的优势

以下是将Adobe Experience Platform Web SDK用于单页应用程序的一些优势：

* 能够在页面加载时缓存所有选件，将多次服务器调用减少至一次服务器调用。
* 大大改善了您网站上的用户体验，因为优惠会通过缓存立即显示，而不会因传统服务器调用引入延迟时间。
* 只需编写一行代码并设置一次性开发人员，营销人员就可以在SPA上通过Visual Experience Composer(VEC)创建并运行A/B和体验定位(XT)活动。

## XDM视图和单页应用程序

Adobe Target VEC for SPA利用了一个称为“视图”的概念：组成SPA体验的视觉元素的逻辑组。 因此，单页应用程序可被视为基于用户交互通过视图而不是URL进行转换。 “视图”通常可显示整个站点或某个站点中分组的可视化元素。

要进一步解释哪些视图，以下示例使用React中实现的假想在线电子商务网站来浏览示例视图。

导航到主网站后，主角图像将宣传复活节的销售以及该网站上提供的最新产品。 在这种情况下，可以为整个主屏幕定义视图。 这种视图可以简单地称为&quot;家&quot;。

![](assets/example-views.png)

随着客户对公司销售的产品更感兴趣，他们决定单击&#x200B;**产品**&#x200B;链接。 与主页网站类似，可将整个产品站点定义为一个“视图”。此视图可命名为“全部产品”。

![](assets/example-products-all.png)

由于视图可以定义为整个站点或站点上的一组可视元素，因此产品站点上显示的四个产品可以分组并视为视图。 此视图可命名为“产品”。

![](assets/example-products.png)

当客户决定单击&#x200B;**加载更多**&#x200B;按钮浏览网站上的更多产品时，网站URL在这种情况下不会更改，但可以在此处创建视图，仅表示显示的第二行产品。 视图名称可以是“products-page-2”。

![](assets/example-load-more.png)

客户决定从该站点购买几款产品，然后继续到结帐屏幕。 在结帐站点上，客户可以选择普通投放或快速投放。 视图可以是站点上的任意可视元素组，因此可以为投放首选项创建视图并称为“投放首选项”。

![](assets/example-check-out.png)

视图的概念可以进一步扩展。 这些只是可在网站上定义的视图的几个示例。

## 实施XDM视图

可以在Adobe Target中利用XDM视图，使营销人员能通过Visual Experience Composer在SPA上运行A/B和XT测试。 这需要执行以下步骤才能完成一次性开发人员设置：

1. 安装[Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md)
2. 确定您希望个性化的单页应用程序中的所有XDM视图。
3. 定义XDM视图后，为了传递AB或XT VEC活动，请在“单页应用程序”中实现`renderDecisions`且设置为`true`的`sendEvent()`函数和相应的XDM视图。 必须在`xdm.web.webPageDetails.viewName`中传递XDM视图。 通过此步骤，营销人员可以利用Visual Experience Composer为这些XDM启动A/B和XT测试。

   ```javascript
   alloy("sendEvent", { 
     "renderDecisions": true, 
     "xdm": { 
       "web": { 
         "webPageDetails": { 
         "viewName":"home" 
         }
       } 
     } 
   });
   ```

>[!NOTE]
>
>在第一次`sendEvent()`调用中，将读取并缓存应呈现给最终用户的所有XDM视图。 随后通过传入的XDM视图进行的`sendEvent()`调用将从缓存中读取，并在不进行服务器调用的情况下呈现。

## `sendEvent()` 函数示例

本节概述三个示例，说明如何为假想的电子商务SPA调用React中的`sendEvent()`函数。

### 示例1:A/B测试主页

营销团队希望对整个主页运行A/B测试。

![](assets/use-case-1.png)

要在整个主站点上运行A/B测试，必须在将XDM `viewName`设置为`home`时调用`sendEvent()`:

```jsx
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
        } 
      } 
    }
  }); 
} 

// react router v4 

const history = syncHistoryWithStore(createBrowserHistory(), store); 

history.listen(onViewChange); 

// react router v3 

<Router history={hashHistory} onUpdate={onViewChange} > 
```

### 示例2:个性化产品

营销团队希望在用户单击&#x200B;**加载更多**&#x200B;后，将价格标签颜色更改为红色，从而个性化第二行产品。

![](assets/use-case-2.png)

```jsx
function onViewChange(viewName) { 

  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName
        }
      } 
    } 
  }); 
} 

class Products extends Component { 
  
  render() { 
    return ( 
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component’s state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### 示例3:A/B测试投放首选项

营销团队希望运行A/B测试，以查看在选择&#x200B;**快速投放**&#x200B;时将按钮的颜色从蓝色更改为红色是否可以提升转换(与使两个投放选项的按钮颜色保持为蓝色相反)。

![](assets/use-case-3.png)

要根据选择的投放首选项对站点上的内容进行个性化，可为每个投放首选项创建一个视图。 选择&#x200B;**普通投放**&#x200B;时，视图可命名为“checkout-normal”。 如果选择了&#x200B;**快速投放**，则视图可命名为“checkout-express”。

```jsx
function onViewChange(viewName) { 
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName 
        }
      }
    }
  }); 
} 

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## 对SPA使用Visual Experience Composer

当您定义完XDM视图并使用传入的XDM视图实现`sendEvent()`后，VEC将能够检测这些视图并允许用户为A/B或XT活动创建操作和修改。

>[!NOTE]
>
>要为SPA使用VEC，必须安装并激活[Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/)或[Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC帮助程序扩展。

### “修改”面板

“修改”面板捕获为特定视图创建的操作。 视图的所有操作都按该视图进行分组。

![](assets/modifications-panel.png)

### 操作

单击某个操作会突出显示将应用此操作的网站上的元素。在视图下创建的每个VEC操作都有以下图标：**信息**、**编辑**、**克隆**、**移动**&#x200B;和&#x200B;**删除**。 下表中将更详细地介绍这些图标。

![](assets/action-icons.png)

| 图标 | 描述 |
|---|---|
| 信息 | 显示操作的详细信息。 |
| Edit | 允许您直接编辑操作的属性。 |
| 克隆 | 将操作克隆到位于“修改”面板上的一个或多个视图，或者您在 VEC 中浏览并导航到的一个或多个视图。该操作不一定存在于“修改”面板中。<br/><br/>**注意：** 执行克隆操作后，必须通过浏览导航到VEC中的视图，以查看克隆操作是否为有效操作。如果该操作未应用到视图，您将看到一个错误。 |
| 移动 | 将操作移动到“页面加载事件”或修改面板中已存在的任何其他视图。<br/><br/>**页面加载事件:** 与页面加载事件对应的任何操作都会应用于Web应用程序的初始页面加载。<br/><br/>**注意**：执行移动操作后，必须通过浏览导航到VEC中的视图，以查看移动是否是有效操作。如果该操作未应用到视图，您将看到一个错误。 |
| Delete | 删除操作。 |

## 将VEC用于SPA示例

本节概述了使用Visual Experience Composer为A/B或XT活动创建操作和修改的三个示例。

### 示例1:更新“主”视图

在本文档的早期，为整个主站点定义了一个名为“home”的视图。 现在，营销团队希望通过以下方式更新“主页”视图:

* 将&#x200B;**添加到Cart**&#x200B;和&#x200B;**类似按钮更改为蓝色的较浅份额。**&#x200B;在页面加载期间应发生这种情况，因为这涉及到更改标题的组件。
* 将“**2019**&#x200B;最新产品”标签更改为“2019 **最热门产品”，并将文本颜色更改为紫色。**

要在VEC中进行这些更新，请选择&#x200B;**合成**&#x200B;并将这些更改应用到“home”视图。

![](assets/vec-home.png)

### 示例2:更改产品标签

对于“products-page-2”视图，营销团队希望将&#x200B;**Price**&#x200B;标签更改为&#x200B;**销售价格**，并将标签颜色更改为红色。

要在VEC中进行这些更新，需要执行以下步骤：

1. 在VEC中选择&#x200B;**浏览**。
2. 在站点的顶部导航中选择&#x200B;**产品**。
3. 选择&#x200B;**加载更多**&#x200B;一次以视图第二行产品。
4. 在VEC中选择&#x200B;**合成**。
5. 应用操作，将文本标签更改为&#x200B;**销售价格**，将颜色更改为红色。

![](assets/vec-products-page-2.png)

### 示例3:个性化投放首选项样式

视图可以按粒度定义，如状态或单选按钮中的选项。 早期在本文档视图中为投放首选项、“checkout-normal”和“checkout-express”定义。 营销团队希望将“checkout-express”视图的按钮颜色更改为红色。

要在VEC中进行这些更新，需要执行以下步骤：

1. 在VEC中选择&#x200B;**浏览**。
2. 将产品添加到网站上的购物车。
3. 选择站点右上角的购物车图标。
4. 选择&#x200B;**结帐**。
5. 在&#x200B;**投放首选项**&#x200B;下选择&#x200B;**快速投放**&#x200B;单选按钮。
6. 在VEC中选择&#x200B;**合成**。
7. 将&#x200B;**付费**&#x200B;按钮颜色更改为红色。

>[!NOTE]
>
>在选择&#x200B;**Express 投放**&#x200B;单选按钮之前，“checkout-express”视图不会显示在“修改”面板中。 这是因为在选择&#x200B;**Express 投放**&#x200B;单选按钮时执行`sendEvent()`函数，因此，在选择单选按钮之前，VEC不知道“checkout-express”视图。

![](assets/vec-delivery-preference.png)
