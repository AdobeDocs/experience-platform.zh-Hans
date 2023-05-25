---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；必需；字段；
title: 在UI中定义必填字段
description: 了解如何在Experience Platform用户界面中定义必需的XDM字段。
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 在UI中定义必填字段

在Experience Data Model (XDM)中，必填字段指示必须提供有效值，才能在数据摄取期间接受特定记录或时间序列事件。 必填字段的常见用例包括用户身份信息和时间戳。

>[!IMPORTANT]
>
>无论是否要求架构字段，平台都不接受 `null` 或任何引入的字段的值为空。 如果记录或事件中的特定字段没有值，则应从摄取有效负载中排除该字段的键。

时间 [定义新字段](./overview.md#define) 在Adobe Experience Platform用户界面中，您可以通过选择 **[!UICONTROL 必需]** 复选框。 选择 **[!UICONTROL 应用]** 以将更改应用于架构。

![“必需”复选框](../../images/ui/fields/required/root.png)

如果字段是租户ID对象下的根级别属性，则其路径立即显示在下 **[!UICONTROL 必填字段]** 在左边栏中。

![根级别必填字段](../../images/ui/fields/required/applied.png)

但是，如果某个必填字段嵌套在未标记为必填对象的对象中，则该嵌套字段不会显示在下方 **[!UICONTROL 必填字段]** 在左边栏中。

在以下示例中， `internalSKU` 字段已设置为必需，但其父对象 `SKUs` 不是。 在这种情况下，如果符合以下条件，将不会发生验证错误 `SKUs` 摄取数据时将被排除，即使子字段也是如此 `internalSKU` 标记为必需。 换言之，当 `SKUs` 是可选的，必须包含 `internalSKU` 字段中显示的值。

![嵌套必填字段](../../images/ui/fields/required/nested.png)

如果您希望架构中始终需要嵌套字段，则还必须根据需要设置所有父字段（租户ID对象除外）。

![父项和子项必填字段](../../images/ui/fields/required/parent-and-child.png)

## 后续步骤

本指南介绍了如何在UI中定义必填字段。 请参阅概述，位于 [在UI中定义字段](./overview.md#special) 了解如何在中定义其他XDM字段类型 [!DNL Schema Editor].
