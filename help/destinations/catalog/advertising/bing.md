---
keywords: '广告；bing; '
title: Microsoft Bing连接
description: 通过Microsoft Bing连接目标，您可以跨Microsoft显示广告执行重定位和受众定位的数字促销活动。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 169a7ad1adfa3282bd0503ce277373b654ec57cd
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 1%

---

# [!DNL Microsoft Bing] 连接 {#bing-destination}

## 概述 {#overview}

的 [!DNL Microsoft Bing] 目标可帮助您将用户档案数据发送到 [!DNL Microsoft Display Advertising].

将用户档案数据发送到 [!DNL Microsoft Bing]，则必须先连接到目标。

## 用例 {#use-cases}

作为营销人员，我希望能够使用 [!DNL Microsoft Advertising IDs] 通过 [!DNL Microsoft Advertising] 渠道。

## 支持的身份 {#supported-identities}

[!DNL Microsoft Bing] 支持激活下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 |
|---|---|
| 女佣 | Microsoft Advertising ID |

## 导出类型 {#export-type}

**[!DNL Segment Export]**  — 将区段（受众）的所有成员导出到 [!DNL Microsoft Bing] 目标。

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>如果您希望通过 [!DNL Microsoft Bing] 尚未启用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在过去的Experience CloudID服务(使用Adobe Audience Manager或其他应用程序)中，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前已设置 [!DNL Microsoft Bing] 集成时，您设置的ID同步会传递到Platform。

配置目标时，必须提供以下信息：

* [!UICONTROL 帐户ID]:这是您的 [!DNL Bing Ads CID]，格式为整数。

## 连接到目标 {#connect}

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 帐户ID]**:您的 [!DNL Bing Ads CID].

## 将区段激活到此目标 {#activate}

请参阅 [将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

在 [区段计划](../../ui/activate-segment-streaming-destinations.md#scheduling) 步骤中，您必须手动将区段映射到目标中相应的ID或友好名称。

在映射区段时，我们建议您使用 [!DNL Platform] 区段名称或更短的形式，以便于使用。 但是，您目标中的区段ID或名称不需要与 [!DNL Platform] 帐户。 您在映射字段中插入的任何值都将反映在目标中。

## 导出的数据 {#exported-data}

验证数据是否已成功导出到 [!DNL Microsoft Bing] 目标位置，检查 [!DNL Microsoft Bing Ads] 帐户。 如果激活成功，则帐户中会填充受众。
