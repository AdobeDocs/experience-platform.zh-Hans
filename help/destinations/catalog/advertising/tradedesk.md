---
keywords: 广告；贸易部门；广告贸易
title: 贸易台连接
description: 交易台是一个自助平台，可供广告购买者跨展示广告、视频和移动库存源执行重定向和受众目标数字活动。
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
translation-type: tm+mt
source-git-commit: 5b72433fcf2318f98538278c6d2650b366e391a2
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# [!DNL The Trade Desk] 连接

## 概述 {#overview}

[!DNL The Trade Desk] 目标可帮助您将用户档案数据发送 [!DNL The Trade Desk]到。

[!DNL The Trade Desk] 是一个自助平台，让广告购买者能够跨展示、视频和移动库存源执行重定向和受众目标数字活动。

要将用户档案数据发送到[!DNL Trade Desk]，您必须首先连接到目标。

## 用例 {#use-cases}

作为营销人员，我希望能够使用由[!DNL Trade Desk IDs]或设备ID构建的细分来创建重定向或受众目标数字活动。

## 支持的身份{#supported-identities}

[!DNL The Trade Desk] 支持下表所述身份的激活。了解有关[identities](/help/identity-service/namespaces.md)的更多信息。

| 目标身份 | 描述 |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| 交易台ID | Trade Desk平台中的广告商ID |

## 导出类型{#export-type}

**[!DNL Segment export]**  — 您要将区段(受众)的所有成员导出到目标。

## 先决条件 {#prerequisites}

如果您希望使用[!DNL The Trade Desk]创建您的第一个目标，并且过去(使用Adobe Audience Manager或其他应用程序)未启用Experience Cloud ID服务中的[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，请联系Adobe咨询或客户服务部门以启用ID同步。 如果您之前在Audience Manager中设置了[!DNL The Trade Desk]集成，则您设置的ID同步将结转到平台。

## 连接到目标{#connect-destination}

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，选择[!DNL The Trade Desk]，然后选择&#x200B;**[!UICONTROL Configure]**。

![配置交易台目标](../../assets/catalog/advertising/tradedesk/configure.png)

如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL Activate]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的详细信息，请参阅目标工作区文档的[目录](../../ui/destinations-workspace.md#catalog)部分。

![激活交易台目标](../../assets/catalog/advertising/tradedesk/activate.png)

## 身份验证步骤{#authentication}

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步骤中，需要输入[!DNL The Trade Desk]连接详细信息：

* **[!UICONTROL Name]**:将来用于识别此目标的名称。
* **[!UICONTROL Description]**:将帮助您在将来确定此目标的描述。
* **[!UICONTROL Account ID]**:您的 [!DNL Trade Desk] [!UICONTROL Account ID]。
* **[!UICONTROL Server Location]**:询问您 [!DNL Trade Desk] 的代表您应使用哪个区域服务器。这些是可用的区域服务器，您可以从以下位置进行选择：

   * **[!UICONTROL Europe]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL North America East]**
   * **[!UICONTROL North America West]**
   * **[!UICONTROL Latin America]**

* **[!UICONTROL Marketing action]**:营销活动指示要将数据导出到目标的目的。您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅Adobe Experience Platform](../../../data-governance/policies/overview.md)中的[数据治理页面。 有关各个Adobe定义的营销操作的信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

![交易台身份验证步骤](../../assets/catalog/advertising/tradedesk/authenticate.png)

单击 **[!UICONTROL Create destination]**。您的目标现在已创建。 如果您希望稍后激活区段，可单击[!UICONTROL Save & Exit]，也可以选择[!UICONTROL Next]继续工作流并选择要激活的区段。 在任一情况下，请参阅工作流其余部分的下一节[激活区段](#activate-segments)。

## 激活区段{#activate-segments}

有关区段用户档案工作流的信息，请参阅[将激活和区段激活到目标](../../ui/activate-destinations.md#select-attributes)。

在[区段计划](../../ui/activate-destinations.md#segment-schedule)步骤中，您必须手动将区段映射到目标中的相应ID或友好名称。

在映射区段时，建议您使用[!DNL Platform]区段名称或更短的区段名称，以便于使用。 但是，目标中的区段ID或名称不需要与[!DNL Platform]帐户中的区段ID或名称匹配。 您在映射字段中插入的任何值都将反映在目标中。

如果您使用多个设备映射(cookie ID、[!DNL IDFA]、[!DNL GAID])，请确保对所有三个映射使用相同的映射值。 [!DNL The Trade Desk] 将所有这些组件聚合到单个细分中，并进行设备级细分。

![区段映射ID](../../assets/common/segment-mapping-id.png)

## 导出的数据{#exported-data}

要验证数据是否已成功导出到[!DNL The Trade Desk]目标，请检查您的[!DNL Trade Desk]帐户。 如果激活成功，则受众将填充到您的帐户中。
