---
title: 卫星对象引用
description: 了解客户端_satellite对象以及可在标记中使用该对象执行的各种功能。
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 05bf3a8c92aa221af153b4ce9949f0fdfc3c86ab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# `_satellite`对象引用

_这些页面概述了如何使用`_satellite`对象，该对象允许您使用JavaScript管理和自定义标记逻辑。 有关如何在数据收集UI中设置实施的详细信息，请参阅[Adobe Experience Platform Web SDK标记扩展](/help/tags/extensions/client/web-sdk/overview.md)。_

`_satellite`对象公开了多个受支持的入口点，可帮助您与网站上发布的标记库交互。 如果正确实施加载程序标记，则所有标记部署都会公开`_satellite`。 此对象有几个主要用例：

* 在自定义代码块中使用标记库，授予您对标记库本身的完全访问权限。
* 在任何环境（开发、暂存或生产）中调试已部署的实施
* 直接在您的网站上实施，使您能够完全控制事件或标记规则触发的时间。 对于新的实施，Adobe建议使用更灵活的策略，如[Adobe客户端数据层](/help/tags/extensions/client/client-data-layer/overview.md)。

>[!IMPORTANT]
>
>如果您从网站代码（例如，`_satellite`）中调用`_satellite.track()`，请&#x200B;**保护每次调用**，以便网站不会与标记库紧密耦合。
>
>在标记属性的自定义代码中使用`_satellite`或在浏览器控制台中本地使用，不需要小心。

## 常见用法示例

```js
// Read and write a temporary data element value (guarded)
if(window._satellite?.getVar && window._satellite?.setVar) {
  const region = _satellite.getVar('user_region');
  _satellite.setVar('promo_code', code);
}

// Manually trigger a rule configured in your tag property (guarded)
if (window._satellite?.track) {
  _satellite.track('cart_add', { sku: '123', qty: 2 });
}

// Local console debugging (guarding not needed)
_satellite.setDebug(true);
_satellite.logger.log('Rule evaluated');
```
