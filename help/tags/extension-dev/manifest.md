---
title: 扩展清单
description: 了解如何配置JSON清单文件，以告知Adobe Experience Platform如何正确使用您的扩展。
exl-id: 7cac020b-3cfd-4a0a-a2d1-edee1be125d0
source-git-commit: a7c66b9172421510510b6acf3466334c33cdaa3d
workflow-type: tm+mt
source-wordcount: '2652'
ht-degree: 66%

---

# 扩展清单

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../term-updates.md)。

在扩展的基目录中，必须创建一个名为 `extension.json` 的文件。其中包含有关扩展的重要详细信息，借助这些信息，Adobe Experience Platform可以正确使用扩展。 其中的部分内容采用 [npm 的 `package.json`](https://docs.npmjs.com/files/package.json) 方式构成。

[Hello World 扩展](https://github.com/adobe/reactor-helloworld-extension/blob/master/extension.json) GitHub 存储库中提供了 `extension.json` 示例。

扩展清单必须包含以下属性：

| 属性 | 描述 |
|--------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | 扩展的名称。它必须唯一，不同于所有其他扩展，且必须符合[命名规则](#naming-rules)。 **标记将此项用作标识符，在发布扩展后不应更改此项。** |
| `platform` | 用于此扩展的平台。目前唯一接受的值是 `web`。 |
| `version` | 此扩展的版本。必须遵循 [semver](https://semver.org/) 版本控制格式。与 [npm 版本字段](https://docs.npmjs.com/files/package.json#version)规则相一致。 |
| `displayName` | 用户可读的扩展名称。将显示给Experience Platform用户。 无需提及“标记”或“扩展”；用户已经知道他们正在查看标记扩展。 |
| `description` | 有关扩展的描述。将显示给Experience Platform用户。 如果您的扩展使用户能够在其网站上实施您的产品，请说明产品的功能。无需提及“标记”或“扩展”；用户已经知道他们正在查看标记扩展。 |
| `iconPath`*（可选）* | 将为扩展显示的图标的相对路径。 不应以斜杠开头。必须引用一个扩展名为 `.svg` 的 SVG 文件。SVG应为正方形，并且可以由Experience Platform进行缩放。 |
| `author` | “author”是一个对象，其结构应如下所示： <ul><li>`name`：扩展的作者姓名。或者，也可以在此使用公司名称。</li><li>`url`*（可选）*：一个 URL，可以从中了解有关扩展作者的更多信息。</li><li>`email`*（可选）*：扩展作者的电子邮件地址。</li></ul>与 [npm 作者字段](https://docs.npmjs.com/files/package.json#people-fields-author-contributors)规则相一致。 |
| `releaseNotesUrl`*（可选）* | 扩展发行说明的URL（如果您有发布此信息的位置）。 此URL将在Adobe Tags UI中使用，以在扩展安装和升级期间显示此链接。 只有Web扩展和Edge扩展支持此属性。 |
| `exchangeUrl`*（公共扩展的必需属性）* | 指向 Adobe Exchange 上列出的扩展的 URL。必须匹配以下模式：`https://www.adobeexchange.com/experiencecloud.details.######.html`。 |
| `viewBasePath` | 包含您的所有视图及视图相关资源（HTML、JavaScript、CSS、图像）的子目录的相对路径。Experience Platform将在Web服务器上托管此目录，并从中加载iframe内容。 这是必填字段，且不应以斜杠开头。例如，如果您的所有视图都包含在 `src/view/` 中，则 `viewBasePath` 的值为 `src/view/`。 |
| `hostedLibFiles`*（可选）* | 我们的许多用户喜欢将所有与标记相关的文件托管在自己的服务器上。 这可以提高用户在运行时对文件可用性的确定级别，而且用户可以轻松扫描代码以发现安全漏洞。如果扩展的库部分需要在运行时加载 JavaScript 文件，则建议使用此属性来列出这些文件。列出的文件将与标记运行时库一起托管。 随后，您的扩展将可以通过使用 [getHostedLibFileUrl](./turbine.md#get-hosted-lib-file) 方法检索到的 URL 来加载文件。<br><br>此选项包含一个数组，其中含有需托管的第三方库文件的相对路径。 |
| `main`*（可选）* | 运行时应执行的库模块的相对路径。<br><br>此模块将始终包含在运行时库中并得以执行。由于此模块始终包含在运行时库中，因此建议仅在绝对有必要的情况下才使用“main”模块，并保持其代码大小最小。<br><br>我们并不保证会首先执行此模块，其他模块有可能会在其之前执行。 |
| `configuration`*（可选）* | 此字段描述扩展的[扩展配置](./configuration.md)部分。如果要求用户提供扩展的全局设置，则需要使用此字段。有关应当如何构建此字段的详细信息，请参阅[附录](#config-object)。 |
| `events`*（可选）* | [事件](./web/event-types.md)类型定义的数组。请参阅附录中的[类型定义](#type-definitions)部分，以了解数组中每个对象的结构。 |
| `conditions`*（可选）* | [条件](./web/condition-types.md)类型定义的数组。请参阅附录中的[类型定义](#type-definitions)部分，以了解数组中每个对象的结构。 |
| `actions`*（可选）* | [操作](./web/action-types.md)类型定义的数组。请参阅附录中的[类型定义](#type-definitions)部分，以了解数组中每个对象的结构。 |
| `dataElements`*（可选）* | [数据元素](./web/data-element-types.md)类型定义的数组。请参阅附录中的[类型定义](#type-definitions)部分，以了解数组中每个对象的结构。 |
| `sharedModules`*（可选）* | 共享模块定义对象的数组。数组中的每个共享模块对象应当具有以下结构： <ul><li>`name`：共享模块的名称。请注意，当从其他扩展引用共享模块时，将使用此名称，如[共享模块](./web/shared.md)中所述。此名称从不显示在任何用户界面中。此名称应当唯一，不同于扩展中其他共享模块的名称，且必须符合[命名规则](#naming-rules)。**标记将此项用作标识符，在发布扩展后不应更改此项。**</li><li>`libPath`：共享模块的相对路径。不应以斜杠开头。必须引用一个扩展名为 `.js` 的 JavaScript 文件。</li></ul> |

## 附录

### 命名规则 {#naming-rules}

`extension.json` 中任意 `name` 字段的值必须符合以下规则：

* 不得超过 214 个字符
* 不得以点或下划线开头
* 不能包含大写字母
* 只能包含 URL 安全字符

与 [npm 包名称](https://docs.npmjs.com/files/package.json#name)规则相一致。

### 配置对象属性 {#config-object}

配置对象应当具有以下结构：

<table>
  <thead>
    <tr>
      <th>属性</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>viewPath</code></td>
      <td>扩展配置视图的相对 URL。应当相对于 <code>viewBasePath</code>，且不应以斜杠开头。必须引用一个扩展名为 <code>.html</code> 的 HTML 文件。可接受查询字符串和片段标识符（哈希）后缀。</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td><a href="https://json-schema.org/">JSON 架构</a>的对象，用来描述从扩展配置视图中保存的有效对象的格式。由于您是配置视图的开发者，因此您有责任确保所有保存的设置对象都与此架构匹配。当用户尝试使用Experience Platform服务保存数据时，此架构还将用于验证。<br><br>架构对象的示例如下所示：
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      我们建议使用诸如 <a href="https://www.jsonschemavalidator.net/">JSON 架构验证器</a>之类的工具，手动测试您的架构。</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>（可选）</em></td>
      <td>一个对象数组，其中的每个对象表示当每个相应的设置对象发出到运行时库时所应执行的转换。有关为何需要转换以及如何使用转换的更多信息，请参阅<a href="#transforms">转换</a>部分。</td>
    </tr>
  </tbody>
</table>

### 类型定义 {#type-definitions}

类型定义是用于描述事件、条件、操作或数据元素类型的对象。该对象包含以下属性：

<table>
  <thead>
    <tr>
      <th>属性</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>name</code></td>
      <td>类型的名称。此名称必须是扩展中的唯一名称。此名称必须符合<a href="#naming-rules">命名规则</a>。<strong>标记将此项用作标识符，在发布扩展后不应更改此项。</strong></td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>用于表示数据收集用户界面中的类型的文本。 该文本应当可供用户读取。</td>
    </tr>
    <tr>
      <td><code>categoryName</code> <em>（可选）</em></td>
      <td>提供该属性后，<code>displayName</code>将列在UI中的<code>categoryName</code>下。 所有具有相同 <code>categoryName</code> 的类型都将列在同一类别下。例如，如果您的扩展提供了 <code>keyUp</code> 事件类型和 <code>keyDown</code> 事件类型，并且它们都具有 <code>categoryName</code> <code>Keyboard</code>，那么当用户在构建规则时从可用事件类型列表中进行选择时，这两个事件类型都会列在 Keyboard 类别下。<code>categoryName</code> 的值应当可供用户读取。</td>
    </tr>
    <tr>
      <td><code>libPath</code></td>
      <td>类型库模块的相对路径。不应以斜杠开头。必须引用一个扩展名为 <code>.js</code> 的 JavaScript 文件。</td>
    </tr>
    <tr>
      <td><code>viewPath</code> <em>（可选）</em></td>
      <td>类型视图的相对 URL。应当相对于 <code>viewBasePath</code>，且不应以斜杠开头。必须引用一个扩展名为 <code>.html</code> 的 HTML 文件。可接受查询字符串和片段标识符（哈希）。如果您的类型库模块不使用用户的任何设置，则可以排除此属性，Experience Platform将改为显示一个占位符，以说明无需任何配置。</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td><a href="https://json-schema.org/">JSON 架构</a>的对象，用来描述用户可保存的有效设置对象的格式。设置通常由用户使用数据收集用户界面进行配置和保存。 在这些用例中，扩展的视图可采取必要步骤来验证用户提供的设置。另一方面，有些用户选择直接使用标记API，而不借助任何用户界面。 此架构的目的在于允许Experience Platform正确验证用户保存的设置对象（无论是否使用了用户界面）是否采用了与运行时基于该设置对象执行操作的库模块兼容的格式。<br><br>架构对象的示例如下所示：<br>
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      我们建议使用诸如 <a href="https://www.jsonschemavalidator.net/">JSON 架构验证器</a>之类的工具，手动测试您的架构。</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>（可选）</em></td>
      <td>一个对象数组，其中的每个对象表示当每个相应的设置对象发出到运行时库时所应执行的转换。有关为何需要转换以及如何使用转换的更多信息，请参阅<a href="#transforms">转换</a>部分。</td>
    </tr>
  </tbody>
</table>

### 转换 {#transforms}

对于某些特定用例，扩展要求在将从视图保存的设置对象发出到标记运行时库之前，先由Experience Platform转换这些设置对象。 您可以通过在 `extension.json` 中定义类型定义时设置 `transforms` 属性，来要求执行一个或多个此类转换。`transforms` 属性是一个对象数组，其中的每个对象表示应当执行的转换。

所有转换都需要一个 `type` 和 `propertyPath`。`type`必须为`function`、`remove`和`file`之一，并说明Experience Platform应将哪个转换应用于设置对象。 `propertyPath`是一个以句点分隔的字符串，它告知标记在何处查找设置对象中需要修改的属性。 下面是一个设置对象及部分 `propertyPath` 的示例：

```js
{
  foo: {
    bar: "A string",
    baz: [
      "A",
      "B",
      "C"
    ]
  }
}
```

* 如果设置 `propertyPath` 为 `foo.bar`，则转换 `"A string"` 值。
* 如果设置 `propertyPath` 为 `foo.baz[]`，则转换 `baz` 数组中的每个值。
* 如果设置 `propertyPath` 为 `foo.baz`，则转换 `baz` 数组。

属性路径可使用数组和对象符号的任意组合，在设置对象的任意级别应用转换。

>[!WARNING]
>
>扩展 sandbox*tool 尚不支持在 `propertyPath` 属性中使用数组符号（例如，`foo.baz[]`）。

以下各部分介绍了一些可用的转换和使用这些转换的方式。

#### 函数转换

函数转换允许库模块在所发出的标记运行时库中执行由Experience Platform用户编写的代码。

假设我们希望提供一个“自定义脚本”操作类型。“自定义脚本”操作视图可能提供一个文本区域，用户可在其中输入一些代码。假设用户在该文本区域中输入了以下代码：

`console.log('Welcome, ' + username +'. This is ZomboCom.');`

当用户保存规则后，视图所保存的设置对象可能如下所示：

```javascript
{
  foo: {
    bar: "console.log('Welcome, ' + username +'. This is ZomboCom.');"
  }
}
```

当使用我们的操作的规则在标记运行时库中触发时，我们希望执行用户的代码并为其传递一个用户名。

在从操作类型的视图保存设置对象时，用户的代码仅为一个字符串。其好处是可以与JSON正确进行双向序列化；不过，这种类型也存在弊端，因为它通常会作为字符串而非可执行函数发出到标记运行时库中。 尽管您可以尝试使用 [`eval`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/eval) 或 [Function 构造函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function)在您的操作类型库模块中执行代码，但是由于[内容安全策略](https://developer.mozilla.org/zh-CN/docs/Web/Security/CSP)可能会阻止代码执行，因此我们强烈建议您不要采取此操作。

作为这种情况的临时应对方法，当用户代码发出到标记运行时库时，使用函数转换告知Experience Platform将用户代码包含在可执行函数中。 为了解决我们的示例问题，我们将在 `extension.json` 的类型定义中定义转换，如下所示：

```json
{
  "transforms": [
    {
      "type": "function",
      "propertyPath": "foo.bar",
      "parameters": ["username"]
    }
  ]
}
```

* `type` 定义应用于设置对象的转换类型。
* `propertyPath`是一个以句点分隔的字符串，用于告知Experience Platform在何处查找设置对象中需要修改的属性。
* `parameters` 是一个参数名称数组，应包含在包装函数的签名中。

当设置对象发出到标记运行时库时，它将转换为以下内容：

```javascript
{
  foo: {
    bar: function(username) {
      console.log('Welcome, ' + username +'. This is ZomboCom.');
    }
  }
}
```

接下来，您的库模块可调用包含用户代码的函数，并在 `username` 参数中传递。

#### 文件转换

文件转换允许将Experience Platform用户编写的代码发出到与标记运行时库不同的文件中。 该文件将与标记运行时库一起托管，并且随后可以根据扩展的需要在运行时加载。

假设我们希望提供一个“自定义脚本”操作类型。该操作类型的视图可能提供一个文本区域，用户可在其中输入一些代码。假设用户在该文本区域中输入了以下代码：

`console.log('This is ZomboCom.');`

当用户保存规则后，视图所保存的设置对象可能如下所示：

```js
{
  foo: {
    bar: "console.log('This is ZomboCom.');"
  }
}
```

我们希望将用户代码放置在一个单独的文件中，而不是包含在标记运行时库中。 当使用我们的操作的规则在标记运行时库中触发时，我们希望通过将脚本元素附加到文档正文来加载用户代码。 为了解决我们的示例问题，我们将在 `extension.json` 的操作类型定义中定义转换，如下所示：

```json
{
  "transforms": [
    {
      "type": "file",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` 定义应用于设置对象的转换类型。
* `propertyPath`是一个以句点分隔的字符串，用于告知Experience Platform在何处查找设置对象中需要修改的属性。

当设置对象发出到标记运行时库时，它将转换为以下内容：

```javascript
{
  foo: {
    bar: "//launch.cdn.com/path/abc.js"
  }
}
```

在此用例中，`foo.bar` 的值已转换为 URL。确切的 URL 将在构建库时进行确定。该文件将始终具有 `.js` 扩展名，并采用面向 JavaScript 的 MIME 类型传送。我们以后可能会添加对其他 MIME 类型的支持。

#### 移除转换

默认情况下，设置对象的所有属性都会发出到标记运行时库。 如果某些属性仅用于扩展视图，尤其是当它们包含敏感信息（例如机密令牌)时，您应该使用“移除转换”来防止将信息发出到标记运行时库。

假设我们希望提供一种新的操作类型。该操作类型的视图可能提供一个输入区域，用户可以在其中输入一个允许连接到特定 API 的密钥。假设用户在该区域输入了以下文本：

`ABCDEFG`

当用户保存规则后，视图所保存的设置对象可能如下所示：

```js
{
  foo: {
    bar: "ABCDEFG"
  }
}
```

我们不希望在标记运行时库中包含属性`bar`。 为了解决我们的示例问题，我们将在 `extension.json` 的操作类型定义中定义转换，如下所示：

```json
{
  "transforms": [
    {
      "type": "remove",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` 定义应用于设置对象的转换类型。
* `propertyPath`是一个以句点分隔的字符串，用于告知Experience Platform在何处查找设置对象中需要修改的属性。

当设置对象发出到标记运行时库时，它将转换为以下内容：

```js
{
  foo: {
  }
}
```

在此用例中，`foo.bar` 的值已从设置对象中移除。
