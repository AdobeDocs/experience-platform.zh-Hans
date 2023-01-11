---
keywords: Experience Platform；主页；热门主题；选择退出；分段；分段服务；分段服务；荣誉退出；选择退出；选择退出；同意；共享；收集；
solution: Experience Platform
title: 在区段中尊重同意
description: 了解如何在区段操作中执行个人数据收集和共享的客户同意首选项。
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# 在区段中尊重同意

法律隐私法规，例如 [!DNL California Consumer Privacy Act] (CCPA)为消费者提供选择退出收集其个人数据或将其个人数据与第三方共享的权利。 Adobe Experience Platform提供标准的Experience Data Model(XDM)组件，这些组件旨在以实时客户资料数据捕获这些客户同意首选项。

如果客户因共享其个人数据而撤回或拒绝同意，则贵组织在为营销活动生成受众时务必遵循该偏好。 本文档介绍如何使用Experience Platform用户界面在区段定义中集成客户同意值。

## 快速入门

尊重客户同意值需要了解 [!DNL Adobe Experience Platform] 涉及的服务。 在启动本教程之前，请确保您熟悉以下服务：

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):Platform用来组织客户体验数据的标准化框架。
* [[!DNL Real-Time Customer Profile]](../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md):允许您从 [!DNL Real-Time Customer Profile] 数据。

## 同意架构字段

为了遵守客户的同意和偏好，您的 [!UICONTROL XDM个人配置文件] 并集架构必须包含标准字段组 **[!UICONTROL 同意和首选项]**.

有关字段组提供的每个属性的结构和预期用例的详细信息，请参阅 [同意和首选项参考指南](../xdm/field-groups/profile/consents.md). 有关如何将字段组添加到架构的分步说明，请参阅 [XDM UI指南](../xdm/ui/resources/schemas.md#add-field-groups).

将字段组添加到 [启用了用户档案的架构](../xdm/ui/resources/schemas.md#profile) 并且其字段已用于从体验应用程序中摄取同意数据，因此您可以在区段规则中使用收集的同意属性。

## 在分段中处理同意

为确保区段中不包含已选择退出的用户档案，必须在创建任何新区段时向现有区段添加和包含特殊字段。

以下步骤演示如何为两种类型的选择退出标记添加相应的字段：

1. [!UICONTROL 数据收集]
1. [!UICONTROL 共享数据]

>[!NOTE]
>
>虽然本指南重点介绍上面的两个选择退出标记，但您也可以配置区段以合并其他同意信号。 的 [同意和首选项参考指南](../xdm/field-groups/profile/consents.md) 提供有关每个选项及其预定用例的更多信息。

在UI中生成区段时，在 **[!UICONTROL 属性]**，导航到 **[!UICONTROL XDM个人配置文件]**，然后选择 **[!UICONTROL 同意和首选项]**. 从此处，您可以看到 **[!UICONTROL 数据收集]** 和 **[!UICONTROL 共享数据]**.

![](./images/opt-outs/consents.png)

首先，选择 **[!UICONTROL 数据收集]** 类别，然后拖动 **[!UICONTROL 选择值]** 到区段生成器中。 向区段添加属性时，您可以指定 [同意值](../xdm/field-groups/profile/consents.md#choice-values) 必须包含或排除的规则。

![](./images/opt-outs/consent-values.png)

一种方法是排除选择禁止收集其数据的任何客户。 要实现此目的，请将运算符设置为 **[!UICONTROL 不等于]**，然后选择以下值：

* **[!UICONTROL 否（选择退出）]**
* **[!UICONTROL 默认为否（选择退出）]**
* **[!UICONTROL 未知]** （如果未知，则假定同意不予受理）

![](./images/opt-outs/collect.png)

在 **[!UICONTROL 属性]** 在左边栏中，导航回 **[!UICONTROL 同意和首选项]** ，然后选择 **[!UICONTROL 共享数据]**. 拖动其对应的 **[!UICONTROL 选择值]** ，并为 [!UICONTROL 数据收集] 选择值。 确保 **[!UICONTROL 或]** 在两个属性之间建立关系。

![](./images/opt-outs/share.png)

通过 **[!UICONTROL 数据收集]** 和 **[!UICONTROL 共享数据]** 添加到区段的同意值后，任何选择禁止使用其数据的客户都将从生成的受众中排除。 从此处，您可以在选择 **[!UICONTROL 保存]** 来完成这个过程。

## 后续步骤

通过阅读本教程，您现在应该能够更好地了解在Experience Platform中构建区段时如何遵循客户的同意和偏好。

有关在Platform中管理同意的更多信息，请参阅以下文档：

* [使用Adobe标准进行同意处理](../landing/governance-privacy-security/consent/adobe/overview.md)
* [使用IAB TCF 2.0标准的同意处理](../landing/governance-privacy-security/consent/iab/overview.md)