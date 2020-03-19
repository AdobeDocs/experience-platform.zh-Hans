---
title: 调试
seo-title: Adobe Experience Platform Web SDK调试
description: 了解如何切换Experience Platform Web SDK调试
seo-description: 了解如何切换Experience Platform Web SDK调试
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# （测试版）调试

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生更改。

启用调试后，SDK会将消息输出到浏览器控制台，这些消息对调试实施和了解SDK的行为有帮助。 调试还会导致服务器端同步验证根据您配置的架构收集的数据。

默认情况下，调试处于禁用状态，但可以通过三种不同的方式进行切换：

* `configure` 命令
* `debug` 命令
* 查询字符串参数

## 使用“配置”命令切换调试

使用命令配置SDK时， `configure` 通过将选项设置为启用 `debugEnabled` 调试 `true`。

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!Hint]
>这允许对网页的所有用户进行调试，而不仅仅是针对您的个人浏览器。

## 使用“调试”命令切换调试

使用以下单独命令切 `debug` 换调试：

```javascript
alloy("debug", {
  "enabled": true
});
```

如果您不希望更改网页上的代码或不希望为网站的所有用户生成日志消息，这特别有用，因为您可以随时在浏览器的JavaScript控制台中运行该 `debug` 命令。

## 使用查询字符串参数切换调试

通过将查询字符串参数设 `alloy_debug` 置为或按如下方式 `true` 切换 `false` 调试：

```HTTP
http://example.com/?alloy_debug=true
```

与命令类 `debug` 似，如果您不希望更改网页上的代码或不希望为网站的所有用户生成日志消息，这特别有用，因为您可以在浏览器中加载网页时设置查询字符串参数。

## 优先级和持续时间

通过命令或查询字符串参 `debug` 数设置调试时，它将覆盖命令中 `debug` 设置的任何选项 `configure` 。 在这两种情况下，调试在会话期间也保持切换状态。 换句话说，如果您使用debug命令或查询字符串参数启用调试，则直到以下某项为止才会启用它：

* 会话结束
* 您运行命 `debug` 令
* 您再次设置查询字符串参数
