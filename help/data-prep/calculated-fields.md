---
keywords: Experience Platform；主页；热门主题；映射csv；映射csv文件；将csv文件映射到xdm；将csv映射到xdm；ui指南；映射器；映射；数据准备；数据准备；准备数据；
solution: Experience Platform
title: 数据准备概述
description: 本文档介绍Adobe Experience Platform中的数据准备。
exl-id: 9bef5c3b-368d-4492-bdef-64e67fc25bfd
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---

# 计算字段

计算字段允许根据输入架构中的属性创建值。 然后，可以将这些值分配给目标架构中的属性，并提供名称和描述以便更轻松地引用。

要创建计算字段，请选择&#x200B;**[!UICONTROL 添加计算字段]**。

![](./images/calculated-fields/add-calculated-field.png)

此时将显示&#x200B;**[!UICONTROL 创建计算字段]**&#x200B;面板。 左侧对话框包含计算字段中支持的字段、函数和运算符。 选择其中一个选项卡，开始向表达式编辑器添加函数、字段或运算符。

![](./images/calculated-fields/create-calculated-field.png)

| 选项卡 | 描述 |
| --- | ----------- |
| 函数 | 函数选项卡列出了可用于转换数据的函数。 若要了解有关可在计算字段中使用的函数的更多信息，请阅读有关[使用数据准备（映射器）函数](./functions.md)的指南。 |
| 字段 | 字段选项卡列出了源架构中可用的字段和属性。 |
| 操作员 | 运算符选项卡列出了可用于转换数据的运算符。 |

您可以使用位于中心的表达式编辑器手动添加字段、函数和运算符。 选择编辑器以开始创建表达式。

![](./images/calculated-fields/write-calculated-field.png)

选择&#x200B;**[!UICONTROL 保存]**&#x200B;以继续。

此时会重新显示映射屏幕，其中包含新创建的源字段。 应用相应的目标字段并选择&#x200B;**[!UICONTROL 完成]**&#x200B;以完成映射。

![](./images/calculated-fields/new-calculated-field.png)
