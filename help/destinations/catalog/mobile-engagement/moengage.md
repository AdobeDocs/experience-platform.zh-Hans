---
title: Moengage连接
description: Moengage是一个客户参与平台，可实时支持消费者和品牌之间以客户为中心的互动。
last-substantial-update: 2023-10-11T00:00:00Z
exl-id: 051f1a10-3c41-4c0a-b187-bf80de0565f0
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---

# [!DNL Moengage] 连接

## 概述 {#overview}

使用 [!DNL Moengage] 用于实时将Adobe数据（用户属性、区段和事件）连接并映射到MoEngage的目标。 然后，客户可以根据这些数据采取行动，提供个性化、有针对性的体验。

通过Adobe，集成非常简单直观。 只需获取任何Adobe用户配置文件，并将其映射到MoEngage用户属性即可。

>[!IMPORTANT]
>
>此目标连接器和文档页面由 *Moengage* 团队。 如有任何查询或更新请求，请直接通过以下电子邮件联系他们： *`https://help.moengage.com/hc/en-us`.*

## 用例 {#use-cases}

营销人员希望通过以下方式定位用户区段(内置于Adobe Experience Platform) [!DNL Moengage] 营销活动。 此外，他们希望根据Adobe Experience Platform用户档案中的属性个性化营销活动内容。 利用此集成，一旦在Adobe Experience Platform中更新区段和用户档案，用户和属性就会在MoEngage中更新。

## 先决条件 {#prerequisites}

在将Adobe Experience Platform数据发送到之前 [!DNL Moengage]，请注意以下先决条件：

* 要将MoEngage目标与Adobe Experience Platform结合使用，用户必须首先有权访问其 [!DNL Moengage] 帐户。 请访问以下页面以注册或登录您的MoEngage帐户：https://app.moengage.com


## 支持的身份 {#supported-identities}

[!DNL Moengage] 支持激活下表中描述的标识。

| 目标身份 | 描述 | 注意事项 |
|---|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| user_id | 唯一标识符，用于唯一标识 [!DNL Moengage] 系统。 | 此标识符支持字符串类型。 需要user_id或anonymous_id之一 |
| anonymous_id | 未知用户配置文件的另一个标识符 — 表示系统中不存在配置文件。 | 此标识符支持字符串类型。 需要user_id或anonymous_id之一 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | 您正在导出具有标识符(user_id、anonymous_id)以及您导出到的自定义属性的区段（受众）的所有成员 [!DNL Moengage]. |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

![Moengage目标身份验证](../../assets/catalog/mobile-engagement/moengage/authentication.png)

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![Moengage目标身份验证](../../assets/catalog/mobile-engagement/moengage/settings.png)
* **[!UICONTROL 用户名]**：设置页面的数据应用程序ID [!DNL Moengage] 仪表板。
* **[!UICONTROL 密码]**：设置页面中的数据应用程序密钥 [!DNL Moengage] 仪表板。

![Moengage目标身份验证](../../assets/catalog/mobile-engagement/moengage/destination_details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 区域]**：您的应用程序 *数据中心*.

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

请参阅 [将受众数据激活到流式区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射属性和身份 {#map}

要正确发送受众数据，请执行以下操作： [!DNL Adobe Experience Platform] 到 [!DNL Moengage] 目标，您需要执行字段映射步骤。

映射包括创建以下对象之间的链接： [!DNL Experience Data Model] (XDM)架构字段 [!DNL Platform] 目标中的帐户及其对应的对等项。

要将XDM字段正确映射到 [!DNL Moengage] 目标字段，请执行以下步骤：

在 [!UICONTROL 映射] 步骤，选择 **[!UICONTROL 复选框]**.

![Moengage目标添加映射](../../assets/catalog/mobile-engagement/moengage/segments.png)

在 [!UICONTROL 映射] 步骤，选择 **[!UICONTROL 添加新映射]**.

![Moengage目标添加映射](../../assets/catalog/mobile-engagement/moengage/mapping.png)

在 [!UICONTROL 源字段] 部分，选择空字段旁边的箭头按钮。

![Moengage目标源映射](../../assets/catalog/mobile-engagement/moengage/mapping-source.png)

在 [!UICONTROL 选择源字段] 窗口中，您可以选择以下两种类别的XDM字段：
* [!UICONTROL 选择属性]：使用此选项将XDM架构中的特定字段映射到 [!DNL Moengage] 属性。

![移动目标映射源属性](../../assets/catalog/mobile-engagement/moengage/mapping-attributes.png)

选择源字段，然后选择 **[!UICONTROL 选择]**.

在 [!UICONTROL 目标字段] 部分，选择字段右侧的映射图标。

![Moengage目标映射](../../assets/catalog/mobile-engagement/moengage/mapping-target.png)

在 [!UICONTROL 选择目标字段] 窗口中，您可以选择以下两种目标字段类别：
* [!UICONTROL 选择身份命名空间]：使用此选项来映射 [!DNL Platform] 身份命名空间到 [!DNL Moengage] 身份命名空间。
* [!UICONTROL 选择自定义属性]：使用此选项将XDM属性映射到自定义 [!DNL Moengage] 您在中定义的属性 [!DNL Moengage] 帐户。 <br> 您还可以使用此选项将现有XDM属性重命名为 [!DNL Moengage]. 例如，映射 `lastName` 自定义的XDM属性 `Last_Name` 中的属性 [!DNL Moengage]，将创建 `Last_Name` 中的属性 [!DNL Moengage]，如果它尚不存在，则映射 `lastName` XDM属性。

![移动目标映射字段](../../assets/catalog/mobile-engagement/moengage/mapping-target-fields.png)

选择目标字段，然后选择 **[!UICONTROL 选择]**.

您现在应在列表中看到字段映射。

![Moengage目标映射完成](../../assets/catalog/mobile-engagement/moengage/mapping-complete.png)

要添加更多映射，请重复上述步骤。

## 导出的数据/验证数据导出 {#exported-data}

验证数据是否已成功导出到 [!DNL Moengage] 目标，转到您的网站上的用户配置文件 [!DNL Moengage] 帐户。 您将看到一个名为AEP区段的用户属性。

![Moengage目标映射完成](../../assets/catalog/mobile-engagement/moengage/validation.png)

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](/help/data-governance/home.md).
