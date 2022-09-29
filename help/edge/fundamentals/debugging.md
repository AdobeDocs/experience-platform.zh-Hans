---
title: 在Adobe Experience Platform Web SDK中进行调试
description: 了解如何在Experience PlatformWeb SDK中切换调试功能。
keywords: 调试Web SDK；调试；配置；配置命令；调试命令；edgeConfigId;setDebug;debugEnabled；调试；
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---

# 调试

启用调试功能后，SDK会将消息输出到浏览器控制台，这有助于调试您的实施并了解SDK的行为方式。

默认情况下，调试处于禁用状态，但可以通过四种不同方式在其中切换：

* `configure` 命令
* `setDebug` 命令
* 查询字符串参数
* 在Adobe Experience Platform Debugger中打开“启用调试”。 Adobe Experience Platform是一款功能强大的工具，可检查您的网页，并帮助您调试Experience Cloud产品的实施问题。 Adobe Experience Platform Debugger同时作为 [铬黄](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 和 [Firefox](https://addons.mozilla.org/zh-CN/firefox/addon/adobe-experience-platform-dbg/) 扩展。 可以从AEP Web SDK部分的配置选项卡中启用调试。

![](../assets/enable-debugging.png)

## 使用“配置”命令切换调试

在使用 `configure` 命令，通过设置 `debugEnabled` 选项 `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>这允许为网页的所有用户进行调试，而不是仅为您的个人浏览器进行调试。

## 使用Debug命令切换调试

使用单独的 `debug` 命令：

```javascript
alloy("setDebug", {
  "enabled": true
});
```

如果您不希望更改网页上的代码或不希望为网站的所有用户生成日志记录消息，则此功能特别有用，因为您可以运行 `debug` 命令。

## 使用查询字符串参数切换调试

通过设置 `alloy_debug` 查询字符串参数 `true` 或 `false` 如下所示：

```HTTP
http://example.com/?alloy_debug=true
```

与 `debug` 命令，如果您不希望更改网页上的代码或不希望为网站的所有用户生成日志记录消息，则此功能特别有用，因为您可以在浏览器中加载网页时设置查询字符串参数。

## 优先级和持续时间

通过 `debug` 命令或查询字符串参数，它将覆盖任何 `debug` 选项 `configure` 命令。 在这两种情况下，调试在会话期间也会保持打开状态。 换言之，如果您使用debug命令或查询字符串参数启用调试功能，则在启用调试功能之前，该功能会一直处于启用状态，直到出现以下任一情况：

* 会话结束
* 运行 `debug` 命令
* 再次设置查询字符串参数

## 检索库信息

访问您加载到网站上的库后面的某些详细信息通常会很有帮助。 为此，请执行 `getLibraryInfo` 命令：

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

目前，提供的 `libraryInfo` 对象包含以下属性：

* `version`:这是已加载库的版本。 例如，如果正在加载的库版本为1.0.0，则值将为 `1.0.0`. 在标记扩展（名为“AEP Web SDK”）中运行库时，版本是库版本，并且标记扩展版本使用“+”符号联接。 例如，如果库版本为1.0.0，而标记扩展的版本为1.2.0，则值将为 `1.0.0+1.2.0`.
* `commands`:这些是加载的库支持的所有可用命令。
* `configs`:这些是已加载库中的所有当前配置。
