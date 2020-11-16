---
keywords: advertising; bing;
title: Microsoft Bing目标
seo-title: Microsoft Bing目标可帮助您将用户档案数据发送到Microsoft Display Advertising。
description: 通过Microsoft Bing目标，您可以跨Microsoft展示广告执行重定位和受众目标数字活动。
seo-description: 通过Microsoft Bing目标，您可以跨Microsoft展示广告执行重定位和受众目标数字活动。
translation-type: tm+mt
source-git-commit: 43795e31f4e39dcabeaf6d69529e80cabe9c90c5
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---


# [!DNL Microsoft Bing] 目标

## 概述 {#overview}

目 [!DNL Microsoft Bing] 标可帮助您将用户档案数据发送 [!DNL Microsoft Display Advertising]到。

要将用户档案数据发 [!DNL Microsoft Bing]送到，必须先连接到目标。

## 目标规范 {#destination-specs}

请注意特定于目标的以下详细 [!DNL Microsoft Bing] 信息：

* 您可以将以下身份 [发送](../../identity-service/namespaces.md) 到目 [!DNL Microsoft Bing] 标： [!DNL Microsoft ID].

## 用例 {#use-cases}

作为营销人员，我希望能够通过跨目标的展示广告，使 [!DNL Microsoft Advertising IDs] 用由渠道用户构成的 [!DNL Microsoft Advertising] 细分。

## 导出类型 {#export-type}

**[!DNL Segment Export]** -您将区段(受众)的所有成员导出到目 [!DNL Microsoft Bing] 标。

## 先决条件 {#prerequisites}

配置目标时，您将要求提供以下信息：

* [!UICONTROL 帐户ID]:这是整 [!DNL Bing Ads CID]数格式的。

## 连接到目标 {#connect-destination}

1. 在“ **[!UICONTROL 连接]** ”>“ **[!UICONTROL 目标]**”中 [!DNL Microsoft Bing]，选 **[!UICONTROL 择并选择“]**&#x200B;配置”。

   ![配置Microsoft Bing目标](assets/bing-destination-configure.png)

   >[!NOTE]
   >
   >如果与此目标的连接已存在，您可以在目标卡 **[!UICONTROL 上看到]** “激活”按钮。 有关激活和配置之 **[!UICONTROL 间差异]** 的详 **[!UICONTROL 细信]**&#x200B;息，请参 [阅目标工](../destinations/destinations-workspace.md#catalog) 作区文档的“目录”部分。

   ![激活Microsoft Bing目标](assets/bing-destination-activate.png)

1. 在身份验证 [!UICONTROL 步骤] ，您必须输入目标连接详细信息：

   * **[!UICONTROL 名称]**:将来用于识别此目标的名称。
   * **[!UICONTROL 描述]**:将来帮助您识别此目标的描述。
   * **[!UICONTROL 帐户ID]**:您的 [!DNL Bing Ads CID]。
   * **[!UICONTROL 营销用例]**:市场营销用例指明要将数据导出到目标的目的。 您可以从Adobe定义的营销用例中进行选择，也可以创建自己的营销用例。 有关市场营销用例的更多信息，请参 [阅Adobe Experience Platform的数据管](../privacy/data-governance-overview.md#destinations) 理页。 有关各个Adobe定义的营销用例的信息，请参阅数据 [使用策略概述](../../data-governance/policies/overview.md#core-actions)。

   ![Microsoft Bing目标身份验证](assets/bing-destination-authentication.png)

1. 单击“ **[!UICONTROL 创建目标]**”。 您的目标现在已创建。 如果要稍后 [!UICONTROL 激活区段] ，可单击保存并退出，也可单击下 [!UICONTROL 一步] ，继续工作流并选择要激活的区段。 在任一情况下，请参阅下一 [节激活](#activate-segments)“区段”，了解工作流的其余部分。

## 激活区段 {#activate-segments}

有关 [区段用户档案工作流的信息](activate-destinations.md#select-attributes) ，请参阅将激活和区段激活到目标。

在“区 [段计划](activate-destinations.md#segment-schedule) ”步骤中，您必须手动将区段映射到目标中相应的ID或友好名称。

在映射区段时，建议您使 [!DNL Platform] 用区段名称或更短的区段名称，以便于使用。 但是，目标中的区段ID或名称不需要与帐户中的区段ID或名称匹 [!DNL Platform] 配。 您在映射字段中插入的任何值都将反映在目标中。

![区段映射ID](assets/segment-mapping-id.png)

## 导出的数据 {#exported-data}

要验证数据是否已成功导出到目 [!DNL Microsoft Bing] 标，请检查您的 [!DNL Microsoft Bing Ads] 帐户。 如果激活成功，则受众将填充到您的帐户中。