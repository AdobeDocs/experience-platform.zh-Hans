---
title: 支持同意
seo-title: 支持Adobe Experience Platform Web SDK同意首选项
description: 了解如何使用Experience Platform Web SDK支持同意首选项
seo-description: 了解如何使用Experience Platform Web SDK支持同意首选项
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# （测试版）支持同意

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生更改。

为了尊重用户的隐私，您可能希望在允许SDK将用户特定数据用于某些用途之前征求用户的同意。 目前，SDK仅允许用户选择加入或退出所有用途，但Adobe希望将来能够对特定用途提供更精细的控制。

如果用户选择用于所有目的，则允许SDK执行以下任务：

* 向Adobe服务器发送数据和从Adobe服务器发送数据。
* 读写cookie或Web存储项目（用户的选择加入首选项保持不变除外）。

如果用户退出所有用途，则SDK不执行任何这些任务。

## 配置同意

默认情况下，用户选择用于所有目的。 要阻止SDK在用户进入之前执行上述任务，请在SDK配置过程中 `"defaultConsent": { "general": "pending" }` 按如下方式传递：

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

当将一般用途的默认同意设置为“待定”时，尝试执行依赖于用户选择加入首选项的任何命令（例如，命令）将导致命令在SDK中排队。 `event` 在您将用户的选择加入首选项通知到SDK之前，不会处理这些命令。

此时，您可能希望用户选择在用户界面中的某个位置。 在收集用户的首选项后，将这些首选项传达到SDK。

## 交流同意偏好

如果用户选择，则执行 `setConsent` 将选项设置 `general` 为如下 `in` 的命令：

```javascript
alloy("setConsent", {
  "general": "in"
});
```

由于用户现在已选择加入，因此SDK将执行所有以前排队的命令。 根据用户选择的将来命令不 _会排队_ ，而是立即执行。

如果用户选择退出，则在将选项设 `setConsent` 置为如下时 `general` 执行该 `out` 命令：

```javascript
alloy("setConsent", {
  "general": "out"
});
```

>[!NOTE]
>
>用户选择退出后，SDK将不允许您将用户同意设置为 `in`。

由于用户选择退出，因此会拒绝从先前排队的命令返回的承诺。 取决于用户选择的将来命令将返回同样被拒绝的承诺。 有关处理或隐藏错误的详细信息，请参阅执 [行命令](executing-commands.md)。

>[!NOTE]
>
>目前，SDK仅支持此目 `general` 的。 尽管我们计划构建一套更可靠的用途或类别，这些用途或类别将与不同的Adobe功能和产品服务相对应，但当前的实施是选择加入的全部或全部方法。  这仅适用于Adobe Experience Platform Web SDK，而不适用于其他Adobe JavaScript库。

## 同意偏好的持续存在

在您使用命令将用户首选项通知SDK `setConsent` 后，SDK会将用户首选项保留到Cookie中。 下次用户在浏览器中加载您的网站时，SDK将检索并使用这些保留的首选项。 无需再执行该命 `setConsent` 令，只需传达用户首选项的更改即可，您可以随时执行此更改。