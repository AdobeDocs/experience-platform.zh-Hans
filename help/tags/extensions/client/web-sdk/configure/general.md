---
title: SDK实例配置设置
description: 配置Web SDK实例的常规设置。
exl-id: cc22b8b3-88c6-4030-91b4-60e14a3b0f42
source-git-commit: 50881ef9498196f2de5519f050800334019a2586
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 2%

---

# SDK实例配置设置

此配置部分管理Web SDK实例名称、它适用的IMS组织以及要将数据发送到的位置。 默认情况下，实例名为`alloy`。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后在&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上选择[!UICONTROL Adobe Experience Platform Web SDK]。
1. 找到位于展开[!UICONTROL SDK instances]折叠面板正下方的实例名称。

![在标记UI中显示Web SDK标记扩展的一般设置的图像](../assets/web-sdk-ext-general.png)

可以使用以下选项：

## [!UICONTROL Name]

Adobe Experience Platform Web SDK标记扩展支持页面上的多个实例。 该名称用于向多个组织发送数据，而无需重复的Web SDK标记库。 您可以将实例名称更改为任何有效的JavaScript对象名称。

## [!UICONTROL IMS organization ID]

您希望将数据发送到Adobe的组织的ID。 大多数情况下，使用自动填充的默认值。 当页面上有多个实例时，使用您要向其发送数据的第二个组织的值填充此字段。

## [!UICONTROL Edge domain]

扩展发送和接收数据的域。 默认情况下，该字段包含`<COMPANYID>.data.adobedc.net`。 较旧的实施可能包含默认值`edge.adobedc.net`，该值也是有效的。

Adobe建议在大多数情况下使用第一方域。 有关如何设置适用于数据收集的第一方域的说明，请参阅[Adobe管理的证书计划](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert)。 另请参阅JavaScript库文档中的[`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md)，以获取设置此值的指南。
