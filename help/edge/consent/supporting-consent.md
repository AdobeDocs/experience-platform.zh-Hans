---
title: 使用Adobe Experience Platform Web SDK支持客户同意首选项
description: 了解如何使用Adobe Experience Platform Web SDK支持同意首选项。
keywords: 同意；默认同意；默认同意；setConnence;用户档案隐私混合；体验事件隐私混合；隐私混合；
translation-type: tm+mt
source-git-commit: 308c10eb0d1f78dad2b8b6158f28d0384a65c78c
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---


# 支持客户同意首选项

为了尊重用户的隐私，您可能希望在允许SDK将用户特定数据用于某些用途之前征求用户的同意。 目前，SDK仅允许用户执行选择加入或执行所有用途，但未来Adobe希望对特定用途提供更精细的控制。

如果用户选择用于所有目的，则允许SDK执行以下任务:

* 在Adobe的服务器之间发送数据。
* 读写cookie或Web存储项。

如果用户选择出于所有目的，则SDK不执行任何这些任务。

## 配置同意

默认情况下，用户选择用于所有目的。 要防止SDK在用户进入之前执行上述任务，请在SDK配置期间按如下方式传递`"defaultConsent": "pending"`:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

当将默认的一般用途同意设置为“待定”时，尝试执行任何依赖于用户参与首选项的命令（例如，`event`命令）会导致命令在SDK中排队。 在您将用户的选择加入首选项通知SDK之前，不会处理这些命令。

此时，您可能希望让用户在您的用选择加入户界面中的某个位置。 在收集用户的首选项后，将这些首选项与SDK进行通信。

## 通过Adobe Standard传达同意偏好

如果用户选择登录，请执行`general`选项设置为`in`的`setConsent`命令，如下所示：

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

由于用户现在已选择加入，SDK将执行所有以前排队的命令。 将来依赖用户选择的命令不会排队，而是立即执行。

如果用户选择选择退出执行`setConsent`命令，并将`general`选项设置为`out`，如下所示：

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
>在用户选择退出后，SDK将不允许您将用户同意设置为`in`。

由于用户选择了选择退出，从先前排队的命令返回的承诺将被拒绝。 取决于用户选择加入的将来命令将返回同样被拒绝的承诺。 有关处理或隐藏错误的详细信息，请参阅[执行命令](../fundamentals/executing-commands.md)。

>[!NOTE]
>
>目前，SDK仅支持`general`用途。 尽管我们计划构建一套更强大的用途或类别，这些用途或Adobe将与不同的功能和产品种类相对应，但当前实施只是选择加入的一种全部或全部方法。  这仅适用于Adobe Experience Platform [!DNL Web SDK]和其他Adobe JavaScript库。

## 通过IAB TCF标准交流同意偏好

SDK支持记录通过交互式广告局欧洲(IAB)透明度和同意框架(TCF)标准提供的用户同意偏好。 同意字符串可以通过相同的`setConsent`命令进行设置，如下所示：

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

以这种方式设置同意后，实时客户用户档案会使用同意信息进行更新。 要使此功能正常工作，用户档案XDM模式需要包含[用户档案隐私混合](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md)。 发送事件时，需要将IAB同意信息手动添加到事件XDM对象。 SDK不会自动在事件中包含同意信息。 要在事件中发送同意信息，[体验事件隐私混音](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md)需要添加到体验事件模式。

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

## 同意偏好的持续

在使用`setConsent`命令向SDK通知用户首选项后，SDK会继续将用户的首选项用于Cookie。 下次用户在浏览器中加载您的网站时，SDK将检索并使用这些保留的首选项来确定是否可以将事件发送到Adobe。 除了传达用户首选项的更改（您可以随时进行更改）之外，无需再次执行`setConsent`命令。

## 在设置同意时同步身份

当默认同意待决时，`setConsent`可能是发出并建立身份的第一个请求。 因此，在第一个请求上同步身份可能很重要。 可以将标识映射添加到`setConsent`命令，就像在`sendEvent`命令中一样。 请参阅[检索Experience CloudID](../identity/overview.md)

