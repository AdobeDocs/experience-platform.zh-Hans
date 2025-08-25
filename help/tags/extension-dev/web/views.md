---
title: Web扩展中的视图
description: 了解如何在Adobe Experience Platform Web扩展中为库模块定义视图。
exl-id: 4471df3e-75e2-4257-84c0-dd7b708be417
source-git-commit: 1bfa2e27e554dc899efc8a32900a926e787a58ac
workflow-type: tm+mt
source-wordcount: '2148'
ht-degree: 70%

---

# Web扩展中的视图

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

每个事件、条件、操作或数据元素类型可以提供允许用户提供设置的视图。扩展还可以具有顶级[扩展配置视图](../configuration.md)，通过该视图，用户可以为整个扩展提供全局设置。在所有类型的视图中，视图的构建过程都是相同的。

## 包含文档类型

确保在 HTML 文件中包含 `doctype` 标记。通常，这意味着 HTML 文件使用以下内容开头：

```xml
<!DOCTYPE html>
```

## 包含标记iframe脚本

在视图的HTML中包含标记iframe脚本：

```html
<script src="https://assets.adobedtm.com/activation/reactor/extensionbridge/extensionbridge.min.js"></script>
```

此脚本提供了一个通信API，以允许视图与标记应用程序进行通信。

## 在扩展桥接通信 API 中注册

加载iframe脚本后，您需要为标记提供一些方法，以便用于通信。 调用 `window.extensionBridge.register` 并向其传递一个对象，如下所示：

```js
window.extensionBridge.register({
  init: function(info) {
    // Populate view with info.settings which will exist if the user is editing something
    // that was previously saved.
    if (info.settings) {
      document.getElementById('name').value = info.settings.name;
    }
  },
  validate: function() {
    // Return whether the view is valid.
    return document.getElementById('name').value.length > 0;
  },
  getSettings: function() {
    // Return user-provided settings.
    return {
      name: document.getElementById('name').value
    };
  }
});
```

每个方法的内容都需要进行修改，以适应您的特定视图要求。

### [!DNL init]

将视图加载到iframe后，标记将立即调用`init`方法。 它将传递一个参数 (`info`)，该参数必须是包含以下属性的对象：

| 属性 | 描述 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `settings` | 包含先前从此视图保存的设置的对象。如果 `settings` 为 `null`，则表示用户正在创建初始设置，而不是加载已保存的版本。如果 `settings` 是一个对象，则应该使用它来填充视图，因为用户正在选择编辑以前保留的设置。 |
| `extensionSettings` | 从扩展配置视图保存的设置。在非扩展配置视图中访问扩展设置时，这可能很有用。如果当前视图是扩展配置视图，请使用`settings`。 |
| `propertySettings` | 包含属性设置的对象。有关此对象中所包含内容的详细信息，请参阅 [turbine 对象指南](../turbine.md#property-settings)。 |
| `tokens` | 包含 API 令牌的对象。要从视图内访问 Adobe API，您通常需要使用 `tokens.imsAccess` 下的 IMS 令牌。此令牌将仅可用于Adobe开发的扩展。 如果您是Adobe员工(代表Adobe创作的扩展)，请[向数据收集工程团队发送电子邮件](mailto:reactor@adobe.com)，并提供扩展的名称，以便我们可以将其添加到允许列表中。 |
| `company` | 包含`orgId` (您的24字符Adobe Experience Cloud ID)、`id` （贵公司在Reactor API中的唯一标识符）和`tenantId` (Adobe Identity Management System中组织的唯一标识符)的对象。 |
| `schema` | [JSON 架构](https://json-schema.org/)格式中的对象。此对象将来自[扩展清单](../manifest.md)，并且可能有助于验证您的表单。 |
| `apiEndpoints` | 包含`reactor`的对象，其中包含对Reactor API的网址的引用。 |
| `userConsentPermissions` | 一个对象，其中包含来自Adobe [产品使用情况数据](https://experienceleague.adobe.com/en/docs/core-services/interface/features/account-preferences#product-usage-data)的同意标志。 使用存储在`globalDataCollectionAndUsage`标记中的以了解是否允许您的扩展收集&#x200B;*any*&#x200B;客户数据。 |
| `preferredLanguages` | 语言字符串的数组。 |

您的视图应使用此信息来呈现和管理其表单。您可能只需要处理 `info.settings`，但其他信息会在必要时提供。

>[!IMPORTANT]
>
>要使扩展符合GDPR要求，请确保使用`userConsentPermissions.globalDataCollectionAndUsage`标志来确定是否允许扩展收集有关用户的数据。

### [!DNL validate]

用户点击“保存”按钮后，将调用`validate`方法。 它应返回以下任一值：

* 一个布尔值，指示用户的输入是否有效。
* 一个稍后使用布尔值（指示用户的输入是否有效）解析的 promise。

作为扩展开发人员，您可以自行决定构成有效输入的内容，因为库模块将基于该输入执行操作。

如果用户的输入无效，请在视图中显示一些说明输入无效的指示，以便用户知晓需要更正的内容。

### [!DNL getSettings]

用户点击“保存”按钮且验证视图后，将调用`getSettings`方法。 该函数应返回以下任一值：

* 一个对象，包含基于用户输入的设置。
* 一个稍后使用包含基于用户输入的设置的对象解析的 promise。

此设置对象稍后将在标记运行时库中发出。 该对象的内容由您自行决定。该对象必须可序列化为 JSON 并从 JSON 反序列化。函数或[正则表达式](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp)实例等值不符合这些条件，因此不允许使用。

## 利用共享视图

`window.extensionBridge`对象具有多种方法，可让您利用通过标记提供的现有视图，这样您就不必在自己的视图中重现它们。 可用的方法如下：

### [!DNL openCodeEditor]

```js
window.extensionBridge.openCodeEditor().then(function(code) { 
  console.log(code);
});
```

调用此方法将显示允许用户编辑代码片段的模态。当用户编辑完代码后，将会使用更新后的代码来解析 promise。如果用户在没有选择保存更改的情况下关闭代码编辑器，则 promise 将永远不会得到解析。`options` 对象的结构应如下所示：

| 属性 | 描述 |
| --- | --- |
| `code` | 应在编辑器中显示的代码。通常在用户编辑现有代码时提供。如果未提供，则代码编辑器在打开时将为空。 |
| `language` | 将要编辑的代码的语言。有效选项为 `javascript`、`html`、`css`、`json` 和 `plaintext`。如果未提供，则假定为 `javascript`。 |

### [!DNL openRegexTester]

```js
window.extensionBridge.openRegexTester().then(function(pattern) { 
  console.log(pattern);
});
```

调用此方法将显示允许用户测试和修改正则表达式模式的模态。当用户编辑完正则表达式后，将会使用更新后的正则表达式模式来解析 promise。如果用户在没有选择保存更改的情况下关闭正则表达式测试器，则 promise 将永远不会得到解析。`options` 对象应包含以下属性：

| 属性 | 描述 |
| --- | --- |
| `pattern` | 应该用作测试器中模式字段初始值的正则表达式模式。通常在用户编辑现有正则表达式时提供。如果未提供，则模式字段最初将为空。 |
| `flags` | 测试器应使用的正则表达式标志。例如，`gi` 将指示全局匹配标志和忽略大小写标志。用户不能在测试器中修改这些标志，但这些标志可用于演示扩展在执行正则表达式时将使用的特定标志。如果未提供，测试器将不使用任何标记。有关正则表达式标志的更多信息，请参阅 [MDN 的正则表达式文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp)。<br><br>一种常见的情况是，扩展允许用户切换正则表达式的“区分大小写”选项。为了支持此功能，扩展通常会在其扩展视图内提供一个复选框，如果选中此复选框，则将启用不区分大小写（由`i`标志表示）。 该视图保存的设置对象将需要表示该复选框是否已选中，这样执行正则表达式的库模块就可以知道是否使用 `i` 标志。此外，当扩展视图希望打开正则表达式测试器时，如果选中了“不区分大小写”复选框，则需要传递`i`标志。 这允许用户在启用了不区分大小写的情况下正确测试正则表达式。 |

### [!DNL openDataElementSelector] {#open-data-element}

```js
window.extensionBridge.openDataElementSelector().then(function(dataElement) { 
  console.log(dataElement);
});
```

调用此方法将显示允许用户选择数据元素的模态。当用户选择完数据元素后，将使用选定数据元素的名称解析 promise（默认情况下，该名称将用百分比符号括起来）。如果用户在没有选择保存更改的情况下关闭元素选择器，则 promise 将永远不会得到解析。

`options`对象应包含单个布尔属性`tokenize`。 此属性指示在解析 promise 之前是否应将选定数据元素的名称用百分比符号括起来。请参阅[支持数据元素](#supporting-data-elements)一节，了解这种属性有用的原因。此选项默认为 `true`。

## 支持的数据元素 {#supporting-data-elements}

您的视图可能包含用户希望在其中利用数据元素的表单字段。 例如，如果视图有一个用户应在其中输入产品名称的文本字段，那么用户在该字段中键入硬编码值可能没有任何意义。 相反，他们可能希望字段的值是动态的（在运行时确定），并且可以通过使用数据元素来实现这一点。

例如，假设我们正在构建一个扩展，它会发送信标以跟踪转化。我们还假设信标所发送的其中一段数据是产品名称。在允许用户配置信标的扩展视图中，很可能包含一个用于输入产品名称的文本字段。 Experience Platform用户键入静态产品名称（例如“Calzone Oven XL”）通常没有多大意义，因为产品名称可能取决于从中发送信标的页面。 对于数据元素来说，这是一个极好的用例。

如果用户希望将名为 `productname` 的数据元素用作产品名称值，则可以键入数据元素的名称，并在名称两侧加上百分比符号 (`%productname%`)。我们将使用百分比符号括起来的数据元素名称称为“数据元素令牌”。 Experience Platform用户通常熟悉此构造。 您的扩展反过来会将数据元素令牌保存在其导出的 `settings` 对象中。然后，您的设置对象可能如下所示：

```js
{
  productName: '%productname%'
}
```

在运行时，在将设置对象传递到库模块之前，将扫描设置对象并将任何数据元素令牌替换为其各自的值。 如果在运行时，`productname`数据元素的值为`Ceiling Medallion Pro 2000`，则将传递到库模块的设置对象可能如下所示：

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

为了指示用户在何处使用数据元素可能会有所帮助，并且方便用户输入数据元素，我们强烈建议在此类字段旁边添加图标按钮，如下所示：

![数据元素字段](../images/data-element-field.png)

>[!NOTE]
>
>要下载相应的图标，请导航到Adobe Spectrum[上的](https://spectrum.adobe.com/page/icons/)图标页面并搜索“[!DNL Data]”。

当用户选择文本字段旁边的按钮时，将调用 `window.extensionBridge.openDataElementSelector`，[如上所述](#open-data-element)。这会显示用户可以从中进行选择的数据元素列表，而不是强制用户记住数据元素名称并键入百分比符号。用户选择数据元素后，您将收到用百分比符号括起来的选定数据元素的名称（除非您已将 `tokenize` 选项设置为 `false`）。我们建议您随后使用该结果填充文本字段。

### 替换数据元素令牌

如前所述，如果一个保留的设置对象包含以下内容：

```js
{
  productName: '%productname%'
}
```

并且在运行时，`productname` 数据元素的值是 `Ceiling Medallion Pro 2000`，那么将传递到库模块的设置对象可能如下所示：

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

每当遇到的设置对象中的值“仅”__&#x200B;由百分比符号、字符串、百分比符号组成时，它就会被数据元素值取代，_而无需更改数据元素值的类型_。

例如，如果在运行时 `productname` 的值改为数字 `538`（而不是字符串），则传递到库模块的设置对象将如下所示：

```js
{
  productName: 538
}
```

请注意，生成的 `538` 在这里是一个数字，而不是字符串。同样，如果在运行时数据元素值是一个函数（一种罕见但可能存在的用例），则生成的设置对象将如下所示：

```js
{
  productName: function() { … }
}
```

另一方面，我们假设保留的设置对象如下：

```js
{
  productName: '%productname% - %modelnumber%'
}
```

在这种情况下，由于 `productName` 的值不只是一个数据元素令牌，因此结果将始终为字符串。每个数据元素令牌在转换为字符串后将替换为其各自的值。如果在运行时，`productname`的值为`Ceiling Medallion Pro` （字符串），`modelnumber`为`2000` （数字），则传递到库模块的生成设置对象将为：

```js
{
  productName: 'Ceiling Medallion Pro - 2000'
}
```

## 避免导航

扩展视图与包含的数据收集用户界面之间的通信取决于扩展视图内未发生导航。 因此，请避免向扩展视图添加任何会使用户离开扩展视图 HTML 页面的内容。例如，如果在扩展视图中提供了一个链接，请确保该链接会打开一个新的浏览器窗口（通常通过将 `target="_blank"` 添加到锚点标记来实现）。如果选择在扩展视图中使用 `form` 元素，请确保永远不会提交表单。如果表单中有一个 `button` 元素，但未能向其添加 `type="button"`，则可能会意外提交表单。在扩展视图内提交表单会导致 HTML 文档刷新，从而造成用户体验受损。
