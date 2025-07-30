---
title: 编辑目标
type: Tutorial
description: 了解如何在Adobe Experience Platform UI中编辑和更新现有目标帐户
badgeBeta: label="Beta 版" type="Informative"
exl-id: f3298836-668b-43fb-b4f3-85a650766f05
source-git-commit: 990fe9162c5b2970f269a5b0668916b7b6e61f44
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 编辑目标

了解如何编辑现有目标连接的各种组件，包括如何使用Experience Platform UI更新身份验证凭据、导出位置等。

>[!IMPORTANT]
>
>此功能处于测试阶段，仅向部分客户提供。 要请求访问权限，请与 Adobe 代表联系。

>[!NOTE]
>
> 此外，还通过API操作支持本教程中描述的编辑操作。 阅读有关如何[编辑API中的目标](/help/destinations/api/edit-destination.md)的教程以了解更多信息。

要编辑现有目标连接的各种组件，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 浏览]**。
2. 选择要编辑的所需目标。
3. 选择`...`名称[!UICONTROL 列中的省略号(])，并使用![编辑目标控件](/help/images/icons/edit.png)**[!UICONTROL 编辑目标&#x200B;]**&#x200B;控件编辑现有目标连接。
4. 在模式窗口中，编辑任何所需的设置。 完成时选择&#x200B;**[!UICONTROL 保存]**。

在“编辑目标”窗口中，可以更新最初连接到目标时配置的任何设置。 这些设置因要更新的目标平台而异。

根据目标的配置方式，某些字段可能是只读的，无法编辑。 要更改只读字段的值，您必须[使用新字段值](../ui/connect-destination.md)创建新的目标连接。

![显示只读字段的屏幕截图。](../assets/ui/edit-destinations/read-only.png)

以下是您可以为[Amazon S3](../catalog/cloud-storage/amazon-s3.md)、[Azure事件中心](../catalog/cloud-storage/azure-event-hubs.md)和[Google Ads](../catalog/advertising/google-ads-destination.md)目标更新的设置示例。

<div style="display: flex; gap: 12px; justify-content: flex-start; align-items: flex-start;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-amazon-s3-connection.png" alt="编辑Amazon S3目标的目标屏幕。" style="max-width: 200px; height: auto; border: 1px solid #ccc;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-eventhubs-connection.png" alt="编辑Azure EventHubs目标的目标屏幕。" style="max-width: 200px; height: auto; border: 1px solid #ccc;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-google-ads-connection.png" alt="编辑Google广告目标的目标屏幕。" style="max-width: 200px; height: auto; border: 1px solid #ccc;">
</div>

>[!SUCCESS]
>
>您的目标连接设置现已更新。

## 其他编辑选项

通过使用Experience Platform UI或流服务API，您可以编辑各种目标配置，如以下链接中所述：

| 使用Experience Platform UI | 使用流服务API |
|---------|----------|
| 编辑目标连接（本页） | [编辑目标连接组件（存储位置和其他组件）](/help/destinations/api/edit-destination.md#patch-target-connection) |
| [编辑帐户](/help/destinations/ui/update-accounts.md) | [编辑基本连接组件（身份验证参数和其他组件）](/help/destinations/api/edit-destination.md#patch-base-connection) |
| [编辑激活数据流](/help/destinations/ui/edit-activation.md) | [更新目标数据流](/help/destinations/api/update-destination-dataflows.md) |

## 后续步骤

通过学习本教程，您已成功使用&#x200B;**[!UICONTROL 目标]**&#x200B;工作区来更新现有的目标连接。

有关目标的详细信息，请参阅[目标概述](../catalog/overview.md)。
