---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;data prep;data preparation;preparing data;
solution: Experience Platform
title: 映射函数
topic: overview
description: 本文档介绍Adobe Experience Platform的数据准备。
translation-type: tm+mt
source-git-commit: db38f0666f5c945461043ad08939ebda52c21855
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 数据准备

数据准备使数据工程师能够映射、转换数据并验证数据与体验数据模型(XDM)之间的关系。 数据准备在数据摄取流程（包括CSV摄取工作流）中显示为“映射”步骤。 数据工程师可以使用数据准备在获取过程中执行以下数据操作：

- 定义简单的传递映射，以将输入属性分配给XDM属性
- 创建计算字段以执行可分配给XDM属性的行内计算
- 通过应用字符串、数字或日期处理函数转换数据
- 使用层次函数构造XDM层次
- 预览数据，因为数据在数据准备中被处理

数据准备还应用多个内在数据验证，以确保在摄取数据时保持数据完整性。 如果可能，数据准备会自动将传入的数据模式映射到XDM。 数据工程师可以更改、更正和删除建议的映射，并视需要将其替换为映射。

## 映射

映射是输入属性或计算字段与一个XDM属性的关联。 单个属性可以通过创建单个映射映射到多个XDM属性。

要进一步了解不同的映射函数，请阅读映 [射函数指南](./functions.md)。

## 映射集

将一个模式转换为另一个映射的映射集统称为映射集。 将创建单个映射集作为每个数据流的一部分。 映射集是数据流的一个组成部分，并作为数据流的一部分被创建、编辑和监视。

## 后续步骤

本文档介绍了Adobe Experience Platform数据准备的基础知识。 要进一步了解不同的映射函数，请阅读映 [射函数指南](./functions.md)。 要进一步了解不同的日期时间字符串，请阅读日 [期字符串指南](./dates.md)。