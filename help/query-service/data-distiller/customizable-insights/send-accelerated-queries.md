---
title: 发送加速查询
description: 关于加速查询API的介绍。
exl-id: c6cd1182-d3a9-457f-81d5-18027e47c3f9
source-git-commit: e0af1f0110ceb514a5b249c42a05bf780ea834c6
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 发送加速查询

作为Data Distiller SKU的一部分， [查询服务API](https://developer.adobe.com/experience-platform-apis/references/query-service/) 允许您对accelerated store进行无状态查询。 此 [加速查询端点](https://developer.adobe.com/experience-platform-apis/references/query-service/#tag/Accelerated-Queries) 基于聚合数据返回结果，这可以缩短结果的等待时间，并提供更具交互性的信息交换。

请参阅 [加速查询端点](../../api/accelerated-queries.md) 有关如何查询accelerated store的说明文档。

使用查询加速存储，您可以构建自定义数据模型和/或扩展现有Adobe Real-time Customer Data Platform数据模型。 要与报表/可视化框架互动或将您的报表见解嵌入到其中，请参阅 [查询accelerated store报告分析指南](./reporting-insights-data-model.md). 您还可以阅读Real-time Customer Data Platform分析数据模型文档以了解如何 [自定义您的SQL查询模板，为您的营销和关键绩效指标(KPI)用例创建Real-Time CDP报表](../../../dashboards/data-models/cdp-insights-data-model-b2c.md). 您可以使用 [基于属性的访问控制功能](../../../access-control/abac/overview.md)，控制对加速存储中数据集的限制级别。 请参阅 [查询服务中的数据治理](../../data-governance/overview.md#create-field-based-access-restrictions-on-accelerated-datasets)
文档，以了解更多信息。
