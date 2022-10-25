---
keywords: Experience Platform；主页；热门主题；
title: （测试版）Adobe Workfront源
description: Adobe Workfront是一个营销工作管理应用程序，可帮助您在一个位置管理整个工作生命周期。 Workfront包含一些报告和分析工具，您可以使用这些工具更好地了解和优化您组织的工作流程。
source-git-commit: 1af0863766e29c599e02f2a553d237bc62f455d2
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# （测试版）Adobe Workfront源

>[!NOTE]
>
>Adobe Workfront源是测试版。 请参阅 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

Adobe Workfront是一个营销工作管理应用程序，可帮助您在一个位置管理整个工作生命周期。 Workfront包含一些报告和分析工具，您可以使用这些工具更好地了解和优化您组织的工作流程。

通过Workfront与Adobe Experience Platform源目录的集成，您可以将Workfront数据纳入Experience Platform并执行以下用例：

* 将工作记录与第三方数据结合使用。
* 对工作记录应用历史分析和时间序列分析。
* 通过第三方业务智能工具(如 [!DNL PowerBI].
* 使用标准SQL查询工作数据。

以下工作项及其相应属性可通过Workfront源包含在Experience Platform中：

* 组合
* 项目
* 项目
* 任务
* 操作任务（问题）
* 用户

Workfront源会流式传输这些属性的所有新更新，并回填长达一年的历史更改事件。 将Workfront数据放入Platform数据集后，您便可以利用 [查询服务](../../../query-service/home.md) 以及其他工具，以便根据需要进一步分析工作相关数据或将其与其他数据集关联。

## 使用UI将Workfront连接到平台

有关如何将Workfront数据导入平台的详细说明，请阅读 [创建源连接以将Workfront数据引入平台](../../tutorials/ui/create/adobe-applications/workfront.md).