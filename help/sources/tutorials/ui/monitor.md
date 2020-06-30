---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 监视帐户和数据集流
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# 监视帐户和数据集流

Adobe Experience Platform中的源连接器提供按计划接收外部源数据的能力。 本教程提供了从“源”工作区查看现有帐户和数据集流 *[!UICONTROL 的步]* 骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

- [体验数据模型(XDM)系统](../../../xdm/home.md): 组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成基础](../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
- [实时客户用户档案](../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

## 监视帐户

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左 **[!UICONTROL 侧导航栏]** 中选 *[!UICONTROL 择源]* ，以访问源工作区。 “ *[!UICONTROL 目录]* ”屏幕显示可为其创建帐户数据集流的各种源。 每个源显示与其关联的现有帐户和数据集流的数量。

从顶 *[!UICONTROL 部标题]* 中选择帐户以视图现有帐户。

![目录](../../images/tutorials/monitor/catalog.png)

将显 *[!UICONTROL 示]* “帐户”页面。 本页是可查看帐户的列表，包括有关其源、用户名、数据集流数和创建日期的信息。

选择左上角的图标以启动排序窗口。

![帐户](../../images/tutorials/monitor/accounts-list.png)

排序面板允许您从特定源访问帐户。 选择要处理的源，并从右侧的列表中选择帐户。

![accounts-select](../../images/tutorials/monitor/accounts-sort.png)

在“帐 *[!UICONTROL 户]* ”页中，您可以视图与您访问的帐户关联的现有数据集流的列表。 选择要视图的数据集流。

![accounts-page](../../images/tutorials/monitor/dataset-flows.png)

出现 *[!UICONTROL “Dataset flow活动]* ”屏幕。 此页以图表形式显示消息的消费率。

![数据集流活动](../../images/tutorials/monitor/dataset-flows-activity.png)

## 监视数据集流

数据集流可以直接从“目录”页 *[!UICONTROL 面访问]* ，而无需查看 *[!UICONTROL 帐户]*。 从顶 *[!UICONTROL 部标题]* 中选择数据集流，以视图现有数据集流的列表。

![数据集流](../../images/tutorials/monitor/dataset-flows-list.png)

与帐户类似，您可以使用左上角的排序图标对数据集流的列表进行排序。 选择要视图的源，并从右侧的列表中选择数据集流。

![select-dataset-flows](../../images/tutorials/monitor/dataset-flows-sort.png)

出现 *[!UICONTROL “Dataset flow活动]* ”屏幕。 此页以图表形式显示消息的消费率。

![数据集流活动](../../images/tutorials/monitor/dataset-flows-activity.png)

有关监视数据集和摄取的详细信息，请参阅有关监视流数据 [流的教程](../../../ingestion/quality/monitor-data-flows.md)。

## 后续步骤

通过本教程，您成功访问了源工作区中的现有帐户和数 *[!UICONTROL 据集]* 流。 现在，下游服务（如和）可 [!DNL Platform] 以使用传入 [!DNL Real-time Customer Profile] 数据 [!DNL Data Science Workspace]。 有关更多详细信息，请参阅以下文档:

- [实时客户用户档案概述](../../../profile/home.md)
- [数据科学工作区概述](../../../data-science-workspace/home.md)