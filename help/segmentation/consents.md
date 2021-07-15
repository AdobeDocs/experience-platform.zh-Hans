---
keywords: Experience Platform；主页；热门主题；选择退出；分段；分段服务；分段服务；遵守选择退出；选择退出；选择退出；同意；共享；收集；
solution: Experience Platform
title: 在区段中尊重同意
topic-legacy: overview
description: 了解如何在区段操作中执行个人数据收集和共享的客户同意首选项。
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# 在区段中尊重同意

[!DNL California Consumer Privacy Act](CCPA)等法律隐私法规为消费者提供了选择退出收集其个人数据或与第三方共享其个人数据的权利。 Adobe Experience Platform提供标准的Experience Data Model(XDM)组件，这些组件旨在以实时客户资料数据捕获这些客户同意首选项。

如果客户因共享其个人数据而撤回或拒绝同意，则贵组织在为营销活动生成受众时务必遵循该偏好。 本文档介绍如何使用Experience Platform用户界面在区段定义中集成客户同意值。

## 快速入门

要尊重客户同意值，需要了解涉及的各种[!DNL Adobe Experience Platform]服务。 在启动本教程之前，请确保您熟悉以下服务：

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md):Platform用来组织客户体验数据的标准化框架。
* [[!DNL Real-time Customer Profile]](../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md):允许您根据数据构建受众 [!DNL Real-time Customer Profile] 区段。

## 同意架构字段

为了遵守客户的同意和首选项，作为[!UICONTROL XDM个人用户档案]并集架构一部分的架构必须包含标准字段组&#x200B;**[!UICONTROL 同意和首选项]**。

有关字段组提供的每个属性的结构和预期用例的详细信息，请参阅[同意和首选项参考指南](../xdm/field-groups/profile/consents.md)。 有关如何将字段组添加到架构的分步说明，请参阅[XDM UI指南](../xdm/ui/resources/schemas.md#add-field-groups)。

将字段组添加到[启用了配置文件的架构](../xdm/ui/resources/schemas.md#profile)并且其字段用于从体验应用程序中摄取同意数据后，您便可以在区段规则中使用收集的同意属性。

## 在分段中处理同意

为确保区段中不包含已选择退出的用户档案，必须在创建任何新区段时向现有区段添加和包含特殊字段。

以下步骤演示如何为两种类型的选择退出标记添加相应的字段：

1. [!UICONTROL 数据收集]
1. [!UICONTROL 共享数据]

>[!NOTE]
>
>虽然本指南重点介绍上面的两个选择退出标记，但您也可以配置区段以合并其他同意信号。 [同意和首选项参考指南](../xdm/field-groups/profile/consents.md)提供了有关每个选项及其预期用例的更多信息。

在UI中的&#x200B;**[!UICONTROL 属性]**&#x200B;下，导航到&#x200B;**[!UICONTROL XDM个人配置文件]**，然后选择&#x200B;**[!UICONTROL 同意和首选项]**。 从此处，您可以看到&#x200B;**[!UICONTROL 数据收集]**&#x200B;和&#x200B;**[!UICONTROL 共享数据]**&#x200B;的选项。

![](./images/opt-outs/consents.png)

首先选择&#x200B;**[!UICONTROL 数据收集]**&#x200B;类别，然后将&#x200B;**[!UICONTROL 选择值]**&#x200B;拖到区段生成器中。 向区段添加属性时，您可以指定必须包含或排除的[同意值](../xdm/field-groups/profile/consents.md#choice-values)。

![](./images/opt-outs/consent-values.png)

一种方法是排除选择禁止收集其数据的任何客户。 为此，请将运算符设置为&#x200B;**[!UICONTROL 不等于]**，然后选择以下值：

* **[!UICONTROL 否（选择退出）]**
* **[!UICONTROL 默认为否（选择退出）]**
* **[!UICONTROL 未知]** （如果未知，则假定不予同意）

![](./images/opt-outs/collect.png)

在左边栏的&#x200B;**[!UICONTROL 属性]**&#x200B;下，导航回&#x200B;**[!UICONTROL 同意和首选项]**&#x200B;部分，然后选择&#x200B;**[!UICONTROL 共享数据]**。 将相应的&#x200B;**[!UICONTROL 选择值]**&#x200B;拖到画布中，并选择与[!UICONTROL 数据收集]选择值相同的值。 确保在两个属性之间建立&#x200B;**[!UICONTROL Or]**&#x200B;关系。

![](./images/opt-outs/share.png)

将&#x200B;**[!UICONTROL 数据收集]**&#x200B;和&#x200B;**[!UICONTROL 共享数据]**&#x200B;同意值添加到区段后，任何选择禁止使用其数据的客户都将从生成的受众中排除。 从此处，您可以在选择&#x200B;**[!UICONTROL 保存]**&#x200B;以完成该过程之前，继续自定义区段定义。

## 后续步骤

通过阅读本教程，您现在应该能够更好地了解在Experience Platform中构建区段时如何遵循客户的同意和偏好。

有关在Platform中管理同意的更多信息，请参阅以下文档：

* [使用Adobe标准进行同意处理](../landing/governance-privacy-security/consent/adobe/overview.md)
* [使用IAB TCF 2.0标准的同意处理](../landing/governance-privacy-security/consent/iab/overview.md)