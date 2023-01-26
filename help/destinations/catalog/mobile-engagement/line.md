---
keywords: 移动设备；移动设备参与目标；LINE;LINE移动设备参与目标
title: 线路连接
description: 利用LINE目标，可向Platform区段添加用户档案，并为连接的用户提供个性化体验。
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 1%

---

# [!DNL LINE] 连接

## 概述 {#overview}

[[!DNL LINE]](https://line.me/en/) 是一个热门的通信平台，可连接人员、服务和信息，并且已经从聊天应用程序发展为娱乐、社交和日常活动的中心。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [[!DNL LINE] 消息传送API](https://developers.line.biz/en/reference/messaging-api/). 您可以从Experience Platform区段中激活用户档案，作为 [!DNL LINE] 满足您的业务需求。

[!DNL LINE] 使用载体令牌作为与 [!DNL LINE] 消息传送API。 验证的说明 [!DNL LINE] 实例的后面，在 [对目标进行身份验证](#authenticate) 中。

## 用例 {#use-cases}

作为营销人员，您可以在移动设备参与目标中定位用户，并内置区段 [!DNL Adobe Experience Platform]. 此外，您还可以根据访客的属性，为他们提供个性化体验 [!DNL Adobe Experience Platform] 用户档案，在 [!DNL Adobe Experience Platform].

## 先决条件 {#prerequisites}

### [!DNL LINE] 先决条件 {#prerequisites-destination}

请注意 [!DNL LINE]，以便将数据从Platform导出到 [!DNL LINE] 帐户：

#### 你需要 [!DNL LINE] 帐户 {#prerequisites-account}

您需要注册并创建 [!DNL LINE] 帐户（如果您还没有）。 要创建帐户，请执行以下操作：

1. 导航到 [!DNL LINE] [帐户登录](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) 页面
2. 选择 **[!UICONTROL 创建帐户]**.

#### 收集 [!DNL LINE channel access token (long-lived)] 从 [!DNL LINE] 开发人员控制台 {#gather-credentials}

允许平台访问 [!DNL LINE] 资源，您将需要 *[!DNL Channel access token (long-lived)]* 从所需的 [!DNL LINE] *消息传送API* 渠道。

1. 使用 [!DNL LINE] 帐户 [[!DNL LINE] 开发人员控制台](https://developers.line.biz/console).
1. 接下来，访问 *[!DNL Providers]* 列表，然后选择 *[!DNL Provider]* 最后选择 *消息传送API* 渠道访问其设置。 如果您是首次访问开发人员控制台，请按照 [[!DNL LINE] 文档](https://developers.line.biz/en/docs/messaging-api/getting-started/) 以完成创建提供程序所需的步骤。
1. 最后，导航到 ***[!DNL Channel access token]*** 部分和复制 ***[!DNL Channel access token (long-lived)]*** 值在 [对目标进行身份验证](#authenticate) 中。

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | 您的 [!DNL LINE Channel access token (long-lived)]。 | `aaa2112XSMWqLXR7..........nyilFU=` |

请参阅 [[!DNL LINE] 文档](https://developers.line.biz/en/docs/messaging-api/getting-started/) 以获取有关创建渠道或将渠道添加到现有渠道的指导 [!DNL LINE] 帐户 [!DNL LINE] 开发人员控制台。

## 支持的身份 {#supported-identities}

[!DNL LINE] 支持更新和导出下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 |
|---|---|
| 广告商的ID | 当源标识为IFA时，为广告商(IFA)目标标识选择ID *(适用于广告商的Apple ID)* 或GAID *(Google广告ID)命名空间。 |
| 行用户ID | 当源标识为LINE用户ID时，选择用户ID目标标识。 |

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | 您要导出区段（受众）的所有成员，以及 [!DNL LINE] 目标。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

在 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 搜索 [!DNL LINE]. 或者，您也可以在 **[!UICONTROL 移动参与度]** 类别。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请选择 **[!UICONTROL 连接到目标]**.
![Platform UI屏幕截图，其中显示了如何进行身份验证。](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

填写以下必填字段。
* **[!UICONTROL 载体令牌]**:您的 [!DNL LINE Channel access token (long-lived)] 从 [!DNL LINE] 开发人员控制台。 请参阅 [收集凭据](#gather-credentials) 中。

如果提供的详细信息有效，UI会显示 **[!UICONTROL 已连接]** 状态为绿色复选标记。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![Platform UI屏幕截图，显示目标详细信息。](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL 受众类型]**:选择 **[!UICONTROL 广告商的ID]** 如果要导出的身份类型为 *广告商的ID*. 选择 **[!UICONTROL 行用户ID]** 如果要导出的身份类型为 *行用户ID*. 请参阅 [支持的身份](#supported-identities) 部分以了解有关身份类型的更多信息。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
>
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射属性和标识 {#map}

要将受众数据从Adobe Experience Platform正确发送到 [!DNL LINE] 目标，您需要完成字段映射步骤。 映射包括在Platform帐户中的体验数据模型(XDM)架构字段与目标目标中相应的对等字段之间创建一个链接。 要将XDM字段正确映射到 [!DNL LINE] 目标字段，请执行以下步骤：

必须根据源标识映射以下目标标识命名空间： |目标标识 |源字段 |目标字段 | | — | — | — | |广告商的ID(IFA) | `IDFA` 或 `GAID` | `LineId` | |行用户ID | `UserID` | `LineId` |

如果您的目标身份为 *行用户ID* 您将需要：
![平台UI屏幕截图示例，显示了在将LINE用户ID用于目标标识时的Target映射。](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

如果您的目标标识为 *广告商的ID* 您将需要：
![Platform UI屏幕截图示例，显示了在将ID用于Target标识的广告商(IFA)时Target映射。](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## 验证数据导出 {#exported-data}

成功导出Experience Platform后， [!DNL LINE] 目标在 [!DNL LINE] 使用选定的区段名称。

要验证您是否已正确设置目标，请执行以下步骤：

1. 在 [!DNL LINE]，登录到 [管理器控制台](https://manager.line.biz/).

1. 接下来，导航到 **[!UICONTROL 数据控件]** > **[!UICONTROL 受众]** 并检查与 **[!UICONTROL 受众名称]** 列。

1. 更新的卷将匹配区段中的计数。

1. 的 *类型* 列将提及 **[!UICONTROL 用户ID]** 如果导出的标识类型为 *用户ID*. 同样， *类型* 列将提及 **[!UICONTROL 移动设备广告Id]** 如果导出的标识类型为 *IDFA*.

中的设置示例 [!DNL LINE] 如下所示：
![显示受众卷的行UI屏幕截图。](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](/help/data-governance/home.md).
