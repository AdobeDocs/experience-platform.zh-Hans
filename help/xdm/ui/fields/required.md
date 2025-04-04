---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；必需；字段；
title: 在UI中定义必填字段
description: 了解如何在Experience Platform用户界面中定义必需的XDM字段。
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 在UI中定义必填字段

在Experience Data Model (XDM)中，必填字段指示必须为它提供有效值，才能在数据摄取期间接受特定记录或时间序列事件。 必填字段的常见用例包括用户身份信息和时间戳。

>[!IMPORTANT]
>
>无论是否需要架构字段，Experience Platform都不会接受任何已摄取字段的`null`或空值。 如果记录或事件中没有特定字段的值，则应该从摄取有效负载中排除该字段的键。

在Adobe Experience Platform用户界面中[定义新字段](./overview.md#define)时，您可以通过选中右边栏中的&#x200B;**[!UICONTROL 必填]**&#x200B;复选框将其设置为必填字段。 选择&#x200B;**[!UICONTROL 应用]**&#x200B;以将更改应用于架构。

![必需复选框](../../images/ui/fields/required/root.png)

如果字段是租户ID对象下的根级别属性，则其路径会立即显示在左边栏中的&#x200B;**[!UICONTROL 必填字段]**&#x200B;下。

![根级必填字段](../../images/ui/fields/required/applied.png)

但是，如果某个必填字段嵌套在未标记为必填对象的对象中，则该嵌套字段不会出现在左边栏中的&#x200B;**[!UICONTROL 必填字段]**&#x200B;下。

在以下示例中，`internalSKU`字段设置为必填，但其父对象`SKUs`不是。 在这种情况下，如果在摄取数据时排除`SKUs`，即使子字段`internalSKU`标记为必需，也不会发生验证错误。 换言之，尽管`SKUs`是可选的，但它必须在其包含的事件中包含一个`internalSKU`字段。

![嵌套必填字段](../../images/ui/fields/required/nested.png)

如果您希望架构中始终需要嵌套字段，则还必须根据需要设置所有父字段（租户ID对象除外）。

![父必填字段和子必填字段](../../images/ui/fields/required/parent-and-child.png)

## 后续步骤

本指南介绍了如何在UI中定义必填字段。 请参阅[在UI](./overview.md#special)中定义字段的概述，了解如何在[!DNL Schema Editor]中定义其他XDM字段类型。
