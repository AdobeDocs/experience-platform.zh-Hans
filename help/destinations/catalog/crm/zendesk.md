---
title: Zendesk连接
description: Zendesk目标允许您导出帐户数据，并在Zendesk中激活该数据，以满足您的业务需求。
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 1%

---

# [!DNL Zendesk] 连接

[[!DNL Zendesk]](https://www.zendesk.com) 是一个客户服务解决方案和销售工具。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [[!DNL Zendesk] 联系人API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/)，以在区段中创建身份并将其更新为中的联系人 [!DNL Zendesk].

[!DNL Zendesk] 使用持有者令牌作为身份验证机制与 [!DNL Zendesk] 联系人API。 向您的验证的说明 [!DNL Zendesk] 实例位于 [向目标进行身份验证](#authenticate) 部分。

## 用例 {#use-cases}

作为营销人员，您可以根据用户的Adobe Experience Platform配置文件中的属性，为其提供个性化体验。 您可以从离线数据构建区段并将这些区段发送到 [!DNL Zendesk]，以便在Adobe Experience Platform中更新区段和配置文件后立即显示在用户的馈送中。

## 先决条件 {#prerequisites}

### Experience Platform先决条件 {#prerequisites-in-experience-platform}

将数据激活到之前 [!DNL Zendesk] 目标，您必须拥有 [架构](/help/xdm/schema/composition.md)， a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)、和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 创建于 [!DNL Experience Platform].

请参阅Experience Platform文档，了解 [“区段成员资格详细信息”架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关区段状态的指南。

### [!DNL Zendesk] 先决条件 {#prerequisites-destination}

为了将数据从Platform导出到 [!DNL Zendesk] 您需要拥有 [!DNL Zendesk] 帐户。

#### 收集 [!DNL Zendesk] 凭据 {#gather-credentials}

在对进行身份验证之前，请记下以下各项 [!DNL Zendesk] 目标：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `Bearer token` | 您在中生成的访问令牌 [!DNL Zendesk] 帐户。 <br> 请按照文档中的说明，访问 [生成 [!DNL Zendesk] 访问令牌](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) 如果你没有。 | `a0b1c2d3e4...v20w21x22y23z` |

## 护栏 {#guardrails}

此 [定价和费率限制](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) 页面详细信息 [!DNL Zendesk] 与您的帐户关联的API限制。 您需要确保您的数据和有效负载处于这些限制范围内。

## 支持的身份 {#supported-identities}

[!DNL Zendesk] 支持更新下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 示例 | 描述 | 必需 |
|---|---|---|---|
| `email` | `test@test.com` | 联系人的电子邮件地址。 | 是 |

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在导出区段的所有成员以及所需的架构字段 *（例如：电子邮件地址、电话号码、姓氏）*，根据您的字段映射。</li><li> 中的每个区段状态 [!DNL Zendesk] 将根据 **[!UICONTROL 映射Id]** 在以下时段提供的值： [区段调度](#schedule-segment-export-example) 步骤。</li></ul> |
| 导出频率 | **[!UICONTROL 流]** | <ul><li>流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

范围 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 搜索 [!DNL Zendesk]. 或者，您也可以在 **[!UICONTROL CRM]** 类别。

### 向目标进行身份验证 {#authenticate}

填写下面的必填字段。 请参阅 [收集 [!DNL Zendesk] 凭据](#gather-credentials) 部分获取任何指导。
* **[!UICONTROL 持有者令牌]**：您在中生成的访问令牌 [!DNL Zendesk] 帐户。

要对目标进行身份验证，请选择 **[!UICONTROL 连接到目标]**.
![显示如何进行身份验证的Platform UI屏幕快照。](../../assets/catalog/crm/zendesk/authenticate-destination.png)

如果提供的详细信息有效，则UI将显示 **[!UICONTROL 已连接]** 带有绿色复选标记的状态。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![显示目标详细信息的Platform UI屏幕快照。](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
>
>要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将配置文件和区段激活到流式区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要正确地将受众数据从Adobe Experience Platform发送到 [!DNL Zendesk] 目标，您需要完成字段映射步骤。 映射包括在Platform帐户中的Experience Data Model (XDM)架构字段与其与目标目标中的相应等效字段之间创建链接。

中指定的属性 **[!UICONTROL 目标字段]** 应按照“属性映射”表中的说明进行命名，因为这些属性将构成请求正文。

中指定的属性 **[!UICONTROL 源字段]** 请勿遵守任何此类限制。 您可以根据需要进行映射，但是，如果数据格式在推送到时不正确 [!DNL Zendesk] 这会导致错误。

要将XDM字段正确映射到 [!DNL Zendesk] 目标字段，请执行以下步骤：

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新映射行。
1. 在 **[!UICONTROL 选择源字段]** 窗口中，选择 **[!UICONTROL 选择属性]** 类别并选择XDM属性或选择 **[!UICONTROL 选择身份命名空间]** 并选择身份。
1. 在 **[!UICONTROL 选择目标字段]** 窗口中，选择 **[!UICONTROL 选择身份命名空间]** 并选择身份或选择 **[!UICONTROL 选择自定义属性]** 类别并根据需要选择属性。
   * 重复这些步骤以添加以下XDM配置文件架构与 [!DNL Zendesk] 实例： |源字段|目标字段|必填| |—|—|—| |`xdm: person.name.lastName`|`Attribute: last_name` <br>或 `Attribute: name`|是 | |`IdentityMap: Email`|`Identity: email`|是 |

   * 下面显示了使用这些映射的示例：
      ![具有属性映射的平台UI屏幕快照示例。](../../assets/catalog/crm/zendesk/mappings.png)

      >[!IMPORTANT]
      >
      >目标字段映射是必需的，对于 [!DNL Zendesk] 去工作。
      >
      >的映射 *姓氏* 或 *名称* 必需，否则 [!DNL Zendesk] API未响应任何错误，传递的任何属性值都将被忽略。

完成提供目标连接的映射后，选择 **[!UICONTROL 下一个]**.

### 计划区段导出和示例 {#schedule-segment-export-example}

在 [[!UICONTROL 计划区段导出]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 在激活工作流的步骤中，您必须手动将Platform区段映射到中的自定义字段属性 [!DNL Zendesk].

为此，请选择每个区段，然后从中输入相应的自定义字段属性 [!DNL Zendesk] 在 **[!UICONTROL 映射Id]** 字段。

下面显示了一个示例：
![显示计划区段导出的平台UI屏幕截图示例。](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 选择 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 并导航到目标列表。
1. 接下来，选择目标并切换到 **[!UICONTROL 激活数据]** 选项卡，然后选择区段名称。
   ![显示目标激活数据的平台UI屏幕截图示例。](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. 监控区段摘要，并确保配置文件计数对应于区段内的计数。
   ![显示区段的平台UI屏幕快照示例。](../../assets/catalog/crm/zendesk/segment.png)

1. 登录到 [!DNL Zendesk] 网站，然后导航到 **[!UICONTROL 联系人]** 页面以检查是否已添加区段中的配置文件。 可将此列表配置为显示使用区段创建的其他字段的列 **[!UICONTROL 映射Id]** 和区段状态。
   ![Zendesk UI屏幕截图显示了“联系人”页面，其中包含使用区段名称创建的其他字段。](../../assets/catalog/crm/zendesk/contacts.png)

1. 或者，您可以向下钻取到个人 **[!UICONTROL 人员]** 页面并检查 **[!UICONTROL 其他字段]** 部分显示区段名称和区段状态。
   ![显示“人员”页面的Zendesk UI屏幕快照，其“其他字段”部分显示区段名称和区段状态。](../../assets/catalog/crm/zendesk/contact.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据治理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

其他有用信息来自 [!DNL Zendesk] 文档如下所示：
* [进行首次调用](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [自定义字段](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)