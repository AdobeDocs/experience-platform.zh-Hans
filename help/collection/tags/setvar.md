---
title: setVar()
description: 设置一个值，以便稍后使用getVar()检索该值。
source-git-commit: 54c32803136bf37a13bb9ca14b1d1c7b09a2041c
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# `setVar()`

`_satellite.setVar()`方法允许您设置一个或多个自定义名称/值对，这些名称/值对以后可由[`_satellite.getVar()`](getvar.md)引用。

```ts
// Set a single name/value pair
_satellite.setVar(name: string, value: unknown): void

// Set multiple name/value pairs at once
_satellite.setVar(vars: { [name: string]: unknown }): void;
```

>[!IMPORTANT]
>
>虽然`getVar()`方法可检索`setVar()`设置的数据元素和值，但这两个实体类型是分开的。 使用`setVar()`设置与标记UI中的数据元素同名的值不会覆盖它。

## 持久性和范围

`setVar()`值仅存在于页面内存中：

* **仅当前页面**：值会一直保留，直到页面卸载为止。 在单页应用程序中，它们将一直保留，直到完全重新加载或覆盖/清除它们。
* **没有浏览器存储**：没有写入Cookie、本地存储或会话存储。

## 引用使用`setVar()`设置的值

您可以使用`getVar()`检索自定义代码中的值：

```js
// Set a custom variable using setVar()
_satellite.setVar('Ad location','Banner advertisement');

// Returns the string 'Banner advertisement'
_satellite.getVar('Ad location');
```

您还可以在支持数据元素表示法的字段中的标记UI中引用这些变量：

```text
%Ad location%
```

>[!NOTE]
>
>如果使用`setVar()`的值集使用与数据元素相同的名称，并且您在数据元素表示法中引用了该名称，则数据元素优先。

## 示例

```js
// Set a single name/value pair
_satellite.setVar('product', 'Circuit Pro');

// Set multiple name/value pairs at once (same as calling setVar() three times)
_satellite.setVar({ 'title': 'Blinding Light', 'category': 'Game', 'genre': 'Tower defense' });

// Retrieve each value
_satellite.getVar('title'); // Blinding Light
_satellite.getVar('category'); // Game
_satellite.getVar('genre'); // Tower defense
```

>[!NOTE]
>
>使用此方法设置变量名称时，请避免使用句点(`.`)。 `getVar()`方法无法识别包含使用`setVar()`设置的句点的变量。 但是，`getVar()` _不_&#x200B;识别在标记UI中定义使用句点的数据元素。
