---
keywords: Experience Platform；主页；热门主题；API;API;XDM;XDM系统；体验数据模型；数据模型；UI；工作区；枚举；字段；
solution: Experience Platform
title: 在UI中定义枚举字段
description: 了解如何在Experience Platform用户界面中定义枚举字段。
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: 878d99d9eb45f40ff76e5e90116abf032be1c93f
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---

# 在UI中定义枚举字段 {#enum}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="枚举和建议值"
>abstract="枚举将约束字符串字段，以便仅允许摄取与预定义值集匹配的数据。 或者，您可以为字段定义一组建议的值，这些值不限制摄取，而是定义可在分段中选择的属性。 有关详细信息，请参阅文档。"

在体验数据模型(XDM)中，枚举字段表示一个受预定义可接受值列表约束的字段。

When [定义新字段](./overview.md#define) 在Adobe Experience Platform用户界面中，您可以通过选择 **[!UICONTROL 枚举]** 复选框。

![](../../images/ui/fields/special/enum.png)

选中复选框后会显示其他控件，允许您指定枚举的值约束。 在 **[!UICONTROL 值]** 列中，您必须提供要将字段限制为的确切值。 此值必须符合 [!UICONTROL 类型] 为枚举字段选择了。 您可以选择提供人性化的 **[!UICONTROL 标签]** 也是约束。

要向枚举添加其他约束，请选择 **[!UICONTROL 添加行]**.

![](../../images/ui/fields/special/enum-add-row.png)

继续向枚举中添加所需的约束和可选标签。 完成后，选择 **[!UICONTROL 应用]** 以将更改应用到架构。

![](../../images/ui/fields/special/enum-configured.png)

画布会更新以反映所做的更改。 将来浏览此架构时，您可以在右边栏中查看和编辑枚举字段的约束。

![](../../images/ui/fields/special/enum-applied.png)

## 后续步骤

本指南介绍如何在UI中定义枚举字段。 请参阅 [在UI中定义字段](./overview.md#special) 了解如何在 [!DNL Schema Editor].
