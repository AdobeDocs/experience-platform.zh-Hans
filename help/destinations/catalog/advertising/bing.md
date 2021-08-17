---
keywords: '广告；bing; '
title: Microsoft Bing连接
description: 通过Microsoft Bing连接目标，您可以在Microsoft Display Advertising中执行重定位和受众定位的数字营销活动。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 1%

---

# [!DNL Microsoft Bing] 连接 {#bing-destination}

## 概述 {#overview}

[!DNL Microsoft Bing]目标可帮助您将用户档案数据发送到[!DNL Microsoft Display Advertising]。

要将用户档案数据发送到[!DNL Microsoft Bing]，您必须先连接到目标。

## 用例 {#use-cases}

作为营销人员，我希望能够使用基于[!DNL Microsoft Advertising IDs]的内置区段，通过跨[!DNL Microsoft Advertising]渠道的展示广告来定位用户。

## 支持的身份 {#supported-identities}

[!DNL Microsoft Bing] 支持激活下表所述的身份。了解有关[identities](/help/identity-service/namespaces.md)的更多信息。

| Target标识 | 描述 |
|---|---|
| 女佣 | Microsoft Advertising ID |

## 导出类型 {#export-type}

**[!DNL Segment Export]**  — 将区段（受众）的所有成员导出到目 [!DNL Microsoft Bing] 标。

## 先决条件 {#prerequisites}

如果您希望使用[!DNL Microsoft Bing]创建您的第一个目标，并且过去(使用Adobe Audience Manager或其他应用程序)未在Experience CloudID服务中启用[ ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了[!DNL Microsoft Bing]集成，则您设置的ID同步会传递到Platform。

配置目标时，必须提供以下信息：

* [!UICONTROL 帐户ID]:这是整 [!DNL Bing Ads CID]数格式的。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 帐户ID]**:您的 [!DNL Bing Ads CID]。

## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请参阅[将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md)。

在[区段计划](../../ui/activate-segment-streaming-destinations.md#scheduling)步骤中，您必须手动将区段映射到目标中相应的ID或友好名称。

在映射区段时，我们建议您使用[!DNL Platform]区段名称或更短的区段名称，以便于使用。 但是，目标中的区段ID或名称不需要与[!DNL Platform]帐户中的区段ID或名称匹配。 您在映射字段中插入的任何值都将反映在目标中。

## 导出的数据 {#exported-data}

要验证数据是否已成功导出到[!DNL Microsoft Bing]目标，请检查您的[!DNL Microsoft Bing Ads]帐户。 如果激活成功，则帐户中会填充受众。
