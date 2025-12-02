---
title: logger
description: 调试时将信息输出到浏览器控制台。
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---

# `logger`

`_satellite.logger`对象包含方法，允许您在启用[调试](../use-cases/debugging.md)时将诊断或信息性消息输出到浏览器控制台。 如果未启用调试，则所有`logger`方法调用将不执行任何操作。

这些方法允许开发人员、技术营销人员和测试人员轻松查看标记资产中的触发因素以及触发时间。 由于这些控制台消息仅在启用调试时显示，因此您可以在部署到生产环境时保留`logger`消息，而不会影响网站访客的浏览器控制台。

```ts
readonly _satellite.logger: {
  debug(...args: unknown[]): void;
  log(...args: unknown[]): void;
  info(...args: unknown[]): void;
  warn(...args: unknown[]): void;
  error(...args: unknown[]): void;
}
```

>[!TIP]
>
>标记对象的早期版本使用了`_satellite.notify()`。 `notify()`函数已弃用，推荐使用`_satellite.logger`。

## 方法

启用调试后，所有`_satellite.logger`方法都会传递到它们对应的JavaScript `console.*`方法。 使用`console`支持大多数`_satellite.logger`参数或对象：

| 方法 | 转发至 | 推荐的用法 |
|---|---|---|
| `_satellite.logger.debug()` | `console.debug()` | 详细诊断；某些浏览器可能需要详细日志记录才能查看。 |
| `_satellite.logger.log()` | `console.log()` | 常规消息。 |
| `_satellite.logger.info()` | `console.info()` | 高级别信息事件。 |
| `_satellite.logger.warn()` | `console.warn()` | 可恢复的问题。 控制台条目以黄色突出显示。 |
| `_satellite.logger.error()` | `console.error()` | 失败。 控制台条目以红色突出显示。 Adobe建议为栈栈使用`error`对象。 |

```js
// First enable debugging mode
_satellite.setDebug(true);

// Logs a debug message
_satellite.logger.debug('Verbose diagnostic event');

// Logs a generic message
_satellite.logger.log('Example');

// Logs an informational message with mixed arguments
_satellite.logger.info('Rule triggered', 42, { ruleId: 'R123' }, ['a', 'b']);

// Logs a warning message
_satellite.logger.warn('Data element does not contain a value');

// Logs an error message with stack
_satellite.logger.error(new Error('Required extension not found'));
```

## 控制台输出

该库在所有控制台输出消息前面加有以下内容：

* **🚀**：帮助您轻松检测哪些控制台消息源自您的标记实施。
* **\[Origin\]**：日志源自的规则、操作、扩展或数据元素名称。 如果在实施之外调用记录器方法（例如通过浏览器控制台），则使用`[Custom Script]`。
* **消息输出**：调用方法时包含消息输出。

>[!NOTE]
>
>未应用浏览器格式令牌，如`%c`、`%s`和`%d`，因为记录器应用了`🚀 [Origin]`前缀。
