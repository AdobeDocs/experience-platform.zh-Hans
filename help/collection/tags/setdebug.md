---
title: setDebug()
description: 通过浏览器控制台在您的网站上启用调试。
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `setDebug()`

`_satellite.setDebug()`方法允许您在您的网站上启用或禁用[调试](../use-cases/debugging.md)。 此方法专门用于在浏览器控制台中本地运行；Adobe建议不要在标记规则中调用此方法。

```ts
_satellite.setDebug(enabled: boolean): void
```

* **`_satellite.setDebug(true);`**：启用[调试](../use-cases/debugging.md)。 标记库（包括[`_satellite.logger`](logger.md)）生成的消息在浏览器控制台中可见。
* **`_satellite.setDebug(false);`**：禁用调试。 标记库生成的控制台消息不可见。

```js
// This console message does not appear because debug mode is not yet enabled
_satellite.logger.log('Example message');

// Enable debug mode
_satellite.setDebug(true);

// This console message appears in the console
_satellite.logger.info('Debug messages are now visible');

// Disable debug mode
_satellite.setDebug(false);

// This console message does not appear because debug mode is no longer enabled
_satellite.logger.warn('Incorrect rule trigger detected');
```

>[!NOTE]
>
>使用JavaScript的本机`console.log()`编写的消息对DevTools打开的任何人都可见。 Adobe建议尽可能使用[`_satellite.logger`](logger.md)。

## 调试模式持久性

调用此方法时，调试模式使用以下范围：

* **浏览器会话**：调试模式在页面加载中持续存在。 在您结束浏览器会话或明确禁用它之前，它将保持启用状态。
* **原始范围**：调试模式仅对同一站点（域+端口+协议）持续存在。
* **每个浏览器配置文件**：调试模式不是跨配置文件模式。

[调试](../use-cases/debugging.md)的其他形式可能会影响调试模式并使用浏览器控制台方法覆盖调试模式。
