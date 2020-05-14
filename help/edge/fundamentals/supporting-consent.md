---
title: 支持同意
seo-title: 支持Adobe Experience Platform Web SDK同意首选项
description: 了解如何通过Experience Platform Web SDK支持同意首选项
seo-description: 了解如何通过Experience Platform Web SDK支持同意首选项
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# 支持同意

为了尊重用户的隐私，您可能希望在允许SDK出于某些目的使用用户特定数据之前征求用户的同意。 目前，SDK仅允许用户选择加入执行或执行所有用途，但Adobe希望将来能够更精细地控制特定用途。

如果用户选择用于所有目的，则允许SDK执行以下任务:

* 在Adobe服务器之间发送数据。
* 读写cookie或Web存储项（用户选择加入首选项的保留除外）。

如果用户选择出于所有目的，则SDK不执行任何这些任务。

## 配置同意

默认情况下，用户选择用于所有目的。 要阻止SDK在用户进入之前执行上述任务，请在SDK配置 `"defaultConsent": { "general": "pending" }` 过程中进行传递，如下所示：

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

当一般用途的默认同意设置为“待定”时，尝试执行任何依赖于用户选择加入首选项的命令(例如，命令 `event` )会导致命令在SDK中排队。 在您将用户的选择加入首选项通知SDK之前，不会处理这些命令。

此时，您可能希望让用户在您的用选择加入户界面中找到某处。 在收集用户的首选项后，将这些首选项告知SDK。

## 交流同意偏好

如果用户选择，则执行 `setConsent` 将选项 `general` 设置为 `in` 如下的命令：

```javascript
alloy("setConsent", {
  "general": "in"
});
```

由于用户现在已选择加入，SDK将执行所有以前排队的命令。 将来根据用户选择加入的命令 _不会_ 排队，而是立即执行。

如果用户选择选择退出执行该命令， `setConsent` 并将选 `general` 项设置为 `out` 如下：

```javascript
alloy("setConsent", {
  "general": "out"
});
```

>[!NOTE]
>
>用户选择退出后，SDK将不允许您设置用户同意 `in`。

由于用户选择选择退出了，从先前排队的命令返回的承诺将被拒绝。 取决于用户选择加入的将来命令将返回同样被拒绝的承诺。 有关处理或隐藏错误的详细信息，请参阅执 [行命令](executing-commands.md)。

>[!NOTE]
>
>目前，SDK仅支持此目 `general` 的。 尽管我们计划构建一套更强大的用途或类别，这些用途或将与不同的Adobe功能和产品产品相对应，但当前的实施只是选择加入的一种全部或全部方法。  这仅适用于Adobe Experience Platform Web SDK，而不适用于其他Adobe JavaScript库。

## 同意偏好的持续存在

在您使用命令向SDK传达用户首 `setConsent` 选项后，SDK会将用户首选项保留为cookie。 下次用户在浏览器中加载您的网站时，SDK将检索并使用这些保留的首选项。 无需再执行该命 `setConsent` 令，只需传达用户首选项的更改即可，您可以随时执行此操作。