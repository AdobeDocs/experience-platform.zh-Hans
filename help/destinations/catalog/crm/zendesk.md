---
title: Zendesk连接
description: Zendesk目标允许您导出帐户数据，并在Zendesk中激活它以满足您的业务需求。
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 55f1eafa68124b044d20f8f909f6238766076a7a
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 1%

---

# [!DNL Zendesk] 连接

[[!DNL Zendesk]](https://www.zendesk.com) 是客户服务解决方案和销售工具。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [[!DNL Zendesk] 联系人API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/)，更改为 **创建和更新身份** 作为 [!DNL Zendesk].

[!DNL Zendesk] 使用承载令牌作为与通信的验证机制 [!DNL Zendesk] 联系人API。 验证的说明 [!DNL Zendesk] 实例位于下面的 [对目标进行身份验证](#authenticate) 中。

## 用例 {#use-cases}

多渠道B2C平台的客户服务部门希望确保为客户提供无缝的个性化体验。 该部门可以根据自己的离线数据构建区段，以创建新的用户配置文件，或通过不同交互（例如购买、退货等）更新现有的配置文件信息 将这些区段从Adobe Experience Platform发送到 [!DNL Zendesk]. 将更新的信息置于 [!DNL Zendesk] 确保客户服务代理可立即获得客户的最新信息，从而加快响应和解决问题。

## 先决条件 {#prerequisites}

### Experience Platform先决条件 {#prerequisites-in-experience-platform}

在将数据激活到 [!DNL Zendesk] 目标，您必须具有 [模式](/help/xdm/schema/composition.md), a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 创建于 [!DNL Experience Platform].

请参阅Experience Platform文档，以了解 [区段成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关区段状态的指导，请执行以下操作：

### [!DNL Zendesk] 先决条件 {#prerequisites-destination}

要将数据从Platform导出到 [!DNL Zendesk] 帐户 [!DNL Zendesk] 帐户。

#### 收集 [!DNL Zendesk] 凭据 {#gather-credentials}

在验证到 [!DNL Zendesk] 目标：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `Bearer token` | 您在 [!DNL Zendesk] 帐户。 <br> 请按照以下文档操作 [生成 [!DNL Zendesk] 访问令牌](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) 如果你没有。 | `a0b1c2d3e4...v20w21x22y23z` |

## 护栏 {#guardrails}

的 [定价和费率限制](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) 页面详细信息 [!DNL Zendesk] 与您的帐户关联的API限制。 您需要确保数据和有效负载在这些限制内。

## 支持的身份 {#supported-identities}

[!DNL Zendesk] 支持更新下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 示例 | 描述 | 必需 |
|---|---|---|---|
| `email` | `test@test.com` | 联系人的电子邮件地址。 | 是 |

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | <ul><li>您正在导出区段的所有成员，以及所需的架构字段 *(例如：电子邮件地址、电话号码、姓氏)*，则会根据字段映射。</li><li> 每个区段状态位于 [!DNL Zendesk] 会根据 **[!UICONTROL 映射ID]** 值 [区段计划](#schedule-segment-export-example) 中。</li></ul> |
| 导出频度 | **[!UICONTROL 流]** | <ul><li>流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

在 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 搜索 [!DNL Zendesk]. 或者，您也可以在 **[!UICONTROL CRM]** 类别。

### 对目标进行身份验证 {#authenticate}

填写以下必填字段。 请参阅 [收集 [!DNL Zendesk] 凭据](#gather-credentials) 部分。
* **[!UICONTROL 载体令牌]**:您在 [!DNL Zendesk] 帐户。

要对目标进行身份验证，请选择 **[!UICONTROL 连接到目标]**.
![Platform UI屏幕截图，其中显示了如何进行身份验证。](../../assets/catalog/crm/zendesk/authenticate-destination.png)

如果提供的详细信息有效，UI会显示 **[!UICONTROL 已连接]** 状态为绿色复选标记。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![Platform UI屏幕截图，显示目标详细信息。](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
>
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要将受众数据从Adobe Experience Platform正确发送到 [!DNL Zendesk] 目标，您需要完成字段映射步骤。 映射包括在Platform帐户中的体验数据模型(XDM)架构字段与目标目标中相应的对等字段之间创建一个链接。

在 **[!UICONTROL 目标字段]** 应完全按照属性映射表中所述的名称命名，因为这些属性将构成请求正文。

在 **[!UICONTROL 源字段]** 不要遵守任何此类限制。 您可以根据需要映射数据格式，但如果数据格式在推送到 [!DNL Zendesk] 这会导致错误。

要将XDM字段正确映射到 [!DNL Zendesk] 目标字段，请执行以下步骤：

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新的映射行。
1. 在 **[!UICONTROL 选择源字段]** 窗口，选择 **[!UICONTROL 选择属性]** 类别，然后选择XDM属性或 **[!UICONTROL 选择身份命名空间]** 并选择一个身份。
1. 在 **[!UICONTROL 选择目标字段]** 窗口，选择 **[!UICONTROL 选择身份命名空间]** 类别，然后选择目标标识，或选择 **[!UICONTROL 选择属性]** 类别中，然后选择一个受支持的架构属性。
   * 重复这些步骤以添加以下必需映射，您还可以添加要在XDM配置文件架构和 [!DNL Zendesk] 实例： |源字段|目标字段|必填| |—|—|—| |`xdm: person.name.lastName`|`xdm: last_name`|是 | |`IdentityMap: Email`|`Identity: email`|是 | |`xdm: person.name.firstName`|`xdm: first_name`| |

   * 使用这些映射的示例如下所示：
      ![Platform UI屏幕截图示例，其中包含属性映射。](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>的 `Attribute: last_name` 和 `Identity: email` 此目标必须进行目标映射。 如果这些映射缺失，则任何其他映射都将被忽略，且不会发送到 [!DNL Zendesk].

完成为目标连接提供映射后，请选择 **[!UICONTROL 下一个]**.

### 计划区段导出和示例 {#schedule-segment-export-example}

在 [[!UICONTROL 计划区段导出]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 在激活工作流的步骤中，您必须手动将Platform区段映射到 [!DNL Zendesk].

为此，请选择每个区段，然后输入 [!DNL Zendesk] 在 **[!UICONTROL 映射ID]** 字段。

示例如下所示：
![Platform UI屏幕截图示例显示了计划区段导出。](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## 验证数据导出 {#exported-data}

要验证您是否已正确设置目标，请执行以下步骤：

1. 选择 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 并导航到目标列表。
1. 接下来，选择目标并切换到 **[!UICONTROL 激活数据]** ，然后选择区段名称。
   ![Platform UI屏幕截图示例，其中显示了目标激活数据。](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. 监控区段摘要，并确保用户档案的计数与区段内的计数相对应。
   ![平台UI屏幕截图示例，其中显示了区段。](../../assets/catalog/crm/zendesk/segment.png)

1. 登录到 [!DNL Zendesk] 网站，然后导航到 **[!UICONTROL 联系人]** 页面来检查是否已添加区段中的用户档案。 此列表可配置为显示使用该区段创建的其他字段的列 **[!UICONTROL 映射ID]** 和区段状态。
   ![Zendesk UI屏幕截图显示“联系人”页面，其中包含使用区段名称创建的其他字段。](../../assets/catalog/crm/zendesk/contacts.png)

1. 或者，您也可以深入到单个 **[!UICONTROL 人员]** 页面并检查 **[!UICONTROL 其他字段]** 区段名称和区段状态。
   ![Zendesk UI屏幕截图显示了“人员”页面，其中包含显示区段名称和区段状态的其他字段部分。](../../assets/catalog/crm/zendesk/contact.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

来自 [!DNL Zendesk] 文档如下所示：
* [首次致电](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [自定义字段](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Changelog

本节将捕获对此目标连接器所做的功能和重要文档更新。

+++ 查看changelog

| 发布月份 | 更新类型 | 描述 |
|---|---|---|
| 2023 年 4 月 | 文档更新 | <ul><li>我们更新了 [用例](#use-cases) 部分，以更清晰的示例说明客户何时会从使用此目标中受益。</li> <li>我们更新了 [映射](#mapping-considerations-example) 部分来反映正确的所需映射。 的 `Attribute: last_name` 和 `Identity: email` 此目标必须进行目标映射。 如果这些映射缺失，则任何其他映射都将被忽略，且不会发送到 [!DNL Zendesk].</li> <li>我们更新了 [映射](#mapping-considerations-example) 部分，其中明确显示了必选和可选映射。</li></ul> |
| 2023 年 3 月 | 初始版本 | 初始目标版本和文档发布。 |

{style="table-layout:auto"}

+++