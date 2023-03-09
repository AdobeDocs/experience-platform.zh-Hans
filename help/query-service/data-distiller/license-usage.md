---
title: 监控批量查询许可证使用情况
description: Adobe Experience Platform UI提供了一个功能板，通过该功能板，您可以查看有关组织的Data Distiller许可证使用情况的重要信息。
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: a1c5b687108a9fc8729008e2b0e39ec6b1842f54
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# (Alpha)监控批量查询许可证使用情况 {#monitor-license-usage}

>[!IMPORTANT]
>
>尚不允许所有用户通过UI监控批量查询许可证使用情况。 此功能处于Alpha阶段，并且仍在测试中。 此文档可能会发生更改。

Adobe Experience Platform用户界面(UI)提供了一个仪表板，通过它可查看有关贵组织的查询服务许可证使用情况的重要信息。

有关如何在UI中访问许可证使用情况仪表板并与之交互的详细说明，以及了解仪表板中显示的可用量度的更多信息，请访问 [许可证使用情况仪表板指南](../../dashboards/guides/license-usage.md).

请阅读 [功能板概述](../../dashboards/home.md) 有关Experience Platform中所有功能板功能的摘要。

## 小组件 {#widgets}

许可证使用情况仪表板由小组件组成，这些小组件显示只读量度，提供有关您组织的许可证使用情况的重要信息。 可见的量度取决于贵组织的特定许可。

选择一个单选按钮以选择要分析的沙盒，然后使用下拉菜单选择分析的时间段。 可用的选项包括30天、90天、12个月期间、上一年、完整合同期间或自定义日期。

## 计算小时数 {#compute-hours}

此 [!UICONTROL 计算小时数] 构件使用折线图将贵组织的批处理查询每天的处理时间可视化。 构件在左上角显示三个由数字表示的量度。 这些是

- [!UICONTROL 实际]：在概述下拉菜单中选择的时段的总计算小时数。 此量度在图表中还以实线表示。
- [!UICONTROL 已许可]：贵组织的许可协议允许的计算小时总数。 此量度还用虚线表示在图表中。
- [!UICONTROL 使用情况]：这是您的使用量相对于您的许可证所同意的最大计算小时数的百分比。

>[!IMPORTANT]
>
>此 [!UICONTROL 计算小时数] 构件仅适用于拥有Data Distiller许可证的客户以进行批量查询。

![突出显示计算小时数小部件的许可证使用情况仪表板。](../images/data-distiller/compute-hours.png)
