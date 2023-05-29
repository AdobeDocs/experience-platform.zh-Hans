---
keywords: Experience Platform；主页；热门主题；
title: (Beta) Adobe Workfront源
description: Adobe Workfront是一个营销工作管理应用程序，可帮助您在一个位置管理整个工作生命周期。 Workfront包括报告和分析工具，可用于更好地了解和优化组织内的工作流程。
exl-id: ea714278-d84d-4929-9a34-81fc5fb70871
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# (Beta) Adobe Workfront源

>[!NOTE]
>
>Adobe Workfront源为测试版。 请参阅 [源概述](../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

Adobe Workfront是一个营销工作管理应用程序，可帮助您在一个位置管理整个工作生命周期。 Workfront包括报告和分析工具，可用于更好地了解和优化组织内的工作流程。

Workfront与Adobe Experience Platform源目录集成允许您将Workfront数据纳入Experience Platform并执行用例，例如：

* 将工作记录与第三方数据相结合。
* 对工作记录应用历史和时间序列分析。
* 通过第三方业务智能工具(如 [!DNL PowerBI].
* 使用标准SQL查询工作数据。

以下工作项及其相应的属性有资格通过Workfront源包含在Experience Platform中：

* 组合
* 项目
* 项目
* 任务
* 操作任务（问题）
* 用户

Workfront源可流式传输这些属性的所有新更新，并回填至多一年的历史更改事件。 将Workfront数据放入Platform数据集后，您便可以利用 [查询服务](../../../query-service/home.md) 和其他工具，以根据需要进一步分析工作相关数据或将其与其他数据集联接。

## 使用UI将Workfront连接到平台

有关如何将Workfront数据引入平台的详细说明，请阅读以下网站上的指南： [创建源连接以将Workfront数据引入平台](../../tutorials/ui/create/adobe-applications/workfront.md).
