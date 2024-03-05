---
title: 使用Adobe Experience Platform Web SDK支持客户同意首选项
description: 了解如何通过Adobe Experience Platform Web SDK支持同意首选项。
keywords: 同意；defaultConsent；默认同意；setConsent；配置文件隐私字段组；体验事件隐私字段组；隐私字段组；
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# 支持客户同意首选项

为了尊重用户的隐私，在允许SDK将特定于用户的数据用于某些目的之前，您可能需要请求用户同意。 目前，SDK仅允许用户选择加入或退出所有目的，但未来Adobe希望针对特定目的提供更精细的控制。

如果用户选择加入所有目的，则允许SDK执行以下任务：

* 将数据发送到Adobe的服务器或从中发送数据。
* 读取和写入Cookie或Web存储项目。

如果用户选择退出所有用途，SDK不会执行任何这些任务。

## 配置同意

默认情况下，用户会选择加入所有用途。 要在用户选择加入之前阻止SDK执行上述任务，请传递 `"defaultConsent": "pending"` 在SDK配置期间，如下所示：

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

当用于常规用途的默认同意设置为pending时，尝试执行依赖于用户选择加入首选项的任何命令(例如 `sendEvent` 命令)会导致命令在SDK中排队。 在将用户的选择加入首选项告知SDK之前，不会处理这些命令。

>[!NOTE]
>
>命令仅在内存中排队。 它们不会跨页面加载保存。

如果您不希望收集在设置用户的选择加入首选项之前发生的事件，则可以传递 `"defaultConsent": "out"` 在SDK配置期间。 在您将用户的选择加入首选项传达给SDK之前，尝试执行任何依赖于用户选择加入首选项的命令将不会起作用。

>[!NOTE]
>
>当前，SDK仅支持一个全部用途或不支持任何用途。 尽管我们计划构建一组更强大的用途或类别，以对应不同的Adobe功能和产品选项，但当前的实施对于选择加入而言要么全有，要么全无。  这仅适用于Adobe Experience Platform [!DNL Web SDK] 而不是其他AdobeJavaScript库。

此时，您可能更希望请求用户在用户界面内的某个位置选择加入。 收集用户的首选项后，将这些首选项传递给SDK。

## 通过Adobe Experience Platform标准传达同意首选项

SDK支持版本1.0和2.0的Adobe Experience Platform consent standard。 目前，1.0和2.0标准仅支持自动执行全部或全部不同意的偏好设置。 1.0标准正在逐步淘汰，取而代之的是2.0标准。 2.0标准允许您添加其他同意首选项，这些首选项可用于手动实施同意首选项。

### 使用Adobe标准版本2.0

如果您使用的是Adobe Experience Platform，则需要在配置文件架构中包含隐私架构字段组。 请参阅 [Adobe Experience Platform中的治理、隐私和安全性](../../landing/governance-privacy-security/overview.md) 有关Adobe标准版本2.0的更多信息。您可以在对应于以下架构的值对象中添加数据 `consents` 字段 [!UICONTROL 同意和偏好设置] 配置文件字段组。

如果用户选择加入，执行 `setConsent` 命令并将收集首选项设置为 `y` 如下所示：

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

时间字段应指定用户上次更新其同意首选项的时间。 如果用户选择退出，请执行 `setConsent` 命令并将收集首选项设置为 `n` 如下所示：

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

如果用户选择加入，执行 `setConsent` 命令和 `general` 选项设置为 `in` 如下所示：

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

如果用户选择退出，请执行 `setConsent` 命令和 `general` 选项设置为 `out` 如下所示：

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

SDK支持记录通过欧洲互动广告局(IAB)透明度和同意框架(TCF)标准提供的用户同意首选项。 同意字符串可以通过相同的 `setConsent` 命令如下所示：

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

以这种方式设置同意后，Real-time Customer Profile将更新同意信息。 要使此功能正常工作，配置文件XDM架构需要包含 [配置文件隐私架构字段组](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). 发送事件时，需要手动将IAB同意信息添加到事件XDM对象。 SDK不会自动在事件中包含同意信息。 要在事件中发送同意信息，请 [体验事件隐私字段组](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) 需要添加到“体验事件”架构中。

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

## 同意偏好设置的持久性

在使用向SDK传达用户偏好设置后， `setConsent` 命令时，SDK会保留用户对Cookie的偏好设置。 下次用户在浏览器中加载您的网站时，SDK将检索并使用这些保留的首选项来确定是否可将事件发送到Adobe。

您需要单独存储用户偏好设置才能显示同意对话框以及当前偏好设置。 无法从SDK检索用户偏好设置。 要确保用户首选项与SDK保持同步，您可以调用 `setConsent` 命令进行加载。 仅当首选项已更改时，SDK才会进行服务器调用。

## 在设置同意时同步身份

当默认同意处于待处理状态或退出状态时， `setConsent` 可能是第一个发出并建立身份的请求。 因此，在第一个请求上同步身份可能很重要。 可以将身份映射添加到 `setConsent` 命令，就像在 `sendEvent` 命令。 请参阅 [正在检索Experience CloudID](../identity/overview.md)
