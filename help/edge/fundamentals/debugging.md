---
title: 在Adobe Experience Platform Web SDK中调试
description: 了解如何在Experience Platform Web SDK中切换调试功能。
keywords: 调试web sdk；调试；配置；配置命令；调试命令；edgeConfigId;setDebug;debugEnabled；调试；
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# 调试

启用调试时，SDK会将消息输出到浏览器控制台，这些消息在调试实施和了解SDK的行为时会有所帮助。 调试还会导致服务器端同步验证根据您配置的模式收集的数据。

默认情况下禁用调试，但可以通过三种不同方式切换：

* `configure` 命令
* `setDebug` 命令
* 查询字符串参数

## 使用“配置”命令切换调试

使用`configure`命令配置SDK时，请通过将`debugEnabled`选项设置为`true`来启用调试。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>这允许对网页的所有用户进行调试，而不是仅针对您的个人浏览器。

## 使用“调试”命令切换调试

使用单独的`debug`命令切换调试，如下所示：

```javascript
alloy("setDebug", {
  "enabled": true
});
```

如果您不希望更改网页上的代码，或不希望为网站的所有用户生成日志记录消息，则此功能特别有用，因为您可以随时在浏览器的JavaScript控制台中运行`debug`命令。

## 使用查询字符串参数切换调试

通过将`alloy_debug`查询字符串参数设置为`true`或`false`来切换调试，如下所示：

```HTTP
http://example.com/?alloy_debug=true
```

与`debug`命令类似，如果您不希望更改网页上的代码或不希望为网站的所有用户生成日志记录消息，则这特别有用，因为您可以在浏览器中加载网页时设置查询字符串参数。

## 优先级和持续时间

当通过`debug`命令或查询字符串参数设置调试时，它将覆盖在`configure`命令中设置的任何`debug`选项。 在这两种情况下，调试在会话期间也保持切换状态。 换句话说，如果您使用debug命令或查询字符串参数启用调试，则直到以下某项为止才会启用它：

* 会话结束
* 运行`debug`命令
* 您再次设置查询字符串参数

## 检索库信息

访问加载到网站的库后的部分详细信息通常很有帮助。 为此，请执行`getLibraryInfo`命令，如下所示：

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

当前，提供的`libraryInfo`对象包含以下属性：

* `version` 这是加载库的版本。例如，如果要加载的库版本为1.0.0，则值将为`1.0.0`。
