---
keywords: '广告；bing; '
title: Microsoft Bing连接
description: 通过Microsoft Bing连接目标，您可以跨Microsoft Display Advertising执行重定位和受众目标数字活动。
translation-type: tm+mt
source-git-commit: 0ef107963f7da377070eb845fd7c24218a99464b
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---


# [!DNL Microsoft Bing] 连接  {#bing-destination}

[!DNL Microsoft Bing]目标可帮助您向[!DNL Microsoft Display Advertising]发送用户档案数据。

要将用户档案数据发送到[!DNL Microsoft Bing]，您必须首先连接到目标。

## 目标规范{#destination-specs}

请注意特定于[!DNL Microsoft Bing]目标的以下详细信息：

* 可以将以下[identities](../../../identity-service/namespaces.md)发送到[!DNL Microsoft Bing]目标：[!DNL Microsoft ID]。

>[!IMPORTANT]
>
>如果您希望使用[!DNL Microsoft Bing]创建您的第一个目标，并且过去(使用Adobe Audience Manager或其他应用程序)未启用Experience Cloud ID服务中的[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，请联系Adobe咨询或客户服务部门以启用ID同步。 如果您之前在Audience Manager中设置了[!DNL Microsoft Bing]集成，则您设置的ID同步将结转到平台。

## 用例 {#use-cases}

作为营销人员，我希望能够通过跨[!DNL Microsoft Advertising]渠道的展示广告，将[!DNL Microsoft Advertising IDs]的细分用于目标用户。

## 导出类型{#export-type}

**[!DNL Segment Export]**  — 您将区段(受众)的所有成员导出到目 [!DNL Microsoft Bing] 标。

## 先决条件 {#prerequisites}

配置目标时，必须提供以下信息：

* [!UICONTROL 帐户ID]:这是您的 [!DNL Bing Ads CID]整数格式。

## 连接到目标{#connect-destination}

在&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**&#x200B;中，选择[!DNL Microsoft Bing]，然后选择&#x200B;**[!UICONTROL 配置]**。

![配置Microsoft Bing目标](../../assets/catalog/advertising/bing/configure.png)

>[!NOTE]
>
>如果与此目标的连接已存在，您可以在目标卡上看到&#x200B;**[!UICONTROL 激活]**&#x200B;按钮。 有关&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之间差异的详细信息，请参阅目标工作区文档的[Catalog](../../ui/destinations-workspace.md#catalog)部分。
>
>![激活Microsoft Bing目标](../../assets/catalog/advertising/bing/activate.png)

在[!UICONTROL 身份验证]步骤中，必须输入目标连接详细信息：

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:将帮助您在将来确定此目标的描述。
* **[!UICONTROL 帐户ID]**:您的 [!DNL Bing Ads CID]。
* **[!UICONTROL 营销活动]**:营销活动指示要将数据导出到目标的目的。您可以从Adobe定义的营销活动中进行选择，也可以创建自己的营销活动。 有关营销操作的详细信息，请参阅Adobe Experience Platform](../../../data-governance/policies/overview.md)中的[数据治理页面。 有关各个Adobe定义的营销操作的信息，请参阅[数据使用策略概述](../../../data-governance/policies/overview.md)。

![Microsoft Bing目标身份验证](../../assets/catalog/advertising/bing/authentication.png)

单击&#x200B;**[!UICONTROL 创建目标]**。 您的目标现在已创建。 如果您希望稍后激活区段，可单击[!UICONTROL 保存并退出]，或单击[!UICONTROL 下一步]继续工作流并选择要激活的区段。 在任一情况下，请参阅工作流其余部分的下一节[激活区段](#activate-segments)。

## 激活区段{#activate-segments}

有关区段用户档案工作流的信息，请参阅[将激活和区段激活到目标](../../ui/activate-destinations.md#select-attributes)。

在[区段计划](../../ui/activate-destinations.md#segment-schedule)步骤中，您必须手动将区段映射到目标中的相应ID或友好名称。

在映射区段时，建议您使用[!DNL Platform]区段名称或更短的区段名称，以便于使用。 但是，目标中的区段ID或名称不需要与[!DNL Platform]帐户中的区段ID或名称匹配。 您在映射字段中插入的任何值都将反映在目标中。

![区段映射ID](../../assets/common/segment-mapping-id.png)

## 导出的数据{#exported-data}

要验证数据是否已成功导出到[!DNL Microsoft Bing]目标，请检查您的[!DNL Microsoft Bing Ads]帐户。 如果激活成功，则受众将填充到您的帐户中。