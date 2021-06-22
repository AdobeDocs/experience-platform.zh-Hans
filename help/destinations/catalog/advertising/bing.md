---
keywords: '广告；bing; '
title: Microsoft Bing连接
description: 通过Microsoft Bing连接目标，您可以在Microsoft Display Advertising中执行重定位和受众定位的数字营销活动。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 2931efa6f67a042255fb1d31c0683f73d817b55b
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# [!DNL Microsoft Bing] 连接  {#bing-destination}

## 概述 {#overview}

[!DNL Microsoft Bing]目标可帮助您将用户档案数据发送到[!DNL Microsoft Display Advertising]。

要将用户档案数据发送到[!DNL Microsoft Bing]，您必须先连接到目标。

## 使用案例{#use-cases}

作为营销人员，我希望能够使用基于[!DNL Microsoft Advertising IDs]的内置区段，通过跨[!DNL Microsoft Advertising]渠道的展示广告来定位用户。

## 支持的标识{#supported-identities}

[!DNL Microsoft Bing] 支持激活下表所述的身份。了解有关[identities](/help/identity-service/namespaces.md)的更多信息。

| Target标识 | 描述 |
|---|---|
| 女佣 | Microsoft Advertising ID |

## 导出类型{#export-type}

**[!DNL Segment Export]**  — 将区段（受众）的所有成员导出到目 [!DNL Microsoft Bing] 标。

## 先决条件 {#prerequisites}

如果您希望使用[!DNL Microsoft Bing]创建您的第一个目标，并且过去(使用Adobe Audience Manager或其他应用程序)未在Experience CloudID服务中启用[ ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了[!DNL Microsoft Bing]集成，则您设置的ID同步会传递到Platform。

配置目标时，必须提供以下信息：

* [!UICONTROL 帐户ID]:这是整 [!DNL Bing Ads CID]数格式的。

## 连接到目标{#connect-destination}

在&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**&#x200B;中，选择[!DNL Microsoft Bing]，然后选择&#x200B;**[!UICONTROL 配置]**。

![配置Microsoft Bing目标](../../assets/catalog/advertising/bing/configure.png)

如果与此目标的连接已存在，则可以在目标卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的更多信息，请参阅目标工作区文档的[Catalog](../../ui/destinations-workspace.md#catalog)部分。

![激活Microsoft Bing目标](../../assets/catalog/advertising/bing/activate.png)

## 身份验证步骤 {#authentication}

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步骤中，必须输入目标连接详细信息：

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 帐户ID]**:您的 [!DNL Bing Ads CID]。
* **[!UICONTROL 营销操作]**:营销操作指示将数据导出到目标的意图。您可以从Adobe定义的营销操作中进行选择，也可以创建自己的营销操作。 有关营销操作的更多信息，请参阅[Adobe Experience Platform中的数据管理](../../../data-governance/policies/overview.md)页面。 有关单个Adobe定义的营销操作的信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

![Microsoft Bing目标身份验证](../../assets/catalog/advertising/bing/authentication.png)

单击&#x200B;**[!UICONTROL 创建目标]**。 您的目标现已创建完成。 如果要稍后激活区段，可以单击[!UICONTROL 保存并退出]，也可以单击[!UICONTROL 下一步]以继续工作流并选择要激活的区段。 无论哪种情况，请参阅下一节（[激活区段](#activate-segments)），以了解工作流的其余部分。

## 激活区段{#activate-segments}

请参阅[将配置文件和区段激活到目标](../../ui/activate-destinations.md#select-attributes) ，以了解有关区段激活工作流的信息。

在[区段计划](../../ui/activate-destinations.md#segment-schedule)步骤中，您必须手动将区段映射到目标中相应的ID或友好名称。

在映射区段时，我们建议您使用[!DNL Platform]区段名称或更短的区段名称，以便于使用。 但是，目标中的区段ID或名称不需要与[!DNL Platform]帐户中的区段ID或名称匹配。 您在映射字段中插入的任何值都将反映在目标中。

![区段映射ID](../../assets/common/segment-mapping-id.png)

## 导出的数据{#exported-data}

要验证数据是否已成功导出到[!DNL Microsoft Bing]目标，请检查您的[!DNL Microsoft Bing Ads]帐户。 如果激活成功，则帐户中会填充受众。
