---
keywords: Experience Platform；主页；热门主题；map csv;map csv;map csv文件；map csv文件到xdm;map csv到xdm;ui指南；mapper;mapping;data preparation;data preparation;preparing data;
solution: Experience Platform
title: 数据准备概述
topic: overview
description: 本文档介绍Adobe Experience Platform中的数据准备。
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
translation-type: tm+mt
source-git-commit: 827a593c046530edba701edf26d9a47918cfd8f8
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 1%

---


# 数据准备概述

数据准备使数据工程师能够映射、转换和验证数据到体验数据模型(XDM)和从体验数据模型(XDM)的数据。 数据准备在包括CSV摄取工作流在内的数据摄取过程中显示为“映射”步骤。 数据工程师可以使用数据准备功能在获取过程中执行以下数据操作：

- 定义简单的传递映射，以将输入属性分配给XDM属性
- 创建计算字段以执行可分配给XDM属性的行内计算
- 通过应用字符串、数字或日期处理函数转换数据
- 使用层次函数构造XDM层次
- 预览数据在数据准备中处理时的数据

数据准备还应用若干内在数据验证，以确保在摄取数据时保持数据完整性。 如果可能，数据准备会自动将传入的数据模式映射到XDM。 数据工程师可以更改、更正和删除建议的映射，并根据需要用映射替换它们。

## 映射

映射是输入属性或计算字段与一个XDM属性的关联。 单个属性可以通过创建单个映射映射到多个XDM属性。

要了解有关不同映射函数的详细信息，请阅读[映射函数指南](./functions.md)。

## 映射集

将一个模式转换为另一个映射的一组映射统称为映射集。 将创建单个映射集作为每个数据流的一部分。 映射集是数据流的一个组成部分，并且作为数据流的一部分被创建、编辑和监视。

## 数据格式处理

数据准备功能可以可靠地处理引入平台的不同格式数据。 要了解有关数据准备如何处理不同数据类型的更多信息，请阅读[数据格式处理概述](./data-handling.md)。

## 后续步骤

本文档介绍了Adobe Experience Platform中数据准备的基础知识。 要了解有关不同映射函数的详细信息，请阅读[映射函数指南](./functions.md)。 要了解有关数据准备如何处理不同数据类型的更多信息，请阅读[数据格式处理指南](./data-handling.md#dates)。 要了解如何使用数据准备API，请阅读[数据准备开发人员指南](api/overview.md)。
