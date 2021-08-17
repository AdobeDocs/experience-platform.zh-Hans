---
keywords: Experience Platform；主页；热门主题；映射CSV；映射CSV文件；将CSV文件映射到XDM；将CSV映射到XDM;UI指南；映射；数据准备；数据准备；准备数据；
solution: Experience Platform
title: 数据准备概述
topic-legacy: overview
description: 本文档介绍了Adobe Experience Platform中的数据准备。
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: 2cc72708b77396e70d006ecd1e21fd2d495ddf61
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---


# 计算字段

计算量度字段允许根据输入架构中的属性创建值。 然后，可以将这些值分配给目标架构中的属性，并提供名称和说明，以便更便于引用。

要创建计算字段，请选择&#x200B;**[!UICONTROL 添加计算字段]**。

![](./images/calculated-fields/add-calculated-field.png)

出现&#x200B;**[!UICONTROL 创建计算字段]**&#x200B;面板。 左侧对话框包含计算字段中支持的字段、函数和运算符。 选择一个选项卡以开始向表达式编辑器添加函数、字段或运算符。

![](./images/calculated-fields/create-calculated-field.png)

| 选项卡 | 描述 |
| --- | ----------- |
| 函数 | 函数选项卡列出了可用于转换数据的函数。 要进一步了解可在计算字段中使用的函数，请阅读[上使用数据准备（映射器）函数](./functions.md)的指南。 |
| 字段 | 字段选项卡列出了源架构中可用的字段和属性。 |
| 运算符 | 运算符选项卡列出了可用于转换数据的运算符。 |

您可以使用中心的表达式编辑器手动添加字段、函数和运算符。 选择编辑器以开始创建表达式。

![](./images/calculated-fields/write-calculated-field.png)

选择&#x200B;**[!UICONTROL 保存]**&#x200B;以继续。

映射屏幕将重新显示您新创建的源字段。 应用相应的目标字段并选择&#x200B;**[!UICONTROL 完成]**&#x200B;以完成映射。

![](./images/calculated-fields/new-calculated-field.png)