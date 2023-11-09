---
title: 监控批量查询许可证使用情况
description: Adobe Experience Platform UI提供了一个功能板，通过该功能板，您可以查看有关贵组织的Data Distiller许可证使用情况的重要信息。
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
recommendations: noCatalog, display
source-git-commit: e55cada0975d771f225e829aeeeeeeb64b9acf4a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 监测批量查询许可证使用情况 {#monitor-license-usage}

许可证使用情况仪表板提供有关贵组织的查询服务许可证使用情况以及每个已购产品的使用情况指标的精细报告。 要了解有关仪表板中显示的可用量度的更多信息，请访问 [许可证使用情况仪表板指南](../../dashboards/guides/license-usage.md#available-metrics).

仪表板提供每个购买产品的使用情况量度、所有生产或开发沙盒中量度的综合使用情况，以及特定沙盒的使用情况量度。 此处显示的信息是在Platform实例的每日快照期间捕获的。

>[!NOTE]
>
>默认情况下，许可证使用情况仪表板未启用。 必须向用户授予“查看许可证使用情况仪表板”权限，用户才能查看仪表板。 有关授予查看许可证使用仪表板的访问权限的步骤，请参阅 [仪表板权限指南](../../dashboards/permissions.md).

## 计算小时数 {#compute-hours}

此 [!UICONTROL 计算小时数] 量度仅适用于具有Data Distiller许可证进行批量查询的客户。 [!UICONTROL 计算小时数] 是测量在执行批量查询时，查询服务引擎读取、处理数据并将其写回数据湖所花费的时间。

>[!NOTE]
>
>**数据可用，但存在限制**：数据从2023年10月1日开始，没有趋势。<br>此 **回填** 从您的合同开始日期开始的数据的工作正在进行中。 预计在日历年年底之前可用。

![突出显示计算小时量度的许可证使用情况仪表板。](../images/data-distiller/compute-hours.png)

要根据贵组织购买的许可证查找有关可用于贵组织的量度的更多信息，请参阅 [许可证使用情况仪表板指南](../../dashboards/guides/license-usage.md).
