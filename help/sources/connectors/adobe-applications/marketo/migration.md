---
title: 使用Marketo Engage源将ECID映射从人员迁移到Activity
description: 了解如何使用Marketo Engage源将ECID映射从人员数据集迁移到活动数据集。
exl-id: bcc91c53-aeca-4d7c-89b5-cf025d0357a0
source-git-commit: d03fcf06fb63ad2484ded3b85fc11ae45661babc
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 将ECID映射从[!DNL Person]数据集迁移到[!DNL Activity]数据集

您可以将ECID映射从[!DNL Marketo Engage Person]数据集迁移到[!DNL Activity]数据集，以便提供更稳定的数据摄取和身份管理行为。 此外，此迁移将处理以下问题：

| 问题 | 解决方案 |
| --- | --- |
| 当[!DNL Marketo Person]数据集具有指向多个ECID的链接时，当Experience Data Model (XDM)记录中的[身份总数超过20](../../../../identity-service/guardrails.md)时，数据摄取失败。 | 通过将ECID字段映射迁移到[!DNL Activity]，您可以确保来自[!DNL Marketo Person]数据流的标识数保持在限制之内，从而允许数据摄取成功。 |
| 每次使用ECID摄取[!DNL Marketo Person]数据集时，[!DNL Marketo Person]数据集中所有ECID的时间戳将更新为人员记录的上次更新时间戳。 这可能会导致从标识图[&#128279;](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated)中删除最近的标识时不正确。 | 通过将ECID字段映射迁移到[!DNL Activity]，Identity Service可以正确反映ECID的时间戳，并且Identity Service的“先进先出”机制将提供更稳定的行为。 |
| 通过[!DNL Marketo Person]数据流摄取ECID时，新添加的ECID不会摄取到Experience Platform中，除非[!DNL Marketo]中的[!DNL Person]记录有更新。 | 当新的ECID链接到[!DNL Marketo]中的[!DNL Person]记录时，您可以通过[!DNL Marketo Activity]数据流摄取该ECID数据，并在Experience Platform时立即提示标识图更新。 |

基本上，您必须：

* 更新您的[!DNL Marketo Activity]数据流。
* 更新您的[!DNL Marketo Person]数据流。

## 更新[!DNL Marketo Activity]数据流 {#update-activity-dataflow}

请按照以下步骤更新您的[!DNL Marketo Activity]数据流：

* 在Experience PlatformUI中，导航到&#x200B;*源*&#x200B;工作区，并查找[!DNL Marketo Activity]数据的现有数据流。
* 假定数据流已启用，请选择数据流名称旁边的省略号(`...`)，然后选择&#x200B;**[!UICONTROL 更新数据流]**。
* 然后，选择&#x200B;**[!UICONTROL 下一步]**，直至到达&#x200B;*映射*&#x200B;接口。
* 在&#x200B;*映射*&#x200B;界面中，选择&#x200B;**[!UICONTROL 新建字段]**，然后选择&#x200B;**[!UICONTROL 添加计算字段]**。 您必须从此处添加以下内容：

| Source数据集 | XDM目标字段 |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>如果现有[!DNL Marketo]数据流的更新仅包含添加或删除ECID映射字段，则数据流会自动跳过历史回填作业。 只有在“访问网页”和“点击网页”等活动类型发生时，才会发生新的数据摄取。

## 更新[!DNL Marketo Person]数据流 {#update-person-dataflow}

请按照以下步骤更新您的[!DNL Marketo Person]数据流：

* 在Experience PlatformUI中，导航到&#x200B;*源*&#x200B;工作区，并查找[!DNL Marketo Person]数据的现有数据流。
* 假定数据流已启用，请选择数据流名称旁边的省略号(`...`)，然后选择&#x200B;**[!UICONTROL 更新数据流]**。
* 然后，选择&#x200B;**[!UICONTROL 下一步]**，直至到达&#x200B;*映射*&#x200B;接口。
* 在&#x200B;*映射*&#x200B;界面中，删除映射到`identityMap`的计算字段，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;和&#x200B;**[!UICONTROL 保存并摄取]**。

>[!NOTE]
>
>如果现有[!DNL Marketo]数据流的更新仅包含添加或删除ECID映射字段，则数据流会自动跳过历史回填作业。 之前已摄取的ECID的时间戳将保持不变。 只有在摄取与现有ECID对应的新数据时，才会更新这些数据。

## 后续步骤

通过阅读本文档，您现在知道如何将ECID映射从[!DNL Marketo Person]数据集迁移到[!DNL Marketo Activity]数据集。 有关详细信息，请阅读以下[!DNL Marketo]文档：

* [创建数据流以将 [!DNL Marketo] 数据摄取到Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md)。
* [字段映射指南](../mapping/marketo.md)。
