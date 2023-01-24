---
title: 监控批量查询许可证使用情况
description: Adobe Experience Platform UI提供了一个功能板，您可以通过该功能板查看有关贵组织的Data Distiller许可证使用情况的重要信息。
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# （测试版）监控批量查询许可证的使用情况 {#monitor-license-usage}

>[!IMPORTANT]
>
>测试版中提供了通过UI监控批量查询许可证使用情况的功能。 其功能和文档可能会发生更改。

Adobe Experience Platform用户界面(UI)提供了一个功能板，您可以通过该功能板查看有关贵组织查询服务许可证使用情况的重要信息。

有关如何访问UI中的许可证使用功能板并与之交互，以及了解有关该功能板中显示的可用量度的更多信息，请访问 [许可证使用仪表板指南](../../dashboards/guides/license-usage.md).

请阅读 [功能板概述](../../dashboards/home.md) 以概要了解Experience Platform中的所有功能板功能。

## 小组件 {#widgets}

许可证使用功能板由小组件组成，这些小组件显示只读量度，提供有关贵组织许可证使用情况的重要信息。 可见量度取决于贵组织的特定许可。

选择一个单选按钮以选择用于分析的沙盒，然后使用下拉菜单选择分析的时间段。 可用选项包括30天、90天、12个月期间、最后一年、完整合同期或自定义日期。

## 计算小时数 {#compute-hours}

的 [!UICONTROL 计算小时数] 小组件每天使用折线图来可视化组织的批量查询处理时间。 小组件在小组件的左上角显示三个由数字表示的量度。 这些是

- [!UICONTROL 实际]:在概述下拉菜单中选择的时间段的总计计算小时数。 此量度还在图表上以实线表示。
- [!UICONTROL 许可]:贵组织的许可协议允许的计算小时数总数。 此量度还通过虚线在图表上指示。
- [!UICONTROL 使用情况]:这是您的使用量相对于许可证商定的最大计算小时数的百分比。

>[!IMPORTANT]
>
>的 [!UICONTROL 计算小时数] 小组件仅适用于拥有Data Distiller批量查询许可证的客户。

![突出显示了“计算时间”小组件的许可证使用功能板。](../images/data-distiller/compute-hours.png)
