---
title: 使用Adobe Experience Platform Web SDK支持客户同意首选项
description: 了解如何通过Adobe Experience Platform Web SDK支持同意首选项。
keywords: 同意；默认同意；默认同意；setConsent；配置文件隐私字段组；体验事件隐私字段组；隐私字段组；
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
source-git-commit: 16c8972333fa67fa2e308445f4ad6282510370d1
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# 支持客户同意首选项

为了尊重用户的隐私，您可能需要先请求用户同意，然后才允许SDK将特定于用户的数据用于某些目的。 目前，SDK仅允许用户选择加入或退出所有目的，但将来，我们希望能够对特定目的提供更加精细的控制。

如果用户出于所有目的选择加入，则允许SDK执行以下任务：

* 将数据发送到Adobe服务器和从服务器发送数据。
* 读取和写入Cookie或Web存储项。

如果用户选择出于所有目的，SDK将不执行任何这些任务。

## 配置同意

默认情况下，用户将选择加入所有目的。 要阻止SDK在用户选择加入之前执行上述任务，请通过 `"defaultConsent": "pending"` 在SDK配置期间执行以下操作：

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

当一般目的的默认同意设置为待处理时，尝试执行依赖于用户选择加入首选项的任何命令(例如， `sendEvent` 命令)会导致命令在SDK中排队。 在将用户的选择加入首选项告知SDK后，才会处理这些命令。

>[!NOTE]
>
>命令仅在内存中排队。 页面加载时不会保存它们。

如果您不想收集在用户的选择加入首选项设置之前发生的事件，则可以通过 `"defaultConsent": "out"` 在SDK配置期间。 尝试执行任何依赖于用户选择加入首选项的命令在您将用户的选择加入首选项告知SDK之前不会起作用。

>[!NOTE]
>
>目前，SDK仅支持一个全部或全部不支持的目的。 尽管我们计划构建一组更可靠的目的或类别，这些目的或类别将与不同的Adobe功能和产品选项相对应，但当前的实施是选择加入的一种完全或完全不采用的方法。  这仅适用于Adobe Experience Platform [!DNL Web SDK] 和其他AdobeJavaScript库。

此时，您可能希望用户在用户界面中的某个位置选择加入。 收集用户首选项后，将这些首选项告知SDK。

## 通过Adobe Experience Platform标准传达同意首选项

SDK支持版本1.0和2.0的Adobe Experience Platform同意标准。 目前，1.0和2.0标准仅支持自动执行全部或全部不执行同意首选项。 1.0标准正在逐步取消，以支持2.0标准。 2.0标准允许您添加其他同意首选项，以用于手动强制执行同意首选项。

### 使用Adobe标准版本2.0

如果您使用的是Adobe Experience Platform，则需要在用户档案架构中包含隐私架构字段组。 请参阅 [Adobe Experience Platform中的管理、隐私和安全](../../landing/governance-privacy-security/overview.md) 有关Adobe标准版本2.0的更多信息。您可以在与 `consents` 字段 [!UICONTROL 同意和首选项] 用户档案字段组。

如果用户选择加入，则执行 `setConsent` 将收集首选项设置为 `y` 如下所示：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    }]
});
```

时间字段应指定用户上次更新其同意首选项的时间。 如果用户选择禁用，请执行 `setConsent` 将收集首选项设置为 `n` 如下所示：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        },
        metadata: {
          time: "2021-03-17T15:51:30-07:00"
        }
      }
    }]
});
```

### 使用Adobe标准版本1.0

如果用户选择加入，则执行 `setConsent` 命令 `general` 选项设置为 `in` 如下所示：

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

如果用户选择禁用，请执行 `setConsent` 命令 `general` 选项设置为 `out` 如下所示：

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

## 通过IAB TCF标准传达同意首选项

SDK支持记录通过欧洲互动广告局(IAB)透明度和同意框架(TCF)标准提供的用户同意首选项。 同意字符串可通过相同的 `setConsent` 命令如下所示：

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

以这种方式设置同意后，实时客户资料会更新以包含同意信息。 要使此功能正常工作，配置文件XDM架构需要包含 [配置文件隐私架构字段组](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). 发送事件时，需要将IAB同意信息手动添加到事件XDM对象。 SDK不会自动在事件中包含同意信息。 要在事件中发送同意信息，请 [体验事件隐私字段组](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) 需要将添加到体验事件架构。

## 在一个请求中发送多个标准

SDK还支持在请求中发送多个同意对象。

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## 同意首选项的持续性

在您使用将用户首选项 `setConsent` 命令时，SDK会将用户首选项保留为Cookie。 下次用户在浏览器中加载您的网站时，SDK将检索并使用这些保留的首选项来确定事件是否可以发送到Adobe。

您需要独立存储用户首选项，才能显示包含当前首选项的同意对话框。 无法从SDK检索用户首选项。 要确保用户首选项与SDK保持同步，您可以调用 `setConsent` 命令。 只有在首选项发生更改时，SDK才会进行服务器调用。

## 在设置同意时同步身份

当默认同意处于待处理状态或结束状态时， `setConsent` 可能是发出并建立身份的第一个请求。 因此，在第一个请求上同步身份可能很重要。 身份映射可添加到 `setConsent` 命令就象在 `sendEvent` 命令。 请参阅 [检索Experience CloudID](../identity/overview.md)
