---
keywords: Experience Platform；主页；热门主题；数据流；数据流；数据；监控；监控数据流；监控数据流；监控；监控数据流；监控数据流；流；流服务；
solution: Experience Platform
title: 数据流概述
description: 本文档介绍了数据流，并阐述了它们在Adobe Experience Platform中的使用方式。
exl-id: 8fe08ffa-f095-4e9f-8bab-d060985f0236
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 5%

---

# 数据流概述

在Adobe Experience Platform中，数据从各种来源摄取，在Experience Platform中进行分析，并激活到各种目的地。 Platform通过提供数据流透明性，使跟踪这种潜在非线性数据流的过程更加容易。

## 使用数据流

数据流是跨平台移动数据的数据作业的表示方法。这些数据流在不同的服务中配置，有助于将数据从源连接器移动到目标数据集，然后在最终激活到目标之前，身份服务和实时客户资料将在目标数据集中使用这些数据。

要了解有关在源连接器中使用数据流的更多信息，请阅读 [源概述](../sources/home.md).

## 正在准备数据

数据准备允许数据工程师映射、转换和验证数据到体验数据模型(XDM)以及从中转换和验证数据。

要了解有关在摄取数据后准备数据的更多信息，请阅读 [数据准备概述](../data-prep/home.md).

## 监控数据流

可以使用Platform API或Platform UI监控数据流。 要了解如何使用API监控数据流，请阅读 [监控数据流API教程](./api/monitor.md). 要了解如何在Platform UI中监控数据流，请阅读上的教程 [监控源的数据流](./ui/monitor-sources.md) 和 [监控目标的数据流](./ui/monitor-destinations.md).
