---
title: 对Ad Hoc架构的基于属性的访问控制支持
description: 有关限制对通过Adobe Experience Platform查询服务生成的临时架构中数据字段的访问的指南。
exl-id: d675e3de-ab62-4beb-9360-1f6090397a17
source-git-commit: 91f318596bf268aa93e8b2df9c13774aab76d13a
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 1%

---

# 对临时架构的基于属性的访问控制支持

引入Adobe Experience Platform的任何数据都由体验数据模型(XDM)架构封装，并可能受到由您的组织或法律法规定义的使用限制的约束。

在未指定架构时，通过查询服务执行CTAS查询，可自动生成临时架构。 通常需要限制临时架构的某些字段或数据集的使用，以控制对敏感个人数据和个人身份信息的访问。 Adobe Experience Platform允许您使用基于属性的访问控制功能通过Platform UI标记架构字段，从而简化此访问控制。

标签可随时应用，从而在您选择如何管理数据方面提供了灵活性。 但是，最佳做法是在数据被摄取到平台后立即为数据添加标签，或在数据在平台中可用后立即为数据添加标签。

基于模式的标签是基于属性的访问控制的重要组成部分，可更好地管理给用户或用户组的访问权限。 Adobe Experience Platform允许您通过创建和应用标签来限制对临时架构任何字段的访问。

本文档提供了一个教程，用于通过将标签应用于通过查询服务生成的临时架构的数据字段来管理对敏感数据的访问。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [Experience Data Model(XDM)系统](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans):Experience Platform组织客户体验数据的标准化框架。
   * [[!DNL Schema Editor]](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html):了解如何在Platform UI中创建和管理模式和其他资源。
* [[!DNL Data Governance]](../../data-governance/home.md):了解如何 [!DNL Data Governance] 允许您管理客户数据，并确保符合适用于数据使用的法规、限制和策略。
* [基于属性的访问控制](../../access-control/abac/overview.md):基于属性的访问控制是Adobe Experience Platform的一项功能，它使管理员能够根据属性控制对特定对象和/或功能的访问。 属性可以是添加到对象的元数据，例如添加到临时架构或常规架构字段的标签。 管理员定义包含属性的访问策略以管理用户访问权限。

## 创建临时架构

执行查询并生成结果后，将自动生成临时架构并将其添加到架构清单。

要添加数据标签，请导航到 [!UICONTROL 模式] 功能板浏览选项卡，选择 [!UICONTROL 模式] ，位于Platform UI的左边栏中。 将显示架构清单。

>[!NOTE]
>
>默认情况下，临时架构不会显示在架构清单中。

## 在平台UI的架构清单中发现临时架构 {#discover-ad-hoc-schemas}

要在Platform UI中显示临时架构，请选择过滤器图标(![过滤器图标。](../images/data-governance/filter.png))，然后选择**[!UICONTROL 显示临时架构] 在显示的左边栏中。

![“架构”功能板过滤器选项左边栏，并启用“显示临时架构”切换开关。](../images/data-governance/adhoc-schema-toggle.png)

从可用列表中选择最近创建的临时架构的名称。 此时会显示临时架构结构的可视化图表。

![示例Ad Hoc架构结构图。](../images/data-governance/adhoc-schema-structure-diagram.png)

## 编辑管理标签

要编辑临时架构的数据标签，请选择 [!UICONTROL 标签] 选项卡。 标签工作区允许您将标签应用、创建和编辑到临时架构字段，并通过UI控制访问权限。 此处显示了临时架构中的所有字段。

## 编辑架构或字段的标签

要编辑整个架构的标签，请选择铅笔图标(![铅笔图标。](../images/data-governance/edit-icon.png))到架构名称旁边(位于 [!UICONTROL 标签] 选项卡。

![模式工作区中的标签视图突出显示了铅笔图标。](../images/data-governance/edit-entire-schema-labels.png)

要将标签应用于现有字段，请从列表中选择一个或多个字段，然后选择 [!UICONTROL 编辑管理标签] 中。

![在“架构”工作区中，“标签”视图在右侧侧栏中突出显示了“编辑管理标签”选项。](../images/data-governance/edit-governance-labels.png)

## 编辑标签弹出窗口

的 [!UICONTROL 编辑标签] 弹出窗口。 从此视图中，您可以通过UI创建或编辑现有管理标签。

![此时会弹出编辑标签。](../images/data-governance/edit-labels-popover.png)

有关如何操作的指导，请参阅相应文档 [创建或编辑所选架构或字段的标签](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/labels.html#edit-the-labels-for-the-schema-or-field).

>[!NOTE]
>
>创建新标签或编辑现有标签需要贵组织的管理员权限。 如果您没有管理员权限，请联系您的系统管理员以安排访问权限。

也可以使用权限工作区创建标签。 请参阅 [有关在权限工作区中创建标签的指南](../../access-control/abac/ui/labels.md) 中。

在应用了适当级别的基于属性的访问控制后，当用户尝试访问不可访问的数据时，以下系统行为将应用于通过查询服务执行的任何查询：

1. 如果用户无法访问某个架构中的某个字段，则用户将无法读取或写入该受限字段。 这适用于以下常见情况：

   * 当用户尝试执行仅具有受限列的查询时，系统将引发该列不存在的错误。
   * 当用户尝试执行包含多个列（其中包含受限列）的查询时，系统将仅返回所有非受限列的输出。

1. 如果用户请求访问计算字段，则用户必须有权访问组合中使用的所有字段，否则系统将拒绝访问计算字段。

如果在临时架构上设置了身份或主标识，则系统会自动执行任何关联的数据卫生请求，并清理与标识列关联的数据集中的数据。

## 后续步骤

阅读本文档后，您对如何向通过查询服务CTAS查询创建的临时架构添加数据使用标签有了更好的了解。 如果您尚未这样做，以下文档有助于您更好地了解查询服务中的数据管理工作：

* [临时架构标识](./ad-hoc-schema-identities.md)
* [数据管理](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans)
