---
title: 使用UI将Bombora的意图连接到Experience Platform
description: 了解如何将Bombora Intent连接到Experience Platform
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hans#rtcdp-editions newtab=true"
badgeB2P: label="B2P版本" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=zh-Hans#rtcdp-editions newtab=true"
exl-id: 76a4fed5-b2d5-46d5-9245-b52792a7d323
source-git-commit: a1af85c6b76cc7bded07ab4acaec9c3213a94397
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 4%

---

# 使用UI将[!DNL Bombora Intent]连接到Experience Platform

阅读本指南，了解如何使用用户界面将您的[!DNL Bombora Intent]帐户连接到Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md)： Real-Time CDP B2B edition专为以B2B服务模式运营的营销人员而构建。 它将来自多个来源的数据汇集在一起&#x200B;，并将其组合成人员和帐户轮廓的单一视图。这种统一的数据使营销人员能够精确锁定特定受众，并通过所有可用渠道吸引这些受众。
* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 先决条件

有关如何检索身份验证凭据的信息，请阅读[[!DNL Bombora Intent] 概述](../../../../connectors/data-partners/bombora.md)。

## 导航源目录

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;*[!UICONTROL 源]*&#x200B;工作区。 您可以在&#x200B;*[!UICONTROL 类别]*&#x200B;面板中选择相应的类别。 或者，您可以使用搜索栏导航到要使用的特定源。

若要使用[!DNL Bombora]，请选择&#x200B;*[!UICONTROL 数据和标识合作伙伴]*&#x200B;下的&#x200B;**[!UICONTROL Bombora Intent]**&#x200B;源卡，然后选择&#x200B;**[!UICONTROL 添加数据]**。

>[!TIP]
>
>当给定的源尚未具有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL 设置]**&#x200B;选项。 一旦存在经过身份验证的帐户，此选项将更改为&#x200B;**[!UICONTROL 添加数据]**。

![已选择“Bombora Intent”卡的源目录。](../../../../images/tutorials/create/bombora/catalog.png)

## 身份验证 {#authentication}

### 使用现有帐户 {#existing}

要使用现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后从界面上的帐户列表中选择要使用的帐户。

选择帐户后，选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续执行下一步。

![源工作流中的现有帐户接口。](../../../../images/tutorials/create/bombora/existing.png)

### 创建新帐户 {#create}

如果您没有现有帐户，则必须通过提供与您的源对应的必需身份验证凭据来创建新帐户。

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后提供帐户名称以及帐户详细信息的描述（可选）。 接下来，提供相应的身份验证值，以便针对Experience Platform验证您的源。 要连接您的[!DNL Bombora]帐户，您必须具有以下凭据：

* **访问密钥ID**：您的[!DNL Bombora]访问密钥ID。 这是一个由61个字符组成的字母数字字符串，向Experience Platform验证您的帐户时需要使用该字符串。
* **访问密钥**：您的[!DNL Bombora]访问密钥。 这是一个40字符、以base-64编码的字符串，向Experience Platform验证您的帐户时需要使用该字符串。
* **存储段名称**：将从其中提取数据的[!DNL Bombora]存储段。

![源工作流中的新帐户接口。](../../../../images/tutorials/create/bombora/new.png)

## 提供数据流详细信息 {#provide-dataflow-details}

帐户经过身份验证并连接后，现在必须为数据流提供以下详细信息：

* **数据流名称**：您的数据流名称。 创建并处理数据流后，即可使用此名称在UI中搜索数据流。
* **描述**： （可选）数据流的简短说明或其他信息。
* **域源**：域或网站字段将您的源帐户记录与Experience Platform帐户相匹配。 此值取决于您的配置。 如果未提供，则域默认为accountOrganization.website。

![源工作流的数据流详细信息接口。](../../../../images/tutorials/create/bombora/dataflow-detail.png)

## 计划数据流 {#schedule-dataflow}

接下来，使用计划界面配置数据流的摄取计划。

* **频率**：配置频率以指示数据流运行的频率。 您可以安排[!DNL Bombora]数据流每周摄取一次数据。
* **间隔**：间隔表示每个摄取周期之间的时间量。 [!DNL Bombora]数据流唯一支持的间隔为1。 这意味着您的数据流将每周、每周摄取一次数据。
* **开始时间**：开始时间指示数据流首次运行迭代的时间。 [!DNL Bombora]每周一次将数据丢到Adobe，时间是UTC时间周一的中午12:00。 因此，您必须在UTC中午12:00之后设置摄取开始时间。 此外，在将文件拖放到Adobe时，必须通过[!DNL Bombora]确认摄取时间，因为他们可能会更改其计划。

配置数据流的摄取计划后，选择&#x200B;**[!UICONTROL 下一步]**。

![源工作流的计划接口。](../../../../images/tutorials/create/bombora/scheduling.png)

## 查看数据流 {#review-dataflow}

数据流创建过程的最后一步是在执行数据流之前对其进行检查。 使用&#x200B;*[!UICONTROL 查看]*&#x200B;步骤可在新数据流运行之前查看其详细信息。 详细信息按以下类别分组：

* **连接**：显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **计划**：显示摄取计划的活动时段、频率和间隔。

查看数据流后，选择&#x200B;**[!UICONTROL 完成]**。

![源工作流的审阅界面。](../../../../images/tutorials/create/bombora/review.png)

## 后续步骤

通过学习本教程，您已成功创建了一个数据流，以将意图数据从[!DNL Bombora]源引入Experience Platform。 有关其他资源，请访问下面列出的文档。

### 监测数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监视数据流的详细信息，请访问有关UI中[监视帐户和数据流的教程](../../../../../dataflows/ui/monitor-sources.md)。

### 更新您的数据流

要更新数据流计划、映射和常规信息的配置，请访问有关[在UI中更新源数据流的教程](../../update-dataflows.md)。

### 删除您的数据流

您可以删除不再必需的数据流或使用&#x200B;**[!UICONTROL 数据流]**&#x200B;工作区中提供的&#x200B;**[!UICONTROL 删除]**&#x200B;功能错误地创建的数据流。 有关如何删除数据流的详细信息，请访问有关[在UI中删除数据流](../../delete.md)的教程。
