---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform；实时客户数据平台；实时CDP;b2b;CDP
solution: Experience Platform
title: Real-time Customer Data Platform B2B版快速入门
description: 使用此情景作为示例，来设置Adobe Real-time Customer Data Platform B2B Edition的实施。
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 0%

---

# Real-time Customer Data Platform B2B Edition快速入门

本文档提供了一个高级端到端工作流，用于开始使用Real-time Customer Data Platform(CDP)B2B Edition，它通过一个示例用例来说明关键概念。

科技公司Bodea希望将来自不同孤立数据源的人员和帐户数据合并在一起，以便通过电子邮件和LinkedIn新产品广告活动来有效定位客户。 Bodea使用Marketo Engage作为其营销自动化平台，需要从包含客户数据的多个CRM中划分特定于B2B的受众。

## 快速入门

本教程工作流依赖于演示中的若干Adobe Experience Platform服务。 如果您想要遵循，建议您对以下服务有很好的了解：

- [体验数据模式(XDM)](../xdm/home.md)
- [源](../sources/home.md)
- [区段](../segmentation/home.md)
- [目标](../destinations/home.md)

## 为数据创建模式

作为初始设置的一部分，Bodea的IT部门需要创建XDM架构，以确保其数据在引入Platform时遵循标准格式，并可在不同的Platform服务和Adobe Experience Cloud产品(如Adobe Analytics和Adobe Target)中使用。

>[!WARNING]
>
>您必须遵循在本教程中链接到的相关源文档中所述的摄取模式。 其他字段映射方法无法保证有效。

Adobe Experience Platform允许您自动生成B2B数据源所需的架构和命名空间。 此工具可确保创建的架构以结构化的可重用方式描述数据。 关注 [B2B命名空间和模式自动生成实用程序文档](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) ，以完整引用设置过程。

在Adobe Experience Platform UI中，Bodea营销人员选择 **[!UICONTROL 模式]** 在左边栏中，后跟 **[!UICONTROL 浏览]** 选项卡。 由于他们使用了Marketo Engage自动生成实用程序，因此新的空架构会显示在列表中，并且所有架构都具有前缀“B2B”。

![架构工作区浏览选项卡](./assets/b2b-tutorial/empty-b2b-schemas.png)

自动生成实用程序使用标准XDM B2B类(例如， [XDM业务帐户](../xdm/classes/b2b/business-account.md) 和 [XDM业务机会](../xdm/classes/b2b/business-opportunity.md))来捕获基本B2B数据实体。 此外，基于这些类自动生成的B2B架构已预先建立了关系，允许高级分段用例。 在此可以通过UI轻松创建数据结构所需的任何其他字段组。 请参阅 [XDM UI指南，将字段组添加到架构部分](../xdm/ui/resources/schemas.md#add-field-groups) 以了解更多信息。

>[!NOTE]
> 
>如果您未使用自动生成器实用程序，或者应该创建新关系，请参阅 [在B2B模式之间创建关系](../xdm/tutorials/relationship-b2b.md).

实时客户资料可合并来自不同来源的数据，以创建关键B2B实体的整合资料。 由于用户档案是基于单个类生成的，因此自动生成实用程序会根据常见的业务用例设置架构之间的关系。 因此，Bodea团队现在可以根据其B2B模式摄取数据。

>[!NOTE]
> 
>在架构工作区中，可轻松发现默认身份命名空间、主键和由自动生成实用程序为架构创建的关系。
>
>![默认架构标识和关系UI显示](./assets/b2b-tutorial/schema-identity-relationship.png)

## 将数据摄取到Experience Platform

接下来，Bodea营销人员使用 [Marketo Engage连接器](../sources/connectors/adobe-applications/marketo/marketo.md) 将数据摄取到平台以用于下游服务。 您还可以使用Real-Time CDP B2B Edition的一个批准源来摄取数据。

>[!NOTE]
> 
>要了解贵组织可以使用哪些源连接器，您可以在平台UI中查看源目录。 要访问目录，请选择 **源** 在左侧导航中，选择 **目录**.

要在Marketo帐户与平台之间创建连接，您必须获取身份验证凭据。 请参阅 [获取Marketo源连接器身份验证凭据指南](../sources/connectors/adobe-applications/marketo/marketo-auth.md) 以了解详细说明。

获取身份验证凭据后，Bodea营销人员将在Marketo帐户与其平台组织之间创建连接。 有关 [如何使用Platform UI连接Marketo帐户](../sources/tutorials/ui/create/adobe-applications/marketo.md).

Marketo Engage源连接器提供了自动映射功能，以更轻松地将所有数据字段映射到新创建架构的数据字段。

>[!NOTE]
> 
>如果您在XDM架构中创建了自定义字段组，则在该过程的此阶段可能会有未连接的字段。 确保检查填充自定义字段组的所有值。

Bodea营销人员检查所有字段组是否已正确映射，并通过初始化数据流来继续源设置过程。 通过创建数据流以引入Marketo数据，下游Platform服务可以使用传入数据。 在初始摄取过程中，数据会以批次形式引入Experience Platform。 之后，后续摄取的数据随后会通过近乎实时的更新流入用户档案。

## 创建区段以评估数据

下一项任务是根据源数据中相关实体的特定属性，为Bodea的新电子邮件营销活动创建受众。 在平台UI中，Bodea营销人员首先会选择 **[!UICONTROL 区段]** ，然后 **[!UICONTROL 创建区段]**.

在此示例中，区段会查找销售部门中的所有工作人员，这些人员与至少具有一个未结机会的任何帐户相关。 此区段要求在XDM Indivial Profile类、 XDM Business Account类和XDM Business Opportunity类之间建立链接。

![用例区段](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>有关如何创建区段以评估数据的说明，请参阅 [区段生成器UI指南](../segmentation/ui/segment-builder.md). 有关更具体的B2B分段用例，请参阅 [Real-Time CDP B2B版分段概述](./segmentation/b2b.md).

区段生成器允许您根据实时客户配置文件数据创建可销售的受众，并根据您定义的属性、事件和现有受众的组合查看潜在受众的估计。

## 将评估的数据激活到目标

成功创建区段后，将在 [!UICONTROL 详细信息] 的子菜单。 由于当前没有为区段激活目标，因此Bodea营销人员需要将受众导出到一个数据集，以供其访问并执行操作。

在 [!UICONTROL 区段] 平台UI的工作区中，Bodea营销人员会选择 **[!UICONTROL 激活到目标]**.

![将区段激活到目标](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>请参阅 [将区段激活到目标](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) 以了解如何完成此操作的全面步骤。

Bodea营销人员将区段激活到Marketo目标，以便他们能够将区段数据从Platform推送到静态列表形式的Marketo Engage。 请参阅 [Marketo目标](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html) 以了解更多信息。

## 后续步骤

通过阅读本教程，您已成功利用Real-Time CDP B2B Edition使用的各种Adobe Experience Platform服务。 因此，您学会了如何将B2B数据作为可操作的受众（可跨不同渠道参与）进行摄取、细分、评估和导出。
