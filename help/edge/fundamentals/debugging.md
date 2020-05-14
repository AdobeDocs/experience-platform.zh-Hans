---
title: 调试
seo-title: Adobe Experience Platform Web SDK调试
description: 了解如何切换Experience Platform Web SDK调试
seo-description: 了解如何切换Experience Platform Web SDK调试
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# 调试

启用调试时，SDK会将消息输出到浏览器控制台，这些消息对调试实施和了解SDK的行为有帮助。 调试还会根据您配置的模式对正在收集的数据进行服务器端同步验证。

默认情况下，调试处于禁用状态，但可以通过三种不同方式切换：

* `configure` 命令
* `debug` 命令
* 查询字符串参数

## 使用“配置”命令切换调试

使用命令配置SDK `configure` 时，通过将选项设置为启 `debugEnabled` 用调试 `true`。

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!Hint]
>这允许为网页的所有用户（而不是仅为您的个人浏览器）进行调试。

## 使用“调试”命令切换调试

按如下方式使用单独的 `debug` 命令切换调试：

```javascript
alloy("debug", {
  "enabled": true
});
```

如果您不希望更改网页上的代码或不希望为网站的所有用户生成日志消息，这特别有用，因为您可以随时在浏览器的JavaScript `debug` 控制台中运行该命令。

## 使用查询字符串参数切换调试

通过将查询字符串参 `alloy_debug` 数设置为或按如 `true` 下方式 `false` 切换调试：

```HTTP
http://example.com/?alloy_debug=true
```

与命 `debug` 令类似，如果您不希望更改网页上的代码或不希望为网站的所有用户生成日志消息，这特别有用，因为您可以在浏览器中加载网页时设置查询字符串参数。

## 优先级和持续时间

当通过命令或查询字 `debug` 符串参数设置调试时，它将覆盖在命 `debug` 令中设置的任何 `configure` 选项。 在这两种情况下，调试在会话期间也保持切换状态。 换言之，如果您使用debug命令或查询字符串参数启用调试，它将一直处于启用状态，直到出现以下情况之一：

* 会话结束
* 您运行命 `debug` 令
* 您再次设置查询字符串参数
