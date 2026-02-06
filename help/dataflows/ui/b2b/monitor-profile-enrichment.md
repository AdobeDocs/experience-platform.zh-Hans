---
description: 使用[!UICONTROL Profile Enrichment]仪表板了解用户档案扩充作业是否已成功运行和完成，并查看基本量度以衡量扩充的有效性。
solution: Experience Platform
title: 监控配置文件扩充作业
type: Tutorial
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hans#rtcdp-editions" newtab=true
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 0e993f7d0791f5f6f9dce63eb3848609d892e788
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---

# 在UI中监控配置文件扩充作业 {#monitor-profile-enrichment}

使用[!UICONTROL Profile Enrichment]仪表板了解用户档案扩充作业是否已成功运行和完成，并查看基本量度以衡量扩充的有效性。

在[Experience Platform UI](https://platform.adobe.com)中，从左侧导航中选择&#x200B;**[!UICONTROL Monitoring]**&#x200B;以访问[!UICONTROL Monitoring]仪表板。 在视图选择器中，选择&#x200B;**B2B流量**&#x200B;以查看特定于[Real-Time CDP B2B](/help/rtcdp/b2b-overview.md)的仪表板元素。  [!UICONTROL Monitoring]仪表板包括最近一次成功运行的基本量度，以及过去90天内的每日作业状态。

## 相关帐户配置文件扩充 {#related-accounts}

[!UICONTROL Related accounts]仪表板显示特定于[相关帐户](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)配置文件扩充的基本指标和每日作业状态。

![有关如何在Experience Platform UI中访问配置文件扩充作业监视屏幕的可视指示。](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

**[!UICONTROL Metrics]**&#x200B;卡中的数据包括最近成功运行相关帐户作业的基本量度。

以下指标可用于相关帐户配置文件扩充作业：

| 量度 | 描述 |
| --------- | ---------- |
| **[!UICONTROL Total account profiles]** | 指示您的组织有权访问的帐户配置文件总数。 |
| **[!UICONTROL Account groups]** | 指示相关帐户机器学习作业所聚类的帐户组数。 |
| **[!UICONTROL Single-account groups]** | 指示未与其他帐户一起分组的帐户数。 |
| **[!UICONTROL Largest group size]** | 指示最大相关帐户组的大小。 允许的最大组大小为30。 |
| **[!UICONTROL Median group size]** | 指示组织中相关帐户组的大小中位数。 |
| **[!UICONTROL Last successful run]** | 指示上次成功的相关帐户作业运行的日期和时间。 |
| **[!UICONTROL Status]** | 指示相关帐户作业的状态（成功、失败或正在处理）。 |
| **[!UICONTROL Message]** | 指示特定作业运行的错误或警告消息。 |

## 商机帐户匹配配置文件扩充 {#lead-to-account-matching}

[!UICONTROL Lead to account matching]仪表板显示特定于[潜在客户与帐户匹配](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)配置文件扩充的基本量度和每日作业运行状态。

![潜在客户帐户匹配配置文件扩充](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

以下指标可用于商机对帐户匹配配置文件扩充作业：

| 量度 | 描述 |
| --------- | ---------- |
| **[!UICONTROL Total persons with accounts]** | 指示与帐户关联的人员总数。 |
| **[!UICONTROL Total accounts]** | 指示帐户总数。 |
| **[!UICONTROL Existing persons with accounts]** | 指示已与数据源中的帐户关联的人员数。 |
| **[!UICONTROL Persons matched]** | 指示与帐户匹配的人数。 |
| **[!UICONTROL Persons unmatched]** | 指示与帐户不匹配的人数。 |
| **[!UICONTROL Last successful run]** | 指示上次成功销售线索与帐户匹配作业运行的日期和时间。 |
| **[!UICONTROL Status]** | 指示商机与帐户匹配作业的状态（成功、失败或正在处理）。 |

## 预测性商机和帐户评分用户档案扩充 {#predictive-lead-to-account-scoring}

[!UICONTROL Predictive lead and account scoring]仪表板显示特定于[预测性商机和帐户评分](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)个人资料扩充的基本量度和每日作业运行状态。

![预测性商机和帐户评分配置文件扩充](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

以下量度可用于预测商机和帐户评分配置文件扩充作业：

| 量度 | 描述 |
| --------- | ---------- |
| **[!UICONTROL Job start]** | 指示预测商机和帐户评分作业运行的开始日期和时间。 |
| **[!UICONTROL Processing time]** | 完成作业所花费的总时间。 |
| **[!UICONTROL Score name]** | 作业的分数名称。 |
| **[!UICONTROL Profile type]** | 得分类型： <ul><li>人员</li><li>帐户</li></ul>。 |
| **[!UICONTROL Job type]** | 作业的类型：<ul><li>评分</li><li>训练</li>。 |
| **[!UICONTROL Status]** | 指示预测商机和帐户评分作业的状态（成功、失败或正在处理）。 |

## UI控件 {#ui-controls}

此部分介绍监视界面中的各种用户界面(UI)选项，这些选项允许您过滤页面上显示的度量。

使用箭头图标（![箭头图标](/help/images/icons/chevron-up.png)）展开或关闭屏幕顶部的信息卡，该信息卡会显示有关用户档案扩充作业的概览信息。

![显示箭头图标UI控件的屏幕录制。](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

使用&#x200B;**[!UICONTROL Metrics and graphs]**&#x200B;切换关闭显示最新量度的视图。

![显示量度和图形切换的屏幕录制。](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

使用&#x200B;**[!UICONTROL Show failures only]**&#x200B;切换可仅显示失败的配置文件扩充作业。

![屏幕录制，显示“仅显示失败情况”切换。](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## 后续步骤 {#next-steps}

通过学习本教程，您现在可以成功监控和了解配置文件扩充作业的量度。 有关更多详细信息，请参阅以下文档：

* [Real-Time CDP B2B中的相关帐户](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [帐户配置文件UI指南中的“相关帐户”选项卡](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Real-Time CDP B2B中的商机帐户匹配](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Real-Time CDP B2B中的预测性商机和客户评分](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
