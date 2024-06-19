---
title: defaultconsent
description: 为Web属性设置默认同意收集方法。
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 5%

---


# `defaultConsent`

此 `defaultConsent` 属性确定在调用 [`setConsent`](../setconsent.md) 命令。 当您不希望意外从居住在数据收集之前需要获得同意的区域中的个人收集数据时，此属性很有价值。

默认情况下，用户选择加入所有用途，并且Web SDK允许执行以下任务：

* 将数据发送到Adobe的服务器或从中发送数据。
* 读取和写入Cookie或Web存储项目。

如果用户选择退出所有用途，Web SDK不会执行任何这些任务。

此 `defaultConsent` 属性支持三个值：

* **`in`**：数据收集会正常进行，直到用户选择退出为止。
* **`out`**：数据将永久丢弃，直到用户选择加入为止。
* **`pending`**：数据存储在本地，直到用户选择使用 [`setConsent`](../setconsent.md) 命令。 当常规用途的默认同意设置为 `pending`，尝试执行任何依赖于用户选择加入首选项的命令(例如 [`sendEvent`](../sendevent/overview.md) 命令)会导致命令在Web SDK中排入队列。 在将用户的选择加入首选项告知Web SDK之前，不会处理排队命令。

>[!NOTE]
>
> 同意数据不会在页面加载之间保留。

如果您的访客不属于《通用数据保护条例》(GDPR)的管辖范围，则默认同意可以设置为 `in`. GDPR管辖区内的访客可以将他们的默认同意设置为 `pending`. 您的同意管理平台(CMP)可以检测客户的区域并提供标记 `gdprApplies` 到IAB TCF 2.0。此标记可用于设置默认同意。

如果您不希望收集在设置用户的选择加入首选项之前发生的事件，则可以传递 `"defaultConsent": "out"` 配置Web SDK期间。 在您将用户的选择加入首选项传达给Web SDK之前，尝试执行任何依赖于用户选择加入首选项的命令将不会起作用。

>[!NOTE]
>
>目前，Web SDK仅支持一个全有或全无的目的。 尽管我们计划构建一组更强大的用途或类别，以对应不同的Adobe功能和产品选项，但当前的实施对于选择加入是一种“要么全有，要么全无”的方法。  这仅适用于 [!DNL Web SDK] 而不是其他AdobeJavaScript库。

## 使用 `defaultConsent` 与 `setConsent` {#using-consent}

Web SDK提供了两个互补的同意配置命令：

* [`defaultConsent`](defaultconsent.md)：此命令用于捕获使用Web SDK的Adobe客户的同意首选项。
* [`setConsent`](../setconsent.md)：此命令用于捕获网站访客的同意首选项。

如果同时使用这些设置，则可能会导致数据收集和Cookie设置结果有所不同，具体取决于其配置的值。

请参阅下表，根据同意设置了解何时进行数据收集以及何时设置Cookie。

| defaultconsent | setConsent | 发生数据收集 | Web SDK设置浏览器Cookie |
|---------|----------|---------|---------|
| `in` | `in` | 是 | 是 |
| `in` | `out` | 否 | 是 |
| `in` | 未设置 | 是 | 是 |
| `pending` | `in` | 是 | 是 |
| `pending` | `out` | 否 | 是 |
| `pending` | 未设置 | 否 | 否 |
| `out` | `in` | 是 | 是 |
| `out` | `out` | 否 | 是 |
| `out` | 未设置 | 否 | 否 |

在同意配置允许时设置以下Cookie：

| 名称 | 最大年龄 | 描述 |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000（395天） | 前提条件 [`idMigrationEnabled`](../configure/idmigrationenabled.md) 已启用。 当站点的某些部分仍在使用时，在过渡到Web SDK时非常有用 `visitor.js`. |
| **Demdex Cookie** | 15552000（180天） | 如果启用了ID同步，则会显示。 Audience Manager通过设置此Cookie来向网站访客分配唯一ID。 demdex Cookie可帮助Audience Manger执行基本的功能，例如访客识别、ID同步、分段、建模和报告等。 |
| **kndctr_orgid_cluster** | 1800（30分钟） | 存储为当前Edge Network提供请求的请求区域。 URL路径中使用区域，以便Edge Network能够将请求路由到正确的区域。 如果用户使用不同的IP地址或以不同的会话连接，则请求将再次路由到最近的区域。 |
| **kndct_orgid_identity** | 34128000（395天） | 存储ECID以及与ECID相关的其他信息。 |
| **kndctr_orgid_consent** | 15552000（180天） | 存储网站的用户同意首选项。 |
| **s_ecid** | 63115200（2年） | 包含Experience CloudID的副本([!DNL ECID])或MID。 MID 存储在一个键值对中，它遵循以下语法：`s_ecid=MCMID\|<ECID>`。 |

## 使用Web SDK标记扩展设置默认同意

在下选择所需的单选按钮 **[!UICONTROL 默认同意]** 时间 [配置标记扩展](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下滚动到 [!UICONTROL 隐私] 部分，然后选择所需的 **[!UICONTROL 默认同意]**.
1. 单击 **[!UICONTROL 保存]**，然后发布更改。

## 使用Web SDK JavaScript库设置默认同意

设置 `defaultConsent` 字符串属性达到所需的同意级别 `configure` 命令。 此属性区分大小写，并且仅支持以下三个值： `"in"`， `"out"`、和 `"pending"`. 如果尝试使用任何其他值，则库会引发错误。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
