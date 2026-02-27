---
title: 监控批量查询许可证使用情况
description: Adobe Experience Platform UI提供了一个功能板，通过该功能板，您可以查看有关贵组织的Data Distiller许可证使用情况的重要信息。
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: dce631923bd38f3237da3e1928e2203dc1a266ca
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# 监测批量查询许可证使用情况 {#monitor-license-usage}

许可证使用情况仪表板提供有关贵组织的查询服务许可证使用情况以及每个已购产品的使用情况指标的精细报告。 若要了解有关仪表板中显示的可用量度的更多信息，请访问[许可证使用情况仪表板指南](../../dashboards/guides/license-usage.md#available-metrics)。

仪表板提供每个购买产品的使用情况量度、所有生产或开发沙盒中量度的综合使用情况，以及特定沙盒的使用情况量度。 此处显示的信息是在Experience Platform实例的每日快照期间捕获的。 管理员可以监视和结束空闲的查询服务会话，以便在没有其他会话可用以及用户因空闲（非活动）会话而被阻止时释放容量。 有关详细信息，请参阅[管理查询服务会话](../ui/session-management.md)。

>[!NOTE]
>
>默认情况下，许可证使用情况仪表板未启用。 必须向用户授予“查看许可证使用情况仪表板”权限，用户才能查看仪表板。 有关授予查看许可证使用仪表板的访问权限的步骤，请参阅[仪表板权限指南](../../dashboards/permissions.md)。

## 计算小时数 {#compute-hours}

[!UICONTROL Compute hours]量度仅适用于具有Data Distiller许可证的客户以进行批量查询。 [!UICONTROL Compute hours]是查询服务引擎在执行批处理查询时读取、处理数据并将其写回数据湖所花费的时间度量。

![已突出显示计算小时量度的许可证使用情况仪表板。](../images/data-distiller/compute-hours.png)

要根据贵组织购买的许可证查找有关贵组织可用量度的更多信息，请参阅[许可证使用情况仪表板指南](../../dashboards/guides/license-usage.md)。
