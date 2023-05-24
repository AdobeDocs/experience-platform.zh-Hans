---
title: 擴充功能資訊清單
description: 瞭解如何設定JSON資訊清單檔案，以告知Adobe Experience Platform如何正確使用您的擴充功能。
exl-id: 7cac020b-3cfd-4a0a-a2d1-edee1be125d0
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '2645'
ht-degree: 76%

---

# 扩展清单

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../term-updates.md)。

在扩展的基目录中，必须创建一个名为 `extension.json` 的文件。该文件包含有关扩展的重要详细信息，借助该信息，Adobe Experience Platform 可以正确使用扩展。其中的部分内容采用 [npm 的 `package.json`](https://docs.npmjs.com/files/package.json) 方式构成。

[Hello World 扩展](https://github.com/adobe/reactor-helloworld-extension/blob/master/extension.json) GitHub 存储库中提供了 `extension.json` 示例。

扩展清单必须包含以下属性：

| 属性 | 描述 |
| --- | --- |
| `name` | 扩展的名称。此名称必须唯一，不同于所有其他 扩展，且必须符合[命名规则](#naming-rules)。**標籤會以此名稱作為識別碼，您在發佈擴充功能後不應加以變更。** |
| `platform` | 用于此扩展的平台。目前唯一接受的值是 `web`。 |
| `version` | 此扩展的版本。必须遵循 [semver](https://semver.org/) 版本控制格式。与 [npm 版本字段](https://docs.npmjs.com/files/package.json#version)规则相一致。 |
| `displayName` | 用户可读的扩展名称。系統會向Platform使用者顯示這項資訊。 名稱中無需提及「標籤」或「擴充功能」；使用者很清楚他們看到的就是標籤擴充功能。 |
| `description` | 有关扩展的描述。系統會向Platform使用者顯示這項資訊。 如果您的扩展使用户能够在其网站上实施您的产品，请说明产品的功能。名稱中無需提及「標籤」或「擴充功能」；使用者很清楚他們看到的就是標籤擴充功能。 |
| `iconPath`*（可选）* | 為擴充功能顯示之圖示的相對路徑。 不应以斜杠开头。必须引用一个扩展名为 `.svg` 的 SVG 文件。SVG應為正方形，並可由Platform縮放。 |
| `author` | “author”是一个对象，其结构应如下所示： <ul><li>`name`：扩展的作者姓名。或者，也可以在此使用公司名称。</li><li>`url`*（可选）*：一个 URL，可以从中了解有关扩展作者的更多信息。</li><li>`email`*（可选）*：扩展作者的电子邮件地址。</li></ul>与 [npm 作者字段](https://docs.npmjs.com/files/package.json#people-fields-author-contributors)规则相一致。 |
| `exchangeUrl`*（公共扩展的必需属性）* | 指向 Adobe Exchange 上列出的扩展的 URL。必须匹配以下模式：`https://www.adobeexchange.com/experiencecloud.details.######.html`。 |
| `viewBasePath` | 包含您的所有视图及视图相关资源（HTML、JavaScript、CSS、图像）的子目录的相对路径。Platform 将在 Web 服务器上托管此目录，并从中加载 iframe 内容。这是必填字段，且不应以斜杠开头。例如，如果您的所有视图都包含在 `src/view/` 中，则 `viewBasePath` 的值为 `src/view/`。 |
| `hostedLibFiles`*（可选）* | 我們有許多使用者偏好將所有標籤相關檔案託管在自己的伺服器上。 这可以提高用户在运行时对文件可用性的确定级别，而且用户可以轻松扫描代码以发现安全漏洞。如果扩展的库部分需要在运行时加载 JavaScript 文件，则建议使用此属性来列出这些文件。列出的檔案將與標籤執行階段程式庫一起託管。 随后，您的扩展将可以通过使用 [getHostedLibFileUrl](./turbine.md#get-hosted-lib-file) 方法检索到的 URL 来加载文件。<br><br>此选项包含一个数组，其中含有需托管的第三方库文件的相对路径。 |
| `main`*（可选）* | 运行时应执行的库模块的相对路径。<br><br>此模块将始终包含在运行时库中并得以执行。由于此模块始终包含在运行时库中，因此建议仅在绝对有必要的情况下才使用“main”模块，并保持其代码大小最小。<br><br>我们并不保证会首先执行此模块，其他模块有可能会在其之前执行。 |
| `configuration`*（可选）* | 此字段描述扩展的[扩展配置](./configuration.md)部分。如果要求用户提供扩展的全局设置，则需要使用此字段。有关应当如何构建此字段的详细信息，请参阅[附录](#config-object)。 |
| `events`*（可选）* | [事件](./web/event-types.md)类型定义的数组。请参阅附录中的[类型定义](#type-definitions)部分，以了解数组中每个对象的结构。 |
| `conditions`*（可选）* | [条件](./web/condition-types.md)类型定义的数组。请参阅附录中的[类型定义](#type-definitions)部分，以了解数组中每个对象的结构。 |
| `actions`*（可选）* | [操作](./web/action-types.md)类型定义的数组。请参阅附录中的[类型定义](#type-definitions)部分，以了解数组中每个对象的结构。 |
| `dataElements`*（可选）* | [数据元素](./web/data-element-types.md)类型定义的数组。请参阅附录中的[类型定义](#type-definitions)部分，以了解数组中每个对象的结构。 |
| `sharedModules`*（可选）* | 共享模块定义对象的数组。数组中的每个共享模块对象应当具有以下结构： <ul><li>`name`：共享模块的名称。请注意，当从其他扩展引用共享模块时，将使用此名称，如[共享模块](./web/shared.md)中所述。此名称从不显示在任何用户界面中。此名称应当唯一，不同于扩展中其他共享模块的名称，且必须符合[命名规则](#naming-rules)。**標籤會以此名稱作為識別碼，您在發佈擴充功能後不應加以變更。**</li><li>`libPath`：共享模块的相对路径。不应以斜杠开头。必须引用一个扩展名为 `.js` 的 JavaScript 文件。</li></ul> |

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
      <td><a href="https://json-schema.org/">JSON 模式</a>的对象，用来描述从扩展配置视图中保存的有效对象的格式。由于您是配置视图的开发者，因此您有责任确保所有保存的设置对象都与此模式匹配。当用户尝试使用 Platform 服务保存数据时，此模式还将用于执行验证。<br><br>模式对象的示例如下所示：
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
      我们建议使用诸如 <a href="https://www.jsonschemavalidator.net/">JSON 模式验证器</a>之类的工具，手动测试您的模式。</td>
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
      <td>类型的名称。此名称必须是扩展中的唯一名称。此名称必须符合<a href="#naming-rules">命名规则</a>。<strong>標籤會以此名稱作為識別碼，您在發佈擴充功能後不應加以變更。</strong></td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>用來代表資料收集使用者介面中型別的文字。 该文本应当可供用户读取。</td>
    </tr>
    <tr>
      <td><code>categoryName</code> <em>（可选）</em></td>
      <td>提供该属性后，<code>displayName</code> 将会列在 用户界面中的 <code>categoryName</code> 下方。所有具有相同 <code>categoryName</code> 的类型都将列在同一类别下。例如，如果您的扩展提供了 <code>keyUp</code> 事件类型和 <code>keyDown</code> 事件类型，并且它们都具有 <code>categoryName</code> <code>Keyboard</code>，那么当用户在构建规则时从可用事件类型列表中进行选择时，这两个事件类型都会列在 Keyboard 类别下。<code>categoryName</code> 的值应当可供用户读取。</td>
    </tr>
    <tr>
      <td><code>libPath</code></td>
      <td>类型库模块的相对路径。不应以斜杠开头。必须引用一个扩展名为 <code>.js</code> 的 JavaScript 文件。</td>
    </tr>
    <tr>
      <td><code>viewPath</code> <em>（可选）</em></td>
      <td>类型视图的相对 URL。应当相对于 <code>viewBasePath</code>，且不应以斜杠开头。必须引用一个扩展名为 <code>.html</code> 的 HTML 文件。可接受查询字符串和片段标识符（哈希）。如果您的类型库模块不使用用户的任何设置，则可以排除此属性，Platform 将改为显示一个占位符，以说明无需任何配置。</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td><a href="https://json-schema.org/">JSON 模式</a>的对象，用来描述用户可保存的有效设置对象的格式。設定通常由使用者透過資料收集使用者介面進行設定和儲存。 在这些用例中，扩展的视图可采取必要步骤来验证用户提供的设置。另一方面，有些使用者會選擇不藉助於任何使用者介面，而直接使用標籤API。 此模式用于允许 Platform 正确验证用户保存的设置对象（不管是否使用了用户界面）是否采用了与运行时基于该设置对象执行操作的库模块相兼容的格式。<br><br>模式对象的示例如下所示：<br>
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
      我们建议使用诸如 <a href="https://www.jsonschemavalidator.net/">JSON 模式验证器</a>之类的工具，手动测试您的模式。</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>（可选）</em></td>
      <td>一个对象数组，其中的每个对象表示当每个相应的设置对象发出到运行时库时所应执行的转换。有关为何需要转换以及如何使用转换的更多信息，请参阅<a href="#transforms">转换</a>部分。</td>
    </tr>
  </tbody>
</table>

### 转换 {#transforms}

針對特定使用案例，擴充功能需要先由Platform轉換從檢視儲存的設定物件，才能將其發出至標籤執行階段程式庫。 您可以通过在 `extension.json` 中定义类型定义时设置 `transforms` 属性，来要求执行一个或多个此类转换。`transforms` 属性是一个对象数组，其中的每个对象表示应当执行的转换。

所有转换都需要一个 `type` 和 `propertyPath`。`type` 必须是 `function`、`remove` 和 `file` 之一，用于说明 Platform 应当对设置对象执行的转换。此 `propertyPath` 是以句點分隔的字串，用來告知標籤應在何處尋找需要在設定物件中修改的屬性。 下面是一个设置对象及部分 `propertyPath` 的示例：

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

函式轉換可讓Platform使用者所撰寫的程式碼，由發出標籤執行階段程式庫中的程式庫模組執行。

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

當使用我們的動作的規則在標籤執行階段程式庫內引發時，我們想要執行使用者的程式碼並傳遞使用者名稱。

在从操作类型的视图保存设置对象时，用户的代码仅为一个字符串。這是好事，因為它可以正確地在JSON之間序列化；但是，這也壞，因為它通常作為字串而不是可執行函式發出到標籤執行階段程式庫中。 尽管您可以尝试使用 [`eval`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/eval) 或 [Function 构造函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function)在您的操作类型库模块中执行代码，但是由于[内容安全策略](https://developer.mozilla.org/zh-CN/docs/Web/Security/CSP)可能会阻止代码执行，因此我们强烈建议您不要采取此操作。

作為此情況的因應措施，當使用者的程式碼在標籤執行階段程式庫中發出時，使用函式轉換可告知Platform將其包裝在可執行的函式中。 为了解决我们的示例问题，我们将在 `extension.json` 的类型定义中定义转换，如下所示：

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
* `propertyPath` 是一个以句点分隔的字符串，用于告知 Platform 在何处查找设置对象中需要修改的属性。
* `parameters` 是一个参数名称数组，应包含在包装函数的签名中。

當設定物件在標籤執行階段程式庫中發出時，它會轉換為以下內容：

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

檔案轉換可讓Platform使用者所撰寫的程式碼發出至與標籤執行階段程式庫不同的檔案中。 檔案將與標籤執行階段程式庫託管在一起，然後可以根據擴充功能在執行階段中的需求載入。

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

我們想要將使用者的程式碼放入個別檔案中，而不是包含在標籤執行階段程式庫中。 當使用我們的動作的規則在標籤執行階段程式庫內引發時，我們想藉由將指令碼元素附加至檔案內文來載入使用者的程式碼。 为了解决我们的示例问题，我们将在 `extension.json` 的操作类型定义中定义转换，如下所示：

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
* `propertyPath` 是一个以句点分隔的字符串，用于告知 Platform 在何处查找设置对象中需要修改的属性。

當設定物件在標籤執行階段程式庫中發出時，它會轉換為以下內容：

```javascript
{
  foo: {
    bar: "//launch.cdn.com/path/abc.js"
  }
}
```

在此用例中，`foo.bar` 的值已转换为 URL。确切的 URL 将在构建库时进行确定。该文件将始终具有 `.js` 扩展名，并采用面向 JavaScript 的 MIME 类型传送。我们以后可能会添加对其他 MIME 类型的支持。

#### 移除转换

依預設，設定物件的所有屬性都會在標籤執行階段程式庫中發出。 如果某些属性仅用于扩展视图，尤其是当它们包含敏感信息（例如秘密代號)，您應使用移除轉換來防止資訊發出至標籤執行階段程式庫中。

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

我們不想包含屬性 `bar` 在標籤執行階段程式庫中。 为了解决我们的示例问题，我们将在 `extension.json` 的操作类型定义中定义转换，如下所示：

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
* `propertyPath` 是一个以句点分隔的字符串，用于告知 Platform 在何处查找设置对象中需要修改的属性。

當設定物件在標籤執行階段程式庫中發出時，它會轉換為以下內容：

```js
{
  foo: {
  }
}
```

在此用例中，`foo.bar` 的值已从设置对象中移除。
