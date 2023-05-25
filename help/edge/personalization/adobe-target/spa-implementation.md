---
title: 适用于Adobe Experience Platform Web SDK的单页应用程序实施
description: 了解如何使用Adobe Target创建Adobe Experience Platform Web SDK的单页应用程序(SPA)实施。
keywords: target；adobe target；xdm视图；视图；单页应用程序；SPA；SPA生命周期；客户端；AB测试；AB；体验定位；XT；VEC
exl-id: cc48c375-36b9-433e-b45f-60e6c6ea4883
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 13%

---

# 单页应用程序实施

Adobe Experience Platform Web SDK提供了丰富的功能，使您的企业能够在下一代客户端技术(如单页应用程序(SPA))上实现个性化。

传统网站使用的是“页面到页面”导航模型，也称为多页应用程序，其中网站设计与 URL 紧密耦合，并且从一个网页转换到另一个网页时，需要页面加载。

现代Web应用程序（例如单页应用程序）采用的模型促进了浏览器UI渲染的快速使用，这种渲染通常与页面重新加载无关。 这些体验可以通过客户交互触发，例如滚动、点击和光标移动。 随着现代Web范例的不断发展，传统通用事件（如页面加载）与部署个性化和实验不再具有相关性。

![](assets/spa-vs-traditional-lifecycle.png)

## Platform Web SDK for SPA的好处

以下是为单页应用程序使用Adobe Experience Platform Web SDK的一些好处：

* 能够在页面加载时缓存所有选件，将多次服务器调用减少至一次服务器调用。
* 由于选件是通过缓存立即显示的，不存在传统服务器调用引入的时间延迟，因此极大地改善了网站上的用户体验。
* 通过一行代码和一次性开发人员设置，营销人员可以在您的SPA上通过可视化体验编辑器(VEC)创建和运行A/B和体验定位(XT)活动。

## XDM视图和单页应用程序

Adobe Target VEC for SPA利用了称为“视图”的概念，即视觉元素的逻辑组合，这些元素共同构成了SPA体验。 因此，单页应用程序可以视为基于用户交互通过视图（而不是URL）进行过渡。 “视图”通常可显示整个站点或某个站点中分组的可视化元素。

为了进一步说明视图是什么，以下示例使用在React中实施的假想在线电子商务网站来探索示例视图。

导航到主页后，主页图像会宣传复活节促销活动以及网站上提供的最新产品。 在这种情况下，可以为整个主屏幕定义一个视图。 此视图可以简单地称为“home”。

![](assets/example-views.png)

随着客户对该企业销售的产品越来越感兴趣，他们决定单击 **产品** 链接。 与主页网站类似，可将整个产品站点定义为一个“视图”。此视图可命名为“products-all”。

![](assets/example-products-all.png)

由于视图可以定义为整个站点或站点上的一组可视化元素，因此产品站点上显示的四个产品可以分组并视为视图。 此视图可命名为“products”。

![](assets/example-products.png)

当客户决定单击 **加载更多** 按钮浏览网站上的更多产品，在这种情况下，网站URL不会更改，但可以在此处创建视图，以仅表示显示的第二行产品。 视图名称可以是“products-page-2”。

![](assets/example-load-more.png)

客户决定从站点购买一些产品并进入结账屏幕。 在结帐站点上，客户可以选择正常交货或快速交货。 视图可以是网站上的任意一组可视化元素，因此可以为投放首选项创建一个视图，并将其称为“投放首选项”。

![](assets/example-check-out.png)

视图的概念可以进一步扩展。 这些只是可以在网站上定义的视图的几个示例。

## 实施XDM视图

在Adobe Target中可利用XDM视图，以使营销人员能够通过可视化体验编辑器在SPA上运行A/B和XT测试。 这需要执行以下步骤，以完成一次性开发人员设置：

1. 安装 [Adobe Experience Platform Web SDK](../../fundamentals/installing-the-sdk.md)
2. 确定单页应用程序中要个性化的所有XDM视图。
3. 定义XDM视图后，为了交付AB或XT VEC活动，请实施 `sendEvent()` 函数为 `renderDecisions` 设置为 `true` 以及单页应用程序中相应的XDM视图。 必须传入XDM视图 `xdm.web.webPageDetails.viewName`. 此步骤允许营销人员利用可视化体验编辑器为这些XDM启动A/B和XT测试。

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
>在第一个 `sendEvent()` 调用，将获取并缓存应呈现给最终用户的所有XDM视图。 后续 `sendEvent()` 将从缓存中读取具有传入的XDM视图的调用，并在不进行服务器调用的情况下进行渲染。

## `sendEvent()` 函数示例

本节概述了三个示例，说明如何调用 `sendEvent()` 函数位于React中，适用于假定的电子商务SPA。

### 示例1：A/B测试主页

营销团队想要在整个主页上运行A/B测试。

![](assets/use-case-1.png)

在整个主站点上运行A/B测试， `sendEvent()` 必须通过XDM调用 `viewName` 设置为 `home`：

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

### 示例2：个性化产品

营销团队想要在用户单击后将价格标签颜色更改为红色，以对第二行产品进行个性化 **加载更多**.

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

### 示例3：A/B测试投放首选项

营销团队想要运行A/B测试，以查看按钮的颜色在下列情况下是否从蓝色更改为红色 **快递** 选中可以提高转化率（与使两个交付选项的按钮颜色保持蓝色不同）。

![](assets/use-case-3.png)

要根据所选的投放首选项对网站上的内容进行个性化，可以为每个投放首选项创建一个视图。 时间 **正常投放** 选中时，可以将视图命名为“checkout-normal”。 如果 **快递** 选中时，可以将视图命名为“checkout-express”。

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

## 使用SPA的可视化体验编辑器

当您完成定义XDM视图并实施时 `sendEvent()` 通过传入这些XDM视图，VEC将能够检测到这些视图，并允许用户为A/B或XT活动创建操作和修改。

>[!NOTE]
>
>要将VEC用于SPA，您必须安装并激活 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 或 [铬黄](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC助手扩展。

### “修改”面板

“修改”面板可捕获为特定视图创建的操作。 视图的所有操作都分组在该视图下。

![](assets/modifications-panel.png)

### 操作

单击某个操作会突出显示将应用此操作的网站上的元素。在视图下创建的每个VEC操作都具有以下图标： **信息**， **编辑**， **克隆**， **移动**、和 **删除**. 下表将对这些图标进行更详细的说明。

![](assets/action-icons.png)

| 图标 | 描述 |
|---|---|
| 信息 | 显示操作的详细信息。 |
| Edit | 允许您直接编辑操作的属性。 |
| 克隆 | 将操作克隆到位于“修改”面板上的一个或多个视图，或者您在 VEC 中浏览并导航到的一个或多个视图。该操作不一定存在于“修改”面板中。<br/><br/>**注意：** 完成克隆操作后，必须通过“浏览”导航到VEC中的视图，以查看克隆操作是否有效。 如果该操作未应用到视图，您将看到一个错误。 |
| 移动 | 将操作移动到“页面加载事件”或修改面板中已存在的任何其他视图。<br/><br/>**页面加载事件：** 与页面加载事件对应的任何操作会应用于Web应用程序的初始页面加载。 <br/><br/>**注意：** 完成移动操作后，必须通过“浏览”导航到VEC中的视图，以查看移动操作是否有效。 如果该操作未应用到视图，您将看到一个错误。 |
| Delete | 删除操作。 |

## 将VEC用于SPA示例

此部分概述了三个使用可视化体验编辑器为A/B或XT活动创建操作和修改的示例。

### 示例1：更新“home”视图

在本文档的前面，为整个home站点定义了一个名为“home”的视图。 现在，营销团队希望通过以下方式更新“主页”视图：

* 更改 **添加到购物车** 和 **点赞** 按钮变浅为蓝色。 这应在页面加载期间发生，因为它涉及更改标头的组件。
* 更改 **2019年最新产品** 标签到 **2019年最畅销产品** 并将文本颜色更改为紫色。

要在VEC中进行这些更新，请选择 **撰写** 并将这些更改应用于“主页”视图。

![](assets/vec-home.png)

### 示例2：更改产品标签

对于“products-page-2”视图，营销团队想要更改 **价格** 标签到 **售价** 并将标签颜色更改为红色。

要在VEC中进行这些更新，需要执行以下步骤：

1. 选择 **浏览** 在VEC中。
2. 选择 **产品** 在站点的顶部导航中。
3. 选择 **加载更多** 一次，以查看产品的第二行。
4. 选择 **撰写** 在VEC中。
5. 应用操作以将文本标签更改为 **售价** 颜色变成红色。

![](assets/vec-products-page-2.png)

### 示例3：个性化投放偏好设置样式

可以在粒度级别定义视图，例如单选按钮中的状态或选项。 本文档前面为投放首选项“checkout-normal”和“checkout-express”定义了视图。 营销团队想要将“checkout-express”视图的按钮颜色更改为红色。

要在VEC中进行这些更新，需要执行以下步骤：

1. 选择 **浏览** 在VEC中。
2. 将产品添加到网站上的购物车。
3. 选择网站右上角的购物车图标。
4. 选择 **结帐订单**.
5. 选择 **快递** 下的单选按钮 **投放首选项**.
6. 选择 **撰写** 在VEC中。
7. 更改 **支付** 按钮颜色变为红色。

>[!NOTE]
>
>“checkout-express”视图在 **快递** 单选按钮处于选中状态。 这是因为 `sendEvent()` 函数执行时间 **快递** 单选按钮处于选中状态，因此，在选择单选按钮之前，VEC不会看到“checkout-express”视图。

![](assets/vec-delivery-preference.png)
