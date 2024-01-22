---
keywords: 移动设备；移动参与目标；LINE；LINE移动参与目标
title: LINE连接
description: 利用LINE目标，可向平台受众添加用户档案，并为连接的用户提供个性化体验。
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 2%

---

# [!DNL LINE] 连接

## 概述 {#overview}

[[!DNL LINE]](https://line.me/en/) 是一个连接人员、服务和信息的流行通信平台，已从聊天应用程序发展为娱乐、社交和日常活动中心。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [[!DNL LINE] 消息传送API](https://developers.line.biz/en/reference/messaging-api/). 您可以将Experience Platform受众中的配置文件激活为中的连接 [!DNL LINE] 以满足您的业务需求。

[!DNL LINE] 使用持有者令牌作为身份验证机制与 [!DNL LINE] 消息传送API。 向您的验证的说明 [!DNL LINE] 实例如下所述，在 [向目标进行身份验证](#authenticate) 部分。

## 用例 {#use-cases}

作为营销人员，您可以定位移动参与目标中的用户，并内置受众 [!DNL Adobe Experience Platform]. 此外，您还可以根据客户的属性为他们提供个性化体验 [!DNL Adobe Experience Platform] 用户档案，一旦在中更新了受众和用户档案 [!DNL Adobe Experience Platform].

## 先决条件 {#prerequisites}

### [!DNL LINE] 先决条件 {#prerequisites-destination}

请注意中的以下先决条件 [!DNL LINE]，以便将数据从Platform导出到 [!DNL LINE] 帐户：

#### 您需要拥有 [!DNL LINE] 帐户 {#prerequisites-account}

您需要注册并创建 [!DNL LINE] 帐户（如果还没有帐户）。 要创建帐户，请执行以下操作：

1. 导航至 [!DNL LINE] [帐户登录](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) 页面
2. 选择 **[!UICONTROL 创建帐户]**.

#### 收集 [!DNL LINE channel access token (long-lived)] 从 [!DNL LINE] 开发人员控制台 {#gather-credentials}

允许Platform访问 [!DNL LINE] 资源，您将需要 *[!DNL Channel access token (long-lived)]* 从所需 [!DNL LINE] *消息传送API* 渠道。

1. 使用您的登录 [!DNL LINE] 帐户至 [[!DNL LINE] 开发人员控制台](https://developers.line.biz/console).
1. 接下来，访问 *[!DNL Providers]* 列表，然后选择 *[!DNL Provider]* ，并最终选择 *消息传送API* 用于访问其设置的渠道。 如果您是首次访问开发人员控制台，请按照 [[!DNL LINE] 文档](https://developers.line.biz/en/docs/messaging-api/getting-started/) 完成创建提供程序所需的步骤。
1. 最后，导航到 ***[!DNL Channel access token]*** 部分并复制 ***[!DNL Channel access token (long-lived)]*** 以下范围中所需的值： [向目标进行身份验证](#authenticate) 步骤。

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | 您的 [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

请参阅 [[!DNL LINE] 文档](https://developers.line.biz/en/docs/messaging-api/getting-started/) 有关创建渠道或向现有渠道添加渠道的指导 [!DNL LINE] 帐户通过 [!DNL LINE] 开发人员控制台。

## 支持的身份 {#supported-identities}

[!DNL LINE] 支持更新和导出下表中描述的标识。 了解有关 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 |
|---|---|
| 广告商ID(IFA) | 当源标识为IFA时，为广告商(IFA)目标标识选择ID *(适用于广告商的Apple ID)* 或GAID *(Google Advertising ID)命名空间。 |
| 行用户ID | 当源标识为LINE用户ID时，选择UserID目标标识。 |

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正使用 [!DNL LINE] 目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

范围 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 搜索 [!DNL LINE]. 或者，您可以将其定位到 **[!UICONTROL 移动参与]** 类别。

### 验证目标 {#authenticate}

要验证目标，请选择 **[!UICONTROL 连接到目标]**.
![显示如何进行身份验证的平台UI屏幕截图。](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

填写下面的必填字段。
* **[!UICONTROL 持有者令牌]**：您的 [!DNL LINE Channel access token (long-lived)] 从 [!DNL LINE] 开发人员控制台。 请参阅 [收集凭据](#gather-credentials) 部分。

如果提供的详细信息有效，UI将显示 **[!UICONTROL 已连接]** 带有绿色复选标记的状态。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![显示目标详细信息的平台UI屏幕截图。](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 受众类型]**：选择 **[!UICONTROL 广告商ID(IFA)]** 如果要导出的标识的类型为 *广告商ID(IFA)*. 选择 **[!UICONTROL 行用户ID]** 如果要导出的标识的类型为 *行用户ID*. 请参阅 [支持的身份](#supported-identities) 部分，以了解有关身份类型的更多信息。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将用户档案和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

### 映射属性和身份 {#map}

要正确地将受众数据从Adobe Experience Platform发送到 [!DNL LINE] 目标，您需要执行字段映射步骤。 映射包括在您的Platform帐户中的Experience Data Model (XDM)架构字段与其在目标目标中的相应等效字段之间创建链接。 要将XDM字段正确映射到 [!DNL LINE] 目标字段，请执行以下步骤：

根据您的源身份，必须映射以下目标身份命名空间： | 目标身份 | 源字段 | 目标字段 | | — | — | — | | 广告商ID(IFA) | `IDFA` 或 `GAID` | `LineId` | | 行用户ID | `UserID` | `LineId` |

如果您的目标身份为 *行用户ID* 您将需要以下各项：
![Platform UI屏幕截图示例，显示将LINE用户ID用于目标身份时的Target映射。](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

如果您的目标身份为 *广告商ID(IFA)* 您将需要以下各项：
![平台UI屏幕截图示例，显示了在将广告商ID (IFA)用于Target身份时的Target映射。](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## 验证数据导出 {#exported-data}

成功从Experience Platform中导出数据后， [!DNL LINE] 目标在中创建新受众 [!DNL LINE] 使用选定的受众名称。

要验证您是否正确设置了目标，请执行以下步骤：

1. 在 [!DNL LINE]，登录到 [管理器控制台](https://manager.line.biz/).

1. 接下来，导航到 **[!UICONTROL 数据控件]** > **[!UICONTROL 受众]** 并检查与中选定受众匹配的名称 **[!UICONTROL 受众名称]** 列。

1. 更新的卷将匹配区段中的计数。

1. 此 *类型* 栏将提及 **[!UICONTROL 用户ID]** 如果您导出的标识属于类型 *用户ID*. 同样地， *类型* 栏将提及 **[!UICONTROL 移动广告ID]** 如果您导出的标识属于类型 *IDFA*.

中的设置示例 [!DNL LINE] 如下所示：
![显示受众数量的LINE UI屏幕截图。](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](/help/data-governance/home.md).
