---
title: 在UI中定义映射字段
description: 了解如何在Experience Platform用户界面中定义映射字段。
exl-id: 657428a2-f184-4d7c-b657-4fc60d77d5c6
source-git-commit: c0421974493884488e4d639278106835ad1d8b1b
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# 在UI中定义映射字段

Adobe Experience Platform允许您完全自定义自定义Experience Data Model (XDM)类、架构字段组和数据类型的结构。

您还可以在架构编辑器中定义映射字段，以使用灵活的动态键存储键值对的集合。

在Experience Platform用户界面(UI)中定义新字段时，请使用&#x200B;**[!UICONTROL 类型]**&#x200B;下拉列表，然后从列表中选择“**[!UICONTROL 映射]**”。

![模式编辑器的“类型”下拉列表和映射值突出显示。](../../images/ui/fields/special/map.png)

出现[!UICONTROL 映射值类型]属性。 [!UICONTROL 映射]数据类型需要此值。 映射的可用值为[!UICONTROL 字符串]和[!UICONTROL 整数]。 从可用选项的下拉列表中选择一个值。

![突出显示具有[!UICONTROL 映射值类型]下拉列表的架构编辑器。](../../images/ui/fields/special/map-value-type.png)

配置子字段后，必须将其分配给字段组。 使用&#x200B;**[!UICONTROL 字段组]**&#x200B;下拉菜单或搜索字段，然后选择&#x200B;**[!UICONTROL 应用]**。 您可以使用相同的过程继续向对象添加字段，或选择&#x200B;**[!UICONTROL 保存]**&#x200B;以确认设置。

![正在应用的字段组选择和设置的录制。](../../images/ui/fields/special/assign-to-field-group.gif)

## 使用限制 {#restrictions}

XDM对此数据类型的使用施加以下限制：

* 映射类型必须是`object`类型。
* 映射类型不能定义属性（换句话说，它们定义“空”对象）。
* 映射类型必须包含描述可以放置在映射中的值的`additionalProperties.type`字段，即`string`或`integer`。
* 多实体分段只能基于映射键而不是值定义。
* 帐户受众不支持映射。
* 在自定义XDM对象中定义的映射被限制在单个级别。 无法创建嵌套映射。 此限制不适用于标准XDM对象中定义的映射。
* 不支持映射数组。

确保仅在绝对必要时使用映射类型字段，因为它们存在以下性能缺陷：

* 来自[Adobe Experience Platform查询服务](../../../query-service/home.md)的响应时间从3秒降至10秒，涉及1亿条记录。
* 地图必须少于16个键，否则可能会进一步降级。

>[!NOTE]
>
>Experience Platform UI在如何提取映射类型字段的键值方面存在限制。 虽然对象类型字段可以展开，但映射显示为一个字段。 通过架构注册表API创建的不是字符串或整数数据类型的映射字段显示为“[!UICONTROL 复杂]”数据类型。

## 后续步骤

阅读本文档后，您现在可以在Experience Platform UI中定义映射字段。 请记住，您只能使用类和字段组向架构添加字段。 要详细了解如何在UI中管理这些资源，请参阅有关创建和编辑[类](../resources/classes.md)和[字段组](../resources/field-groups.md)的指南。

有关[!UICONTROL 架构]工作区的功能的更多信息，请参阅[[!UICONTROL 架构]工作区概述](../overview.md)。
