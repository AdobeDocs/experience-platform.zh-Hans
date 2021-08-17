---
keywords: 广告；交易台；广告交易台
title: 交易台连接
description: 交易台是一个自助平台，可让广告购买者跨展示、视频和移动设备库存源执行重定位和受众定位的数字促销活动。
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 2%

---

# [!DNL The Trade Desk] 连接

## 概述 {#overview}

[!DNL The Trade Desk] 目标可帮助您将用户档案数据发送到 [!DNL The Trade Desk]。

[!DNL The Trade Desk] 是一个自助平台，可让广告购买者跨展示、视频和移动设备库存源执行重定位和受众定位的数字促销活动。

要将用户档案数据发送到[!DNL Trade Desk]，您必须先连接到目标。

## 用例 {#use-cases}

作为营销人员，我希望能够使用基于[!DNL Trade Desk IDs]或设备ID构建的区段来创建重定位或受众定位的数字营销活动。

## 支持的身份 {#supported-identities}

[!DNL The Trade Desk] 支持激活下表所述的身份。了解有关[identities](/help/identity-service/namespaces.md)的更多信息。

| Target标识 | 描述 |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| 交易台ID | 交易台平台中的广告商ID |

## 导出类型 {#export-type}

**[!DNL Segment export]**  — 将区段（受众）的所有成员导出到目标。

## 先决条件 {#prerequisites}

如果您希望使用[!DNL The Trade Desk]创建您的第一个目标，并且过去(使用Adobe Audience Manager或其他应用程序)未在Experience CloudID服务中启用[ ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前在Audience Manager中设置了[!DNL The Trade Desk]集成，则您设置的ID同步会传递到Platform。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

### 连接参数 {#parameters}

在[设置](../../ui/connect-destination.md)此目标时，必须提供以下信息：

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 帐户ID]**:您的 [!DNL Trade Desk] [!UICONTROL 帐户ID]。
* **[!UICONTROL 服务器位置]**:请咨询您 [!DNL Trade Desk] 的代表您应使用哪个区域服务器。这些是可用的区域服务器，您可以从以下位置进行选择：
   * **[!UICONTROL 欧洲]**
   * **[!UICONTROL 新加坡]**
   * **[!UICONTROL 东京]**
   * **[!UICONTROL 北美洲东]**
   * **[!UICONTROL 北美洲西]**
   * **[!UICONTROL 拉丁美洲]**

## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请参阅[将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md)。

在[区段计划](../../ui/activate-segment-streaming-destinations.md#scheduling)步骤中，您必须在目标平台中手动将区段映射到其相应的ID或友好名称。

在映射区段时，我们建议您使用平台区段名称或更短的区段名称，以便于使用。 但是，目标中的区段ID或名称不需要与Platform帐户中的区段ID或名称匹配。 您在映射字段中插入的任何值都将反映在目标中。

如果您使用多个设备映射(Cookie ID、[!DNL IDFA]、[!DNL GAID])，请确保对所有三个映射使用相同的映射值。 [!DNL The Trade Desk] 将所有区段聚合到单个区段中，并进行设备级别划分。

![区段映射ID](../../assets/common/segment-mapping-id.png)

## 导出的数据 {#exported-data}

要验证数据是否已成功导出到[!DNL The Trade Desk]目标，请检查您的[!DNL Trade Desk]帐户。 如果激活成功，则帐户中会填充受众。
