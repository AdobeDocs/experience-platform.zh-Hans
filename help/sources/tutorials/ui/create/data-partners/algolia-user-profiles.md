---
title: 使用UI将Algolia用户配置文件连接到Experience Platform
description: 了解如何将阿尔及利亚用户意图连接到Experience Platform
exl-id: d4c936a7-4983-4a12-a813-03b672116e44
source-git-commit: 9bc7d372eba9ffcfe64f90d2d58a532411e5f1ce
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 1%

---

# 使用UI将[!DNL Algolia User Profiles]数据摄取到Experience Platform

阅读本教程，了解如何使用用户界面将数据从[!DNL Algolia User Profiles]帐户摄取到Adobe Experience Platform。

## 快速入门

>[!IMPORTANT]
>
>在开始之前，请确保您已完成[[!DNL Algolia User Profiles] 概述](../../../../connectors/data-partners/algolia-user-profiles.md#prerequisites)中列出的先决条件步骤。

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。

### 收集所需的凭据

为了将[!DNL Algolia]连接到Experience Platform，您必须提供以下凭据的值：

| 凭据 | 描述 |
| --- | --- |
| 应用程序Id | [!DNL Algolia]应用程序ID是分配给您[!DNL Algolia]帐户的唯一标识符。 |
| API密钥 | [!DNL Algolia] API密钥是一个用于向[!DNL Algolia]的搜索和索引服务验证和授权API请求的凭据。 |

有关这些凭据的详细信息，请参阅[!DNL Algolia] [身份验证文档](https://www.algolia.com/doc/tools/cli/get-started/authentication/)。

## 连接您的[!DNL Algolia]帐户

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;*[!UICONTROL 源]*&#x200B;工作区。 您可以在&#x200B;*[!UICONTROL 类别]*&#x200B;面板中选择相应的类别。 或者，您可以使用搜索栏导航到要使用的特定源。

若要使用[!DNL Algolia]，请选择&#x200B;*[!UICONTROL 数据和标识合作伙伴]*&#x200B;下的&#x200B;**[!UICONTROL Algolia]**&#x200B;源卡，然后选择&#x200B;**[!UICONTROL 设置]**。

>[!TIP]
>
>当给定的源尚未具有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL 设置]**&#x200B;选项。 一旦存在经过身份验证的帐户，此选项将更改为&#x200B;**[!UICONTROL 添加数据]**。

![已选择阿尔及利亚用户配置文件源的源目录。](../../../../images/tutorials/create/algolia/user-profiles/catalog.png)

## 身份验证

### 使用现有帐户

若要使用现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后选择要使用的[!DNL Algolia User Profiles]帐户。 若要继续，请选择&#x200B;**[!UICONTROL 下一步]**。

![现有帐户接口。](../../../../images/tutorials/create/algolia/user-profiles/existing-account.png)

### 创建新帐户

如果要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后提供名称、可选描述和[!DNL Algolia]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

![新帐户接口。](../../../../images/tutorials/create/algolia/user-profiles/new-account.png)

## 添加数据

创建您的[!DNL Algolia User Profiles]帐户后，将显示&#x200B;**[!UICONTROL 添加数据]**&#x200B;步骤，该步骤为您提供了一个界面来探索要带到Experience Platform的[!DNL Algolia]用户配置文件。

* 界面的左侧部分允许您输入可选的&#x200B;**[!UICONTROL 索引]**&#x200B;和&#x200B;**[!UICONTROL 关联]**&#x200B;字段。
* 界面的右侧部分允许您预览最多100行用户配置文件。

选择并预览要摄取的数据后，请选择&#x200B;**[!UICONTROL 下一步]**。

![工作流的选择数据步骤。](../../../../images/tutorials/create/algolia/user-profiles/select-data.png)

## 提供数据流详细信息

如果您使用的是现有数据集，请选择与使用[!DNL Algolia Profile]字段组的架构关联的数据集。

![源工作流的现有数据集步骤。](../../../../images/tutorials/create/algolia/user-profiles/dataflow-detail-existing-dataset.png)

如果要创建新数据集，请选择一个使用[!DNL Algolia Profile]字段组的架构，该字段组是映射步骤中必需的。

![源工作流的新数据集步骤。](../../../../images/tutorials/create/algolia/user-profiles/dataflow-detail-new-dataset.png)

## 将数据字段映射到XDM架构

在将数据摄取到Experience Platform之前，使用映射界面将源数据映射到相应的架构字段。  有关详细信息，请阅读UI[&#128279;](../../../../../data-prep/ui/mapping.md)中的映射指南。

![源工作流的映射步骤。](../../../../images/tutorials/create/algolia/user-profiles/mapping.png)

## 计划摄取运行

接下来，使用计划界面定义数据流的摄取计划。

<!-- The Scheduling step allows for configuration of the data/time to execute the [!DNL Algolia Uer Profiles] Source connector. There is configuration to backfill the data from [!DNL Algolia] which will pull all the profiles from the source system.  If the source is scheduled, then it will retrieve modified profiles from the [!DNL Algolia] based on the configured time interval. -->

![源工作流的计划步骤。](../../../../images/tutorials/create/algolia/user-profiles/scheduling.png)

| 计划配置 | 描述 |
| --- | --- |
| 频度 | 配置频率以指示数据流运行的频率。 您可以将频率设置为： <ul><li>**一次**：将频率设置为`once`以创建一次性引入。 创建一次性摄取数据流时，间隔和回填配置不可用。 默认情况下，调度频率设置为一次。</li><li>**分钟**：将频率设置为`minute`，以计划数据流以每分钟摄取数据。</li><li>**小时**：将频率设置为`hour`，以计划数据流每小时摄取数据。</li><li>**天**：将频率设置为`day`，以计划数据流每天摄取数据。</li><li>**周**：将频率设置为`week`，以计划数据流每周摄取数据。</li></ul> |
| 间隔 | 选择频率后，可以配置间隔设置以建立每次引入之间的时间范围。 例如，如果将频率设置为天并将间隔配置为15，则数据流将每15天运行一次。 不能将间隔设置为零。 每个频率的最小接受间隔值如下：<ul><li>**一次**：不适用</li><li>**分钟**： 15</li><li>**小时**： 1</li><li>**天**： 1</li><li>**周**： 1</li></ul> |
| 开始时间 | 预计运行的时间戳，以UTC时区显示。 |
| 回填 | 回填可确定最初摄取的数据。 如果启用了回填，则指定路径中的所有当前文件将在第一次计划摄取期间摄取。 如果禁用回填，则只摄取在第一次引入运行到开始时间之间加载的文件。 将不会摄取在开始时间之前加载的文件。 |

## 查看您的数据流

使用“复查”页可在摄取之前获取数据流摘要。 详细信息按以下类别分组：

* **连接** — 显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **分配数据集和映射字段** — 显示要将源数据摄取到哪个数据集，包括该数据集所遵循的架构。
* **正在计划** — 显示摄取计划的活动周期、频率和间隔。

查看数据流后，选择&#x200B;**[!UICONTROL 完成]**，然后等待一些时间来创建数据流。

![源工作流的审核步骤。](../../../../images/tutorials/create/algolia/user-profiles/review.png)

## 后续步骤

通过学习本教程，您已成功创建了一个数据流，以将意图数据从[!DNL Algolia]源引入Experience Platform。 有关其他资源，请访问下面列出的文档。

### 监测数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监视数据流的详细信息，请访问有关UI中[监视帐户和数据流的教程](../../../../../dataflows/ui/monitor-sources.md)。

### 更新您的数据流

要更新数据流计划、映射和常规信息的配置，请访问有关[在UI中更新源数据流的教程](../../update-dataflows.md)。

### 删除您的数据流

您可以删除不再必需的数据流或使用&#x200B;**[!UICONTROL 数据流]**&#x200B;工作区中提供的&#x200B;**[!UICONTROL 删除]**&#x200B;功能错误地创建的数据流。 有关如何删除数据流的详细信息，请访问有关[在UI中删除数据流](../../delete.md)的教程。
