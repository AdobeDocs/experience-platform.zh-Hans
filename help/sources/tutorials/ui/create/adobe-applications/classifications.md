---
description: 了解如何在UI中创建Adobe Analytics源连接器，以将分类数据引入Adobe Experience Platform。
title: 在UI中为分类数据创建Adobe Analytics Source连接
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: dfc8a1d51e6dd25210a0b6f24dad4d0f00052414
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# 在UI中为分类数据创建Adobe Analytics源连接

>[!TIP]
>
>默认情况下，Adobe Analytics分类数据每周更新一次。 分类数据的数据摄取将在数据流初始设置七天后处理。 第一次加载摄取整个数据，随后的每周摄取运行增量数据。

阅读本教程，了解有关如何通过用户界面将Adobe Analytics分类数据摄取到Adobe Experience Platform的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md)： Experience Platform提供了可将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

Analytics Classifications Source Connector要求在使用之前，将您的数据迁移到Adobe Analytics的新分类基础架构。 要确认数据的迁移状态，请联系您的Adobe客户团队。

## 选择您的分类

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;*Adobe应用程序*&#x200B;类别下，选择&#x200B;**[!UICONTROL Adobe Analytics]**，然后选择&#x200B;**[!UICONTROL Set up]**。

>[!TIP]
>
>如果没有经过身份验证的帐户，则源目录中的源将显示&#x200B;**[!UICONTROL Set up]**&#x200B;选项。 帐户通过身份验证后，选项将更改为&#x200B;**[!UICONTROL Add data]**。

![已选择Adobe Analytics源的Experience Platform UI中的源目录。](../../../../images/tutorials/create/classifications/catalog.png)

接下来，选择[!UICONTROL Classifications]，然后选择要摄取到Experience Platform的分类数据集。 或者，您可以使用搜索来过滤并选择特定分类。

您最多可以选择30个不同的分类数据集以引入Experience Platform。 您选择的任何数据集都将出现在右边栏中。 完成后，选择[!UICONTROL Next]以继续。

![选择了多个分类数据集的分类页面。](../../../../images/tutorials/create/classifications/select.png)

## 查看分类

此时将显示&#x200B;**[!UICONTROL Review]**&#x200B;步骤，允许您在创建选定的分类数据集之前对其进行查看。 详细信息分为以下类别：

* **[!UICONTROL Connection]**：显示源平台和连接的状态。
* **[!UICONTROL Data type]**：显示所选分类的数量。
* **[!UICONTROL Scheduling]**：显示分类数据的同步频率。 **注意**：分类数据每周更新一次。

查看数据流后，单击&#x200B;**[!UICONTROL Finish]**&#x200B;并留出一段时间来创建数据流。

![Adobe Analytics分类数据的审核页面。](../../../../images/tutorials/create/classifications/review.png)

## 后续步骤

通过学习本教程，您已创建一个Analytics分类SATA连接器，它将分类数据引入到Experience Platform中。 有关[!DNL Analytics]和分类数据的详细信息，请参阅以下文档：

* [Adobe Analytics源连接器概述](../../../../connectors/adobe-applications/analytics.md)
* [在UI中为报表包数据创建Analytics源连接](./analytics.md)
* [关于分类](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html?lang=zh-Hans)
