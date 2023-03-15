---
title: 数据Distiller概述
description: 与您的授权许可相关的查询服务数据的Distiller使用限制摘要。
source-git-commit: ae4ecd43071a198592193a1a598a064cdc6be2f6
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 数据Distiller概述

Data Distiller是一款产品包，其中包含Adobe Experience Platform功能的子集。 借助Data Distiller，您可以通过在查询服务中执行批量查询，为实时客户资料或分析用例执行摄取后数据准备（例如清理、整形和操作）。 您对Data Distiller的使用取决于您对基于平台的应用程序的授权。

## 许可证使用 {#license-usage}

的  [数据Distiller许可证使用功能板](./license-usage.md) 在您购买了数据Distiller计算小时数后，即可使用。 许可证使用功能板可帮助您监控授权计算小时数的使用情况。 请参阅 [数据Distiller许可证使用文档](./license-usage.md) 查看有关贵组织查询服务许可证使用情况的重要信息。

<!-- Update these descriptions post 23.3 release
## Scoping parameters {#scoping-parameters}

Scoping parameters are usage limits that relate to the scoping of your required set up, and are defined by your license capacity. Without add-ons, Data Distiller's scoping parameters are as follows: 

* **Compute Hours**: You can use PSQL or the Query Service API to run batch queries executed in any sandbox (scheduled or otherwise) to scan and write data. This uses your allotted Compute Hours per year as determined in the scoping process of your license agreement. Total Compute Hours is accumulated across all Sandboxes.
* **Data Ingested**: The data ingested into Adobe Experience Platform which can be queried using Data Distiller is subject to the limitations described in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer.
* **Data Lake Storage**: The data lake storage provided in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Data Lake Storage is a shared feature.
* **Query Service Users**: The number of Query Service users detailed in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Query Service Users is a shared feature. 
-->

## 护栏

请参阅 [查询服务护栏](../guardrails.md) 有关与您的许可授权相关的查询服务数据的默认使用限制的文档。

<!-- Update these descriptions post 23.3 release
## Static limits

A static limit is the usage limit that relates to the functional boundaries of Adobe Experience Platform Activation. [More information on Adobe Experience Platform Activation](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) can be found in the Adobe help documents. A summary of Data Distiller static limits are listed below, for more complete information please refer to the Query Service guardrail document.  

* **Batch Queries**: Scheduled batch queries time out after 24 hours.
* **Query Service**: You can use Query Service for the following purposes: 
    * To run SQL queries for data analysis and post ingestion data preparation (cleaning, shaping, and manipulation).
    * To run SQL queries to create roll-up metrics to surface directly into a BI tool.
    * To quickly inspect data within Adobe Experience Platform.
    * To generate meaningful insights from your data.
* **Reporting API Call**: To ensure queries run on aggregated data using the reporting API have enough resources to execute efficiently. This includes queries that enhance existing data models such as those provided by Real-Time Customer Data Platform. The reporting API tracks resource utilization by assigning concurrency slots to each query. A maximum of four reporting API calls are available concurrently. If you access the reporting API through a BI tool and require more concurrency slots, a BI server is required.
-->

