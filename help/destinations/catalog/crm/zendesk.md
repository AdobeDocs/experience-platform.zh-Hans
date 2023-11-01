---
title: Zendesk 连接
description: Zendesk目标允许您导出帐户数据，并在Zendesk中激活该数据，以满足您的业务需求。
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: e7fcbbf4-5d6c-4abb-96cb-ea5b67a88711
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 1%

---

# [!DNL Zendesk] 连接

[[!DNL Zendesk]](https://www.zendesk.com) 是一个客户服务解决方案和销售工具。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [[!DNL Zendesk] 联系人API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/)，至 **创建和更新身份** 在受众中作为联系人 [!DNL Zendesk].

[!DNL Zendesk] 使用持有者令牌作为身份验证机制与 [!DNL Zendesk] 联系人API。 向您的验证的说明 [!DNL Zendesk] 实例位于 [向目标进行身份验证](#authenticate) 部分。

## 用例 {#use-cases}

多渠道B2C平台的客户服务部希望为其客户提供无缝的个性化体验。 部门可以根据自身的离线数据构建受众，以创建新的用户配置文件或更新来自不同交互（例如购买、退货等）的现有配置文件信息 并将这些受众从Adobe Experience Platform发送到 [!DNL Zendesk]. 将更新后的信息放在 [!DNL Zendesk] 确保客户服务代理能够立即获得客户的最新信息，从而加快响应和解决问题。

## 先决条件 {#prerequisites}

### Experience Platform先决条件 {#prerequisites-in-experience-platform}

将数据激活到之前 [!DNL Zendesk] 目标，您必须拥有 [架构](/help/xdm/schema/composition.md)， a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)、和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) 创建于 [!DNL Experience Platform].

请参阅Experience Platform文档 [受众成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关受众状态的指南。

### [!DNL Zendesk] 先决条件 {#prerequisites-destination}

为了将数据从Platform导出到 [!DNL Zendesk] 您需要拥有 [!DNL Zendesk] 帐户。

#### 收集 [!DNL Zendesk] 凭据 {#gather-credentials}

在对进行身份验证之前，请记下以下各项 [!DNL Zendesk] 目标：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `Bearer token` | 您在中生成的访问令牌 [!DNL Zendesk] 帐户。 <br> 按照文档操作 [生成 [!DNL Zendesk] 访问令牌](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) 如果你没有。 | `a0b1c2d3e4...v20w21x22y23z` |

## 护栏 {#guardrails}

此 [定价和利率限制](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) 页面详细信息 [!DNL Zendesk] 与您的帐户关联的API限制。 您需要确保数据和有效负载均在这些限制之内。

## 支持的身份 {#supported-identities}

[!DNL Zendesk] 支持更新下表中描述的标识。 了解有关 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 示例 | 描述 | 必需 |
|---|---|---|---|
| `email` | `test@test.com` | 联系人的电子邮件地址。 | 是 |

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在导出区段的所有成员以及所需的架构字段 *（例如：电子邮件地址、电话号码、姓氏）*，根据您的字段映射。</li><li> 中的每个区段状态 [!DNL Zendesk] 将根据 **[!UICONTROL 映射Id]** 值在 [受众调度](#schedule-segment-export-example) 步骤。</li></ul> |
| 导出频率 | **[!UICONTROL 流]** | <ul><li>流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

范围 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 搜索 [!DNL Zendesk]. 或者，您可以将其定位到 **[!UICONTROL CRM]** 类别。

### 向目标进行身份验证 {#authenticate}

填写下面的必填字段。 请参阅 [收集 [!DNL Zendesk] 凭据](#gather-credentials) 部分获取任何指导。
* **[!UICONTROL 持有者令牌]**：您在中生成的访问令牌 [!DNL Zendesk] 帐户。

要验证目标，请选择 **[!UICONTROL 连接到目标]**.
![显示如何进行身份验证的平台UI屏幕截图。](../../assets/catalog/crm/zendesk/authenticate-destination.png)

如果提供的详细信息有效，UI将显示 **[!UICONTROL 已连接]** 带有绿色复选标记的状态。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![显示目标详细信息的平台UI屏幕截图。](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将受众激活到此目标 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将用户档案和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要正确地将受众数据从Adobe Experience Platform发送到 [!DNL Zendesk] 目标，您需要执行字段映射步骤。 映射包括在您的Platform帐户中的Experience Data Model (XDM)架构字段与其在目标目标中的相应等效字段之间创建链接。

中指定的属性 **[!UICONTROL 目标字段]** 应完全按照属性映射表中所述命名，因为这些属性将构成请求正文。

中指定的属性 **[!UICONTROL 源字段]** 请勿遵循任何此类限制。 您可以根据需要进行映射，但是，如果数据格式在推送到时不正确 [!DNL Zendesk] 这将导致出现错误。

要将XDM字段正确映射到 [!DNL Zendesk] 目标字段，请执行以下步骤：

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新映射行。
1. 在 **[!UICONTROL 选择源字段]** 窗口中，选择 **[!UICONTROL 选择属性]** 类别并选择XDM属性或选择 **[!UICONTROL 选择身份命名空间]** 并选择身份。
1. 在 **[!UICONTROL 选择目标字段]** 窗口中，选择 **[!UICONTROL 选择身份命名空间]** 类别并选择目标身份，或选择 **[!UICONTROL 选择属性]** 类别并选择支持的架构属性之一。
   * 重复这些步骤以添加以下强制映射，您还可以添加要在XDM配置文件架构与 [!DNL Zendesk] 实例： |源字段|目标字段|必填| |—|—|—| |`xdm: person.name.lastName`|`xdm: last_name`|是 | |`IdentityMap: Email`|`Identity: email`|是 | |`xdm: person.name.firstName`|`xdm: first_name`| |

   * 下面显示了使用这些映射的示例：
     ![具有属性映射的平台UI屏幕快照示例。](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>此 `Attribute: last_name` 和 `Identity: email` 目标映射对于此目标是必需的。 如果缺少这些映射，则会忽略任何其他映射并且不会发送至 [!DNL Zendesk].

完成提供目标连接的映射后，选择 **[!UICONTROL 下一个]**.

### 计划受众导出和示例 {#schedule-segment-export-example}

在 [[!UICONTROL 计划受众导出]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 在激活工作流的步骤中，您必须手动将Platform受众映射到中的自定义字段属性 [!DNL Zendesk].

要实现此目的，请选择每个区段，然后从中输入相应的自定义字段属性 [!DNL Zendesk] 在 **[!UICONTROL 映射Id]** 字段。

下面显示了一个示例：
![显示计划受众导出的平台UI屏幕截图示例。](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 选择 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 并导航到目标列表。
1. 接下来，选择目标并切换到 **[!UICONTROL 激活数据]** 选项卡，然后选择受众名称。
   ![显示目标激活数据的平台UI屏幕截图示例。](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. 监控受众摘要，并确保用户档案计数对应于区段中的计数。
   ![显示区段的平台UI屏幕截图示例。](../../assets/catalog/crm/zendesk/segment.png)

1. 登录到 [!DNL Zendesk] 网站，然后导航到 **[!UICONTROL 联系人]** 页面检查是否已添加受众的用户档案。 此列表可以配置为显示使用受众创建的其他字段的列**[!UICONTROL 映射Id]**和受众状态。
   ![Zendesk UI屏幕截图，其中显示了“联系人”页面以及使用受众名称创建的其他字段。](../../assets/catalog/crm/zendesk/contacts.png)

1. 或者，您可以深入到个人 **[!UICONTROL 人员]** 页面并检查 **[!UICONTROL 其他字段]** 部分显示受众名称和受众状态。
   ![Zendesk UI屏幕截图显示“人员”页面，其他字段部分显示受众名称和受众状态。](../../assets/catalog/crm/zendesk/contact.png)

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

其他有用信息来自 [!DNL Zendesk] 文档如下所示：
* [首次致电](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [自定义字段](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Changelog

此部分捕获此目标连接器的功能和重要文档更新。

+++ 查看更改日志

| 发行月份 | 更新类型 | 描述 |
|---|---|---|
| 2023 年 4 月 | 文档更新 | <ul><li>我们更新了 [用例](#use-cases) 部分中提供了客户何时将从使用此目标中受益的更清晰示例。</li> <li>我们更新了 [映射](#mapping-considerations-example) 部分，以反映所需的正确映射。 此 `Attribute: last_name` 和 `Identity: email` 目标映射对于此目标是必需的。 如果缺少这些映射，则会忽略任何其他映射并且不会发送至 [!DNL Zendesk].</li> <li>我们更新了 [映射](#mapping-considerations-example) 部分，其中包含强制映射和可选映射的明确示例。</li></ul> |
| 2023 年 3 月 | 初始版本 | 初始目标版本和文档发布。 |

{style="table-layout:auto"}

+++
