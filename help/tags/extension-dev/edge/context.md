---
title: Edge擴充功能模組中的內容
description: 瞭解上下文物件，及其在與Edge屬性的標籤擴充功能中的程式庫模組互動時所扮演的角色。
exl-id: 04e4e369-687e-4b46-9d24-18a97a218555
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 77%

---

# Edge 扩展模块中的上下文

>[!NOTE]
>
> Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

Edge 扩展中的所有库模块在执行时，都会获得一个 `context` 对象。本文档介绍了 `context` 对象提供的属性，以及些属性在库模块中发挥的作用。

## Adobe 请求上下文 (arc)

`arc` 属性作为一个对象，提供了关于触发规则的事件的信息。以下各部分介绍了此对象中包含的各种子属性。

### [!DNL event]

此 `event` object代表觸發規則的事件，並包含以下值：

```js
logger.log(context.arc.event);
```

| 属性 | 描述 |
| --- | --- |
| `xdm` | 事件的 XDM 对象。 |
| `data` | 自定义数据层。 |

### [!DNL request]

不要与客户端设备的请求混淆，`request` 是来自 Adobe Experience Platform Edge Network 的稍作修改的对象。

```js
logger.log(context.arc.request)
```

`request` 对象有两个顶级属性：`body` 和 `head`。此 `body` 屬性包含Experience Data Model (XDM)資訊，當您導覽至「 」時，可在Adobe Experience Platform Debugger中檢視 **[!UICONTROL Launch]** 並選取 **[!UICONTROL 邊緣追蹤]** 標籤。

### [!DNL ruleStash] {#rulestash}

`ruleStash` 是一个对象，将从操作模块中收集所有结果。

```js
logger.log(context.arc.ruleStash);
```

每个扩展都有自己的命名空间。例如，如果您将扩展命名为 `send-beacon`，则 `send-beacon` 操作的所有结果都将存储在 `ruleStash['send-beacon']` 命名空间中。

每个扩展的命名空间都是唯一的，并且开头的值为 `undefined`。

从每个操作中返回的结果将会覆盖命名空间。例如，假定一个 `transform` 扩展中包含两个操作：`generate-fullname` 和 `generate-fulladdress`。则这两个操作随后会添加到规则中。

如果 `generate-fullname` 操作的结果为 `Firstname Lastname`，则完成该操作后的规则存储将如下所示：

```js
{
  transform: 'Firstname Lastname'
}
```

如果 `generate-address` 操作的结果为 `3900 Adobe Way`，则完成该操作后的规则存储将如下所示：

```js
{
  transform: '3900 Adobe Way'
}
```

请注意，“Firstname Lastname”不再存在于规则存储中，因为 `generate-address` 操作会用新值将其覆盖。

如果您想让 `ruleStash` 在 `transform` 命名空间内存储这两个操作的结果，您可以编写类似于以下示例的操作模块：

```js
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;

  if (!transformRuleStash) {
    transformRuleStash = {};
  }

  transformRuleStash.fullName = 'Firstname Lastname';

  return transformRuleStash;
}
```

首次执行此操作时，由于 `ruleStash` 开始于 `undefined`，因此将其初始化为一个空对象。下次执行该操作时，将会收到先前调用该操作时所返回的 `ruleStash`。通过将对象用作 `ruleStash`，您可以添加新数据，而不会丢失先前由扩展中的其他操作设置的数据。

>[!NOTE]
>
>使用此策略時，請務必小心傳回完整的擴充功能規則隱藏專案。 如果您只傳回值，則會覆寫您可能已設定的任何其他屬性。

## 实用工具

此 `utils` 屬性代表提供標籤執行階段專用公用程式的物件。

### [!DNL logger]

此 `logger` 公用程式可讓您記錄在使用時於偵錯工作階段顯示的訊息 [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob).

```js
context.utils.logger.error('Error!');
```

该日志记录器包括以下方法，其中 `message` 是您要记录的消息：

| 方法 | 描述 |
| --- | --- |
| `log(message)` | 将消息记录到控制台。 |
| `info(message)` | 将信息性消息记录到控制台。 |
| `warn(message)` | 将警告消息记录到控制台。 |
| `error(message)` | 将错误消息记录到控制台。 |
| `debug(message)` | 将调试消息记录到控制台。仅当在浏览器控制台中启用 `verbose` 日志记录时才可见。 |

### [!DNL fetch]

该实用程序将实施 [Fetch API](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API)。您可以使用该函数向第三方端点发送请求。

```js
context.utils.fetch('http://example.com/movies.json')
  .then(response => response.json())
```

### [!DNL getBuildInfo]

此公用程式會傳回物件，內含目前標籤執行階段程式庫組建的相關資訊。

```js
logger.log(context.utils.getBuildInfo().turbineBuildDate);
```

该对象包含以下值：

| 属性 | 描述 |
| --- | --- |
| `turbineVersion` | 当前库中使用的 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) 版本。 |
| `turbineBuildDate` | 生成容器内使用的 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge) 版本的 ISO 8601 日期。 |
| `buildDate` | 生成当前库的 ISO 8601 日期。 |
| `environment` | 生成此库的环境。可能的值包括 `development`、`staging` 和 `production.`。 |

以下是一个示例 `getBuildInfo` 对象，用于演示它返回的值：

```js
{
  turbineVersion: "1.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

### [!DNL getExtensionSettings]

该实用程序返回了上次从[扩展配置](../configuration.md)视图中保存的 `settings` 对象。

```js
logger.log(context.utils.getExtensionSettings());
```

### [!DNL getSettings]

该实用程序返回了上次从相应的库模块视图中保存的 `settings` 对象。

```js
logger.log(context.utils.getSettings());
```

### [!DNL getRule]

该实用程序返回了一个对象，其中包含有关触发模块的规则的信息。

```js
logger.log(context.utils.getRule());
```

该对象将包含以下值：

| 属性 | 描述 |
| --- | --- |
| `id` | 规则 ID。 |
| `name` | 规则名称。 |
