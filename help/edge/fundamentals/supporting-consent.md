---
title: 支持同意
seo-title: 支持Adobe Experience PlatformWeb SDK同意首选项
description: 了解如何使用Experience PlatformWeb SDK支持同意首选项
seo-description: 了解如何使用Experience PlatformWeb SDK支持同意首选项
keywords: consent;defaultConsent;default consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---


# 支持同意

为了尊重用户的隐私，您可能希望在允许SDK出于某些目的使用用户特定数据之前征求用户的同意。 目前，SDK仅允许用户选择加入执行所有用途，但未来Adobe希望对特定用途提供更精细的控制。

如果用户选择用于所有目的，则允许SDK执行以下任务:

* 向Adobe服务器发送数据或从其发送数据。
* 读写cookie或Web存储项（用户选择加入首选项的保留除外）。

如果用户选择出于所有目的，则SDK不执行任何这些任务。

## 配置同意

默认情况下，用户选择用于所有目的。 要阻止SDK在用户进入之前执行上述任务，请在SDK配置 `"defaultConsent": "pending"` 过程中进行传递，如下所示：

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

当一般用途的默认同意设置为“待定”时，尝试执行任何依赖于用户选择加入首选项的命令(例如，命令 `event` )会导致命令在SDK中排队。 在您将用户的选择加入首选项通知SDK之前，不会处理这些命令。

此时，您可能希望让用户在您的用选择加入户界面中找到某处。 在收集用户的首选项后，将这些首选项告知SDK。

## 通过Adobe标准交流同意偏好

如果用户选择，则执行 `setConsent` 将选项 `general` 设置为 `in` 如下的命令：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    }]
});
```

由于用户现在已选择加入，SDK将执行所有以前排队的命令。 将来根据用户选择的命令不会排队，而是立即执行。

如果用户选择选择退出执行该命令， `setConsent` 并将选 `general` 项设置为 `out` 如下：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "out"
      }
    }]
});
```

>[!NOTE]
>
>用户选择退出后，SDK将不允许您设置用户同意 `in`。

由于用户选择选择退出了，从先前排队的命令返回的承诺将被拒绝。 取决于用户选择加入的将来命令将返回同样被拒绝的承诺。 有关处理或隐藏错误的详细信息，请参阅执 [行命令](executing-commands.md)。

>[!NOTE]
>
>目前，SDK仅支持此目 `general` 的。 尽管我们计划构建一套更可靠的用途或类别，这些用途或Adobe将与不同的功能和产品产品相对应，但当前的实施只是选择加入的全部或全部方法。  这仅适用于Adobe Experience Platform, [!DNL Web SDK] 而不适用于其他AdobeJavaScript库。

## 通过IAB TCF标准交流同意偏好

SDK支持记录通过交互式广告局欧洲(IAB)透明度和同意框架(TCF)标准提供的用户同意偏好。 同意字符串可通过上述相同的setConnence命令进行设置，如下所示：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

以这种方式设置同意后，实时客户用户档案会使用同意信息进行更新。 要使此用户档案正常工作，XDM模式需要包含 [用户档案隐私混合](https://github.com/adobe/xdm/blob/master/docs/reference/context/profile-privacy.schema.md)。 发送事件时，需要将IAB同意信息手动添加到事件XDM对象。 SDK不会自动在事件中包含同意信息。 要在事件中发送同意信息， [需要将“体验事件隐](https://github.com/adobe/xdm/blob/master/docs/reference/context/experienceevent-privacy.schema.md) 私混合”添加到“体验事件”模式。

## 在一个请求中发送两个标准

SDK还支持在请求中发送多个同意对象。

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## 同意偏好的持续存在

在您使用命令向SDK传达用户首 `setConsent` 选项后，SDK会将用户首选项保留为cookie。 下次用户在浏览器中加载您的网站时，SDK将检索并使用这些保留的首选项来确定是否可以将事件发送到Adobe。 无需再执行该命 `setConsent` 令，只需传达用户首选项的更改即可，您可以随时执行此操作。

## 设置同意时同步身份

当默认同意待决时，“setConnence”可能是发出并确定身份的第一个请求。 因此，在第一个请求上同步身份可能很重要。 可以像在“sendEvent”命令中一样将标识图添加到“setConnence”命令中。 请参 [阅检索Experience CloudID](./identity.md)

