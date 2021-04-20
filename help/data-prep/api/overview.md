---
keywords: Experience Platform；数据准备；数据准备api；疑难解答；API
title: 数据准备API概述
topic: guide
description: 数据准备API允许您以编程方式创建映射集和函数，从而在源模式和目标应用程序之间转换数据。
translation-type: tm+mt
source-git-commit: cae6dc80d0394db51dc97478b92459be64c64498
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---


# 映射服务API指南

数据准备使数据工程师能够映射、转换和验证数据到体验数据模型(XDM)和从体验数据模型(XDM)的数据。 数据准备在包括CSV摄取工作流在内的数据摄取过程中显示为“映射”步骤。

映射服务API（也称为数据准备API）包括以下概述的多个端点。 请访问各个端点指南以了解详细信息，并参阅[快速入门指南](./getting-started.md)，了解有关所需标头、读取示例API调用等的重要信息。

## 函数

映射集函数允许您在源模式和目标应用程序之间转换数据。 您可以使用`/languages/el`端点验证表达式，并获取所有可用映射集函数和操作的列表。

有关如何使用映射集函数的详细信息，请阅读[函数端点指南](./functions.md)。

## 映射集

映射集可用于定义源模式中的数据如何映射到目标模式。 您可以使用数据准备API中的`/mappingSets`端点以编程方式检索、创建、更新和验证映射集。

有关如何使用映射集的详细信息，请阅读[映射集端点指南](./mapping-set.md)。

## 后续步骤

要开始使用映射服务API进行调用，请阅读[快速入门指南](./getting-started.md)，然后选择一个端点指南来了解如何使用特定端点。