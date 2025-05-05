---
title: 单页应用程序实施
description: 了解如何在Adobe Journey Optimizer中实施SPA视图
exl-id: 1883251b-2d59-46d3-ac74-b8657edd0325
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# 实施单页应用程序(SPA) {#web-spa-implementation}

Adobe Experience Platform Web SDK提供了丰富的功能，使您的企业能够在下一代客户端技术(如单页应用程序(SPA))上实现个性化。

传统网站使用的是“页面到页面”导航模型，也称为多页面应用程序，其中网站设计与URL紧密耦合，并且从一个网页转换到另一个网页时，需要页面加载。

而现代Web应用程序(例如单页应用程序(SPA))采用的模型可以提高使用浏览器UI渲染的速度，这种渲染通常与页面重新加载无关。 这些体验可以通过客户交互触发，例如滚动、点击和光标移动。 随着现代Web范例的不断发展，传统的通用事件（如页面加载）与部署个性化和实验不再具有相关性。

![页面生命周期图表。](assets/web-spa-vs-traditional-lifecycle.png)

## 使用Web SDK for SPA的好处 {#web-spa-benefits}

以下是将Web SDK用于单页应用程序的一些好处：

* 能够在页面加载时缓存所有选件，将多次服务器调用减少至一次服务器调用。
* 由于选件是通过缓存立即显示的，不存在传统服务器调用引入的时间延迟，因此极大地提升了网站上的用户体验。
* 通过一次性开发人员设置，营销人员可以在SPA上通过Adobe Journey Optimizer Web可视化编辑器创建和运行个性化和试验活动。

## XDM视图和单页应用程序 {#web-spa-xdm}

Journey Optimizer Web编辑器利用了名为&#x200B;_视图_&#x200B;的概念。

视图是视觉元素的逻辑组，这些元素共同构成了SPA体验。 因此，单页应用程序可以被视为基于用户交互通过视图（而不是URL）进行转换。 视图通常可以表示整个网站、单个页面或页面中分组的可视化元素。

为了进一步说明视图是什么，以下示例使用了一个假定的在线电子商务网站。

* 导航到主页后，主页图像会宣传季节性系列以及网站上提供的不同产品目录。 在这种情况下，可以为整个主屏幕定义视图。 这种观点可以简单地称为“家”。

  ![显示主页的示例网站图像。](assets/web-spa-home.png)

* 随着客户对该企业销售的产品越来越感兴趣，他们决定单击&#x200B;**Men**&#x200B;链接。 与主页类似，可以将&#x200B;**Men**&#x200B;页面的整个定义为视图。 这个观点可以命名为“men”。

  ![显示特定视图的示例网站图像。](assets/web-spa-men.png)

* 由于视图可以定义为整个站点或站点上的一组可视化元素，因此产品站点上显示的四个产品可以分组并视为一个视图。 此视图可命名为“products”。

  ![显示特定视图的示例网站图像。](assets/web-spa-men-products.png)

* 当客户决定单击&#x200B;**ALL MEN&#39;S PRODUCTS**&#x200B;按钮以浏览站点上的更多产品时，在此情况下，网站URL不会更改，但可以在此处创建视图以仅表示显示的第二行产品。 视图名称可以是“products-page-2”。

* 客户决定从站点购买一些产品并进入结账屏幕。 购物车屏幕本身可以与名为“cart”的视图关联。 或者，您可以在签出屏幕内部使用不同的视图来处理以下推荐的产品。

  ![显示特定视图的示例网站图像。](assets/web-spa-cart.png)

视图的概念可以进一步扩展。 这些只是可以在网站上定义的视图的几个示例。

## 实施XDM视图 {#implement-xdm-views}

在Adobe Journey Optimizer中可利用XDM视图，使营销人员能够通过Journey Optimizer Web可视化编辑器在SPA上运行Web个性化和实验营销活动。

这需要执行以下步骤以完成一次性开发人员设置：

1. 安装[Adobe Experience Platform Web SDK](/help/web-sdk/install/overview.md)并检查[Web渠道先决条件](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/configure-web-channel/web-prerequisites.html?lang=zh-Hans)页面。

2. 确定单页应用程序中要个性化的所有XDM视图。

3. 在定义XDM视图后，为了向这些视图交付内容，您需要在单页应用程序中实施`sendEvent()`函数并将`renderDecisions`设置为`true`以及相应的XDM视图。 必须在`xdm.web.webPageDetails.viewName`中传递XDM视图。 此步骤允许营销人员在Journey Optimizer Web编辑器中发现这些视图，并为这些视图应用内容修改：

```js
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
>在第一个`sendEvent()`调用中，将获取并缓存所有应该呈现给最终用户的XDM视图。 将从缓存中读取后续的`sendEvent()`调用（已传入XDM视图），并在不进行服务器调用的情况下进行渲染。

## `sendEvent()`函数示例

本节概述了两个示例，说明如何在React中为假定的电子商务SPA调用`sendEvent()`函数。

### 示例1：A/B测试主页 {#web-spa-sample-1}

营销团队想要在整个主页上运行A/B测试。

![单页应用程序示例页面。](assets/web-spa-home.png)

要在整个主页网站上运行A/B测试，必须在将XDM `viewName`设置为`home`的情况下调用`sendEvent()`：

```js
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

### 示例2：个性化产品 {#web-spa-sample-2}

营销团队想要在用户单击查看所有Men产品后将价格标签颜色更改为红色，以对第二行产品进行个性化。

![包含个性化产品的单页应用程序示例页面。](assets/web-spa-men-products.png)

```js
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

            <
            button type = "button"
            onClick = {
                this.handleLoadMoreClicked
            } > All Men 's Products</button>
        );
    }

    handleLoadMoreClicked() {
        var page = this.state.page + 1; // assuming page number is derived from component's state
        this.setState({
            page: page
        });
        onViewChange('PRODUCTS-PAGE-' + page);
    }
}
```
