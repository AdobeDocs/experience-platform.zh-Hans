---
title: 傳送加速查詢
description: 加速查詢API的簡介。
exl-id: c6cd1182-d3a9-457f-81d5-18027e47c3f9
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# 傳送加速的查詢

在Data Distiller SKU中， [查詢服務API](https://developer.adobe.com/experience-platform-apis/references/query-service/) 可讓您對加速存放區進行無狀態查詢。 此 [加速的查詢端點](https://developer.adobe.com/experience-platform-apis/references/query-service/#tag/Accelerated-Queries) 會根據彙總的資料傳回結果，以減少結果的等待時間，並提供互動性更強的資訊交換。

請參閱 [加速查詢端點](../../api/accelerated-queries.md) 有關如何查詢accelerated store的說明檔案。

使用query accelerated store ，您可以建立自訂資料模型和/或擴充現有的Adobe Real-time Customer Data Platform資料模型。 若要與報表/視覺效果架構互動或將您的報表深入解析內嵌於其中，請參閱 [query accelerated store報告見解指南](./reporting-insights-data-model.md). 您也可以閱讀Real-time Customer Data Platform Insights資料模型檔案，以瞭解如何 [自訂SQL查詢範本，為您的行銷和關鍵績效指標(KPI)使用案例建立Real-Time CDP報表](../../../dashboards/cdp-insights-data-model.md). 您可以使用 [屬性型存取控制功能](../../../access-control/abac/overview.md)，可控制加速存放區中資料集的限制等級。 請參閱 [查詢服務中的資料控管](../../data-governance/overview.md#create-field-based-access-restrictions-on-accelerated-datasets)
檔案以取得詳細資訊。
