---
keywords: Experience Platform；主页；热门主题；API;API;XDM;XDM系统；体验数据模型；数据模型；UI；工作区；必填；字段；
title: 在UI中定义必填字段
description: 了解如何在Experience Platform用户界面中定义必需的XDM字段。
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: 11dcb1a824020a5b803621025863e95539ab4d71
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 在UI中定义必填字段

在体验数据模型(XDM)中，必填字段指示必须为其提供有效值，以便在数据摄取期间接受特定记录或时间系列事件。 必填字段的常见用例包括用户身份信息和时间戳。

>[!IMPORTANT]
>
>无论架构字段是否为必填字段，Platform都不接受 `null` 或任何摄取的字段的空值。 如果记录或事件中特定字段没有值，则应从摄取有效负载中排除该字段的键。

When [定义新字段](./overview.md#define) 在Adobe Experience Platform用户界面中，您可以通过选择 **[!UICONTROL 必需]** 复选框。 选择 **[!UICONTROL 应用]** 将更改应用到架构。

![“必需”复选框](../../images/ui/fields/required/root.png)

如果字段是租户ID对象下的根级别属性，则其路径会立即显示在 **[!UICONTROL 必填字段]** 中。

![根级别必填字段](../../images/ui/fields/required/applied.png)

但是，如果必填字段嵌套在未标记为必填字段的对象中，则嵌套的字段不会显示在 **[!UICONTROL 必填字段]** 中。

在以下示例中， `loyaltyId` 字段，但其父对象 `loyalty` 不是。 在这种情况下，如果 `loyalty` 在摄取数据时被排除，即使子字段也是如此 `loyaltyId` 标记为必需。 换句话说， `loyalty` 可选，它必须包含 `loyaltyId` 字段。

![嵌套的必填字段](../../images/ui/fields/required/nested.png)

如果您希望架构中始终需要嵌套字段，则还必须根据需要设置所有父字段（租户ID对象除外）。

![父和子必填字段](../../images/ui/fields/required/parent-and-child.png)

## 后续步骤

本指南介绍了如何在UI中定义必填字段。 请参阅 [在UI中定义字段](./overview.md#special) 了解如何在 [!DNL Schema Editor].
