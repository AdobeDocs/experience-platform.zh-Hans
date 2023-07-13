---
solution: Experience Platform
title: 在区段中接受同意
description: 了解如何在区段操作中执行个人数据收集和共享的客户同意首选项。
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# 在区段中遵循同意

>[!NOTE]
>
>本指南介绍如何在中遵循同意 **区段定义**.

法律隐私法规，例如 [!DNL California Consumer Privacy Act] (CCPA)为消费者提供选择退出收集其个人数据或与第三方共享数据的权利。 Adobe Experience Platform提供了标准Experience Data Model (XDM)组件，这些组件旨在捕获实时客户配置文件数据中的这些客户同意首选项。

如果客户撤回或拒绝同意共享其个人数据，贵组织在为营销活动生成受众时务必遵循该偏好设置。 本文档介绍如何使用Experience Platform用户界面将客户同意值集成到区段定义中。

## 快速入门

尊重客户同意值需要了解各种 [!DNL Adobe Experience Platform] 涉及的服务。 在开始本教程之前，请确保您熟悉以下服务：

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md)：Platform用于组织客户体验数据的标准化框架。
* [[!DNL Real-Time Customer Profile]](../profile/home.md)：根据来自多个来源的汇总数据实时提供统一的客户用户档案。
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md)：允许您从构建受众 [!DNL Real-Time Customer Profile] 数据。

## 同意架构字段

为了尊重客户同意和偏好设置，您的解决方案中包含的其中一个架构 [!UICONTROL XDM个人资料] 合并架构必须包含标准字段组 **[!UICONTROL 同意和偏好设置]**.

有关字段组提供的每个属性的结构和预期用例的详细信息，请参阅 [同意和偏好设置参考指南](../xdm/field-groups/profile/consents.md). 有关如何将字段组添加到架构的分步说明，请参阅 [XDM UI指南](../xdm/ui/resources/schemas.md#add-field-groups).

将字段组添加到 [启用配置文件的架构](../xdm/ui/resources/schemas.md#profile) 及其字段用于从体验应用程序中摄取同意数据，您可以在区段规则中使用收集的同意属性。

## 在分段中处理同意

为了确保选择退出的用户档案不包含在区段定义中，必须在现有区段定义中添加特殊字段，并在创建任何新区段定义时包含这些字段。

以下步骤演示了如何为两种类型的选择退出标记添加相应的字段：

1. [!UICONTROL 数据收集]
1. [!UICONTROL 共享数据]

>[!NOTE]
>
>虽然本指南重点介绍上述两个选择退出标记，但您也可以配置区段定义以纳入其他同意信号。 此 [同意和偏好设置参考指南](../xdm/field-groups/profile/consents.md) 提供了有关每个选项及其预期用例的更多信息。

在UI中构建区段定义时，在 **[!UICONTROL 属性]**，导航到 **[!UICONTROL XDM个人资料]**，然后选择 **[!UICONTROL 同意和偏好设置]**. 从这里，您可以看到以下各项的选项 **[!UICONTROL 数据收集]** 和 **[!UICONTROL 共享数据]**.

![](./images/opt-outs/consents.png)

首先，选择 **[!UICONTROL 数据收集]** 类别，然后拖动 **[!UICONTROL 选项值]** 放入区段生成器中。 将属性添加到区段定义时，可以指定 [同意值](../xdm/field-groups/profile/consents.md#choice-values) 必须包含或排除的重复项。

![](./images/opt-outs/consent-values.png)

一种方法是排除任何选择不收集其数据的客户。 要实现此目的，请将运算符设置为 **[!UICONTROL 不等于]**，然后选择以下值：

* **[!UICONTROL 否（选择退出）]**
* **[!UICONTROL 默认为“否”（选择退出）]**
* **[!UICONTROL 未知]** （如果同意被假定为不批准，如果其他情况未知）

![](./images/opt-outs/collect.png)

下 **[!UICONTROL 属性]** 在左边栏中，导航回 **[!UICONTROL 同意和偏好设置]** 部分，然后选择 **[!UICONTROL 共享数据]**. 拖动其对应的 **[!UICONTROL 选项值]** ，然后选择与相同的值 [!UICONTROL 数据收集] 选项值。 确保 **[!UICONTROL 或]** 在两个属性之间建立关系。

![](./images/opt-outs/share.png)

同时使用 **[!UICONTROL 数据收集]** 和 **[!UICONTROL 共享数据]** 添加到区段定义的同意值，将从生成的受众中排除已选择退出使用其数据的任何客户。 从这里，您可以在选择之前继续自定义区段定义 **[!UICONTROL 保存]** 完成该过程。

## 后续步骤

通过学习本教程，您现在应该能够更好地了解在Experience Platform中构建区段定义时如何遵循客户同意和偏好设置。

有关在Platform中管理同意的更多信息，请参阅以下文档：

* [使用Adobe标准进行同意处理](../landing/governance-privacy-security/consent/adobe/overview.md)
* [使用IAB TCF 2.0标准进行同意处理](../landing/governance-privacy-security/consent/iab/overview.md)