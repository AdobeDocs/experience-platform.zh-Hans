---
title: 使用Marketo Engage源将ECID映射从人员迁移到Activity
description: 了解如何使用Marketo Engage源将ECID映射从人员数据集迁移到活动数据集。
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 迁移ECID映射自 [!DNL Person] 数据集到 [!DNL Activity] 数据集

您可以从以下位置迁移ECID映射 [!DNL Marketo Engage Person] 数据集到 [!DNL Activity] 数据集以提供更稳定的数据摄取和身份管理行为。 此外，此迁移将处理以下问题：

| 问题 | 解决方案 |
| --- | --- |
| 当 [!DNL Marketo Person] 数据集具有指向多个ECID的链接，在以下情况下，数据摄取失败： [Experience Data Model (XDM)记录中的身份总数超过20](../../../../identity-service/guardrails.md). | 通过将ECID字段映射迁移到 [!DNL Activity]，您可以确保 [!DNL Marketo Person] 数据流保持在限制内，因此允许数据摄取成功。 |
| 每当 [!DNL Marketo Person] 数据集是使用ECID摄取的，这是来自的所有ECID上的时间戳。 [!DNL Marketo Person] 使用人员记录的上次更新时间戳更新数据集。 这会导致 [从身份图中删除最近的身份不正确](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | 通过将ECID字段映射迁移到 [!DNL Activity]，Identity Service可以正确反映ECID的时间戳，并且Identity Service的“先进先出”机制将提供更稳定的行为。 |
| 通过摄取ECID时 [!DNL Marketo Person] 数据流时，新添加的ECID不会被摄取到Experience Platform中，除非对 [!DNL Person] 记录位置 [!DNL Marketo]. | 当新的ECID链接到 [!DNL Person] 记录位置 [!DNL Marketo]，您可以通过摄取该ECID数据 [!DNL Marketo Activity] 数据流并在Experience Platform时立即提示更新身份图。 |

基本上，您必须：

* 更新您的 [!DNL Marketo Activity] 数据流。
* 更新您的 [!DNL Marketo Person] 数据流。

## 更新 [!DNL Marketo Activity] 数据流 {#update-activity-dataflow}

请按照以下步骤更新您的 [!DNL Marketo Activity] 数据流：

* 在Experience PlatformUI中，导航到 *源* 工作区并查找现有数据流 [!DNL Marketo Activity] 数据。
* 鉴于数据流已启用，请选择省略号(`...`)，然后选择 **[!UICONTROL 更新数据流]**.
* 然后，选择 **[!UICONTROL 下一个]** 直到您到达 *映射* 界面。
* 在 *映射* 界面，选择 **[!UICONTROL 新建字段]** 然后选择 **[!UICONTROL 添加计算字段]**. 您必须从此处添加以下内容：

| 源数据集 | XDM目标字段 |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>如果您更新到现有的 [!DNL Marketo] 数据流仅由添加或删除ECID映射字段组成，然后数据流自动跳过历史回填作业。 只有在“访问网页”和“点击网页”等活动类型发生时，才会发生新的数据摄取。

## 更新 [!DNL Marketo Person] 数据流 {#update-person-dataflow}

请按照以下步骤更新您的 [!DNL Marketo Person] 数据流：

* 在Experience PlatformUI中，导航到 *源* 工作区并查找现有数据流 [!DNL Marketo Person] 数据。
* 鉴于数据流已启用，请选择省略号(`...`)，然后选择 **[!UICONTROL 更新数据流]**.
* 然后，选择 **[!UICONTROL 下一个]** 直到您到达 *映射* 界面。
* 在 *映射* 界面，删除映射到的计算字段 `identityMap` 然后选择 **[!UICONTROL 下一个]** 和 **[!UICONTROL 保存并摄取]**.

>[!NOTE]
>
>如果您更新到现有的 [!DNL Marketo] 数据流仅由添加或删除ECID映射字段组成，然后数据流自动跳过历史回填作业。 之前已摄取的ECID的时间戳将保持不变。 只有在摄取与现有ECID对应的新数据时，才会更新这些数据。

## 后续步骤

通过阅读本文档，您现在知道如何从 [!DNL Marketo Person] 数据集到 [!DNL Marketo Activity] 数据集。 有关详细信息，请阅读以下内容 [!DNL Marketo] 文档：

* [创建数据流以进行摄取 [!DNL Marketo] 要Experience Platform的数据](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [字段映射指南](../mapping/marketo.md).