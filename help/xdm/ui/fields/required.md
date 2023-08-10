---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；必需；字段；
title: 在UI中定义必填字段
description: 了解如何在Experience Platform用户界面中定义必需的XDM字段。
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# 在UI中定义必填字段

在Experience Data Model (XDM)中，必填字段指示必须为它提供有效值，才能在数据摄取期间接受特定记录或时间序列事件。 必填字段的常见用例包括用户身份信息和时间戳。

>[!IMPORTANT]
>
>无论是否需要架构字段，Platform都不会接受 `null` 或任何引入的字段的值为空。 如果记录或事件中没有特定字段的值，则应该从摄取有效负载中排除该字段的键。

时间 [定义新字段](./overview.md#define) 在Adobe Experience Platform用户界面中，您可以通过选择 **[!UICONTROL 必填]** 复选框。 选择 **[!UICONTROL 应用]** 将更改应用于架构。

![“必需”复选框](../../images/ui/fields/required/root.png)

如果字段是租户ID对象下的根级别属性，则其路径立即显示在下 **[!UICONTROL 必填字段]** 在左边栏中。

![根级别必填字段](../../images/ui/fields/required/applied.png)

但是，如果必填字段嵌套在未标记为必填对象的对象中，则嵌套字段不会显示在下方 **[!UICONTROL 必填字段]** 在左边栏中。

在以下示例中， `internalSKU` 字段已设置为必填，但其父对象 `SKUs` 不是。 在这种情况下，如果在以下情况下，将不会发生验证错误： `SKUs` 摄取数据时将被排除，即使子字段也是如此 `internalSKU` 标记为必需。 换言之，当 `SKUs` 是可选的，它必须包含 `internalSKU` 字段。

![嵌套必填字段](../../images/ui/fields/required/nested.png)

如果您希望架构中始终需要嵌套字段，则还必须根据需要设置所有父字段（租户ID对象除外）。

![父必填字段和子必填字段](../../images/ui/fields/required/parent-and-child.png)

## 后续步骤

本指南介绍了如何在UI中定义必填字段。 有关更多详细信息，请参阅 [在UI中定义字段](./overview.md#special) 了解如何在中定义其他XDM字段类型 [!DNL Schema Editor].
