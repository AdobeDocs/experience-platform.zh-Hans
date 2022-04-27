---
keywords: Google Ad Manager;Google Ad;DoubleClick AdX;DoubleClick;Google Ad Manager;Google Ad Manager;DFP
title: Google Ad Manager连接
description: Google Ad Manager（以前称为DoubleClick for Publishers或DoubleClick AdX）是Google的一个广告服务平台，它为出版商提供了通过视频和移动设备应用程序管理其网站上广告显示的方法。
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 3%

---

# [!DNL Google Ad Manager] 连接

## 概述 {#overview}

[!DNL Google Ad Manager]，以前称为 [!DNL DoubleClick for Publishers] (DFP)或 [!DNL DoubleClick AdX]，是 [!DNL Google] 这为出版商提供了通过视频和移动设备应用程序管理网站上广告显示的方法。

## 目标详情 {#specifics}

请注意以下特定于 [!DNL Google Ad Manager] 目标：

* 激活的受众是在 [!DNL Google] 平台。
* [!DNL Platform] 当前不包括用于验证激活是否成功的测量量度。 请参阅Google中的受众计数，以验证集成并了解受众定位大小。

## 支持的标识 {#supported-identities}

[!DNL Google Ad Manager] 支持激活下表所述的身份。

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 如果源标识是GAID命名空间，请选择此目标标识。 |
| IDFA | [!DNL Apple ID for Advertisers] | 如果源标识是IDFA命名空间，请选择此目标标识。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也称为 [!DNL Device ID]. 一个38位数的数字设备ID，Audience Manager会将其与之交互的每个设备相关联。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) 来定位加利福尼亚州的用户，以及所有其他用户的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 会使用此ID来定位加州以外的用户。 |
| RIDA | 用于广告的Roku ID。 此ID唯一标识Roku设备。 |  |
| 女佣 | Microsoft广告ID。 此ID唯一标识运行Windows 10的设备。 |  |
| Amazon Fire TV ID | 此ID可唯一标识Amazon Fire TV。 |  |

{style=&quot;table-layout:auto&quot;}

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您将区段（受众）的所有成员导出到Google目标。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 先决条件 {#prerequisites}

如果您希望通过 [!DNL Google Ad Manager] 尚未启用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在过去的Experience CloudID服务(使用Audience Manager或其他应用程序)中，请联系Adobe咨询或客户关怀团队以启用ID同步。 如果您之前已设置 [!DNL Google] 集成时，您设置的ID同步会传递到Platform。

### 允许列表 {#allow-listing}

>[!NOTE]
>
>允许列表在设置第一个 [!DNL Google Ad Manager] 目标。 请确保已完成下述允许列表流程 [!DNL Google] 创建目标之前。

在创建 [!DNL Google Ad Manager] 目标，您必须联系 [!DNL Google] Adobe添加到允许的数据提供程序列表，以及将帐户添加到允许列表。 联系人 [!DNL Google] 并提供以下信息：

* **帐户ID**:Adobe的帐户ID与Google。 帐户ID:87933855。
* **客户ID**:Adobe的客户帐户ID和Google。 客户ID:89690775。
* **网络ID**:这是你的帐户 [!DNL Google Ad Manager]
* **受众链接ID**:这是你的帐户 [!DNL Google Ad Manager]
* 您的帐户类型。 由Google或AdX购买者提供的DFP。

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md).

### 连接参数 {#parameters}

While [设置](../../ui/connect-destination.md) 此目标中，您必须提供以下信息：

* **[!UICONTROL 名称]**:填写此目标的首选名称。
* **[!UICONTROL 描述]**:可选。 例如，您可以提及您使用此目标的促销活动。
* **[!UICONTROL 帐户类型]**:根据您使用Google的帐户选择一个选项：
   * 使用 `DFP by Google` 表示 [!DNL DoubleClick] （发布者）
   * 使用 `AdX buyer` 表示 [!DNL Google AdX]
* **[!UICONTROL 帐户ID]**:使用 [!DNL Google]. 这可以是您的网络ID或受众链接ID。 通常，这是一个八位数的ID。

>[!NOTE]
>
>设置 [!DNL Google Ad Manager] 目标，请与您的 [!DNL Google Account Manager] 或Adobe代表，了解您拥有的帐户类型。

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

请参阅 [将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

## 导出的数据 {#exported-data}

验证数据是否已成功导出到 [!DNL Google Ad Manager] 目标位置，检查 [!DNL Google Ad Manager] 帐户。 如果激活成功，则帐户中会填充受众。
