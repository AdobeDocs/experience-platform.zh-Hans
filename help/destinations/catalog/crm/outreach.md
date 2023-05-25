---
keywords: CRM；CRM；CRM目标；外联；外联CRM目标
title: 外联联系
description: 外联目标允许您导出帐户数据，并在外联中激活它以满足您的业务需求。
exl-id: 7433933d-7a4e-441d-8629-a09cb77d5220
source-git-commit: 4ef83c152c4649721c6a424f3ba47b7c6bbfef3f
workflow-type: tm+mt
source-wordcount: '1711'
ht-degree: 1%

---

# [!DNL Outreach] 连接

## 概述 {#overview}

[[!DNL Outreach]](https://www.outreach.io/) 是一个销售执行平台，拥有世界上最大的B2B买方和卖方交互数据，并在专有人工智能技术方面投入巨资，将销售数据转化为情报。 [!DNL Outreach] 帮助企业自动执行销售接洽并根据收入情报采取行动，以提高其效率、可预测性和增长。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [外展更新资源API](https://api.outreach.io/api/v2/docs#update-an-existing-resource)，允许您更新与中的潜在客户对应的区段中的标识 [!DNL Outreach].

[!DNL Outreach] 使用具有授权授予的OAuth 2作为身份验证机制，与 [!DNL Outreach] [!DNL Update Resource API]. 向您的验证的说明 [!DNL Outreach] 下面是实例，位于 [向目标进行身份验证](#authenticate) 部分。

## 用例 {#use-cases}

作为营销人员，您可以根据潜在客户的Adobe Experience Platform配置文件中的属性，为其提供个性化体验。 您可以从离线数据构建区段并将这些区段发送到 [!DNL Outreach]，以便在Adobe Experience Platform中更新区段和用户档案后立即显示在潜在客户的信息源中。

## 先决条件 {#prerequisites}

### Experience Platform先决条件 {#prerequisites-in-experience-platform}

将数据激活到之前 [!DNL Outreach] 目标，您必须拥有 [架构](/help/xdm/schema/composition.md)， a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)、和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 创建于 [!DNL Experience Platform].

请参阅Adobe的文档，了解 [“区段成员资格详细信息”架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关区段状态的指南。

### 外联先决条件 {#prerequisites-destination}

请注意中的以下先决条件 [!DNL Outreach]，以便将数据从Platform导出到 [!DNL Outreach] 帐户：

#### 您需要有一个外联帐户 {#prerequisites-account}

转到 [!DNL Outreach] [登录](https://accounts.outreach.io/users/sign_in) 页面注册并创建帐户（如果尚未注册）。 另请参阅 [!DNL Outreach] 支持 [页面](https://support.outreach.io/hc/en-us/articles/207238607-Claim-Your-Outreach-Account) 了解更多详细信息。

在对进行身份验证之前，请记下以下各项 [!DNL Outreach] CRM目标：

| 凭据 | 描述 |
|---|---|
| 电子邮件 | 您的 [!DNL Outreach] 帐户电子邮件 |
| 密码 | 您的 [!DNL Outreach] 帐户密码 |

#### 设置自定义字段标签 {#prerequisites-custom-fields}

[!DNL Outreach] 支持自定义字段 [潜在客户](https://support.outreach.io/hc/en-us/articles/360001557554-Outreach-Prospect-Profile-Overview). 请参阅 [如何在外联活动中添加自定义字段](https://support.outreach.io/hc/en-us/articles/219124908-How-To-Add-a-Custom-Field-in-Outreach) 以获取其他指导。 为了便于识别，建议手动将标签更新为其相应的区段名称，而不是保留默认值。 例如，如下所示：

[!DNL Outreach] 潜在客户的“设置”页面显示自定义字段。
![显示设置页面中自定义字段的外联UI屏幕截图。](../../assets/catalog/crm/outreach/outreach-custom-fields.png)

[!DNL Outreach] 潜在客户显示自定义字段的设置页面 *用户友好* 与区段名称匹配的标签。 您可以在目标客户页面上根据这些标签查看区段状态。
![外联UI屏幕快照，显示设置页面上具有关联标签的自定义字段。](../../assets/catalog/crm/outreach/outreach-custom-field-labels.png)

>[!NOTE]
>
> 标签名称仅便于识别。 更新潜在客户时不会使用它们。

## 护栏

此 [!DNL Outreach] API的速率限制为每用户每小时10,000个请求。 如果您达到此限制，您将收到 `429` 响应以下消息： `You have exceeded your permitted rate limit of 10,000; please try again at 2017-01-01T00:00:00.`.

如果收到此消息，则必须更新区段导出计划以符合速率阈值。

请参阅 [[!DNL Outreach] 文档](https://api.outreach.io/api/v2/docs#rate-limiting) 以了解更多详细信息。

## 支持的身份 {#supported-identities}

[!DNL Outreach] 支持更新下表中描述的标识。 详细了解 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| `OutreachId` | <ul><li>[!DNL Outreach] 标识符。 这是对应于目标客户配置文件的数值。</li><li>ID必须与 [!DNL Outreach] 要更新的目标客户的URL。</li><li>请参阅 [[!DNL Outreach] 文档](https://api.outreach.io/api/v2/docs#update-an-existing-resource) 了解更多详细信息。</li></ul> | 必需 |

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li> 您正在导出区段的所有成员以及所需的架构字段 *（例如：电子邮件地址、电话号码、姓氏）*，根据您的字段映射。</li><li> 中的每个区段状态 [!DNL Outreach] 将根据 [!UICONTROL 映射Id] 在以下时段提供的值： [区段调度](#schedule-segment-export-example) 步骤。</li></ul> |
| 导出频率 | **[!UICONTROL 流]** | <ul><li> 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流式目标](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
> 要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

范围 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 搜索 [!DNL Outreach]. 或者，您可以在CRM类别下找到它。

### 向目标进行身份验证 {#authenticate}

要对目标进行身份验证，请选择 **[!UICONTROL 连接到目标]**.

![平台UI屏幕快照，显示如何对外联进行身份验证。](../../assets/catalog/crm/outreach/authenticate-destination.png)

您将会看到 [!DNL Outreach] 登录页面。 提供您的电子邮件。

![外联UI屏幕快照，显示输入电子邮件以验证外联的字段。](../../assets/catalog/crm/outreach/authenticate-destination-login-email.png)

接下来，提供您的密码。

![外联UI屏幕快照，显示用于输入密码步骤以验证外联的字段。](../../assets/catalog/crm/outreach/authenticate-destination-login-password.png)

* **[!UICONTROL 用户名]**：您的 [!DNL Outreach] 帐户电子邮件。
* **[!UICONTROL 密码]**：您的 [!DNL Outreach] 帐户密码。

如果提供的详细信息有效，则UI将显示 **已连接** 带有绿色复选标记的状态。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![平台UI屏幕快照，显示如何填写外联目标的详细信息。](../../assets/catalog/crm/outreach/destination-details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关流向目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
> 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

读取 [将配置文件和区段激活到流式区段导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要正确地将受众数据从Adobe Experience Platform发送到 [!DNL Outreach] 目标，您需要完成字段映射步骤。 映射包括在Platform帐户中的Experience Data Model (XDM)架构字段与其与目标目标中的相应等效字段之间创建链接。 要将XDM字段正确映射到 [!DNL Outreach] 目标字段，请执行以下步骤：

1. 在 [!UICONTROL 映射] 步骤，单击 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新映射行。
   ![显示如何添加新映射的平台UI屏幕快照](../../assets/catalog/crm/outreach/add-new-mapping.png)

1. 在 [!UICONTROL 选择源字段] 窗口中，选择 **[!UICONTROL 选择身份命名空间]** 类别并添加所需的映射。
   ![显示源映射的平台UI屏幕快照](../../assets/catalog/crm/outreach/source-mapping.png)

1. 在 [!UICONTROL 选择目标字段] 窗口中，选择要将源字段映射到的目标字段类型。
   * **[!UICONTROL 选择身份命名空间]**：选择此选项可从列表中将源字段映射到身份命名空间。
      ![平台UI屏幕截图，其中显示了使用ExtendeoId的Target映射。](../../assets/catalog/crm/outreach/target-mapping.png)

   * 在XDM配置文件架构和您的配置文件架构之间添加以下映射 [!DNL Outreach] 实例： |XDM配置文件架构|[!DNL Outreach] 实例|必需| |—|—|—| |`Oid`|`OutreachId`|是 |

   * **[!UICONTROL 选择自定义属性]**：选择此选项可将源字段映射到您在 [!UICONTROL 属性名称] 字段。 请参阅 [[!DNL Outreach] 潜在客户文档](https://api.outreach.io/api/v2/docs#prospect) 以获取支持的属性的完整列表。
      ![显示使用LastName的Target映射的平台UI屏幕截图。](../../assets/catalog/crm/outreach/target-mapping-lastname.png)

   * 例如，根据要更新的值，添加以下XDM配置文件架构与您的配置文件架构之间的映射 [!DNL Outreach] 实例： |XDM配置文件架构|[!DNL Outreach] 实例| |—|—| |`person.name.firstName`|`firstName`| |`person.name.lastName`|`lastName`|

   * 下面显示了使用这些映射的示例：
      ![显示Target映射的平台UI屏幕快照示例。](../../assets/catalog/crm/outreach/mappings.png)

### 计划区段导出和示例 {#schedule-segment-export-example}

* 执行 [计划区段导出](../../ui/activate-segment-streaming-destinations.md) 必须手动将Platform区段映射到中的自定义字段属性的步骤 [!DNL Outreach].

* 要实现此目的，请选择每个区段，然后输入与 *自定义字段 `N` 标签* 字段自 [!DNL Outreach] 在 **[!UICONTROL 映射Id]** 字段。

   >[!IMPORTANT]
   >
   > * 数值 *(`N`)* 在中使用 [!UICONTROL 映射Id] 应该匹配后缀为中的数字值的自定义属性键 [!DNL Outreach]. 示例： *自定义字段 `N` 标签*.
   > * 您只需指定数字值，而无需指定整个自定义字段标签。
   > * [!DNL Outreach] 支持最多150个自定义标签字段。
   > * 请参阅 [[!DNL Outreach] 潜在客户文档](https://api.outreach.io/api/v2/docs#prospect) 了解详细信息。


   * 例如：

      | [!DNL Outreach] 字段 | 平台映射ID |
      |---|---|
      | 自定义字段 `4` 标签 | `4` |

      ![Platform UI屏幕截图显示了计划区段导出期间的示例映射ID。](../../assets/catalog/crm/outreach/schedule-segment-export.png)

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 选择 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 导航到目标列表。
   ![显示浏览目标的平台UI屏幕截图。](../../assets/catalog/crm/outreach/browse-destinations.png)

1. 选择目标并验证状态为 **[!UICONTROL 已启用]**.
   ![显示选定目标的目标数据流运行的平台UI屏幕截图。](../../assets/catalog/crm/outreach/destination-dataflow-run.png)

1. 切换到 **[!DNL Activation data]** 选项卡，然后选择区段名称。
   ![显示目标激活数据的平台UI屏幕截图。](../../assets/catalog/crm/outreach/destinations-activation-data.png)

1. 监控区段摘要，并确保配置文件计数对应于在区段内创建的计数。
   ![显示区段摘要的Platform UI屏幕快照。](../../assets/catalog/crm/outreach/segment.png)

1. 登录到 [!DNL Outreach] 网站，然后导航到 [!DNL Apps] > [!DNL Contacts] 页面，并检查是否已添加区段中的配置文件。 您可以在中看到每个区段状态 [!DNL Outreach] 已根据，从Platform更新了相应的区段状态 [!UICONTROL 映射Id] 在以下时段提供的值： [区段调度](#schedule-segment-export-example) 步骤。

![外联UI屏幕截图显示了具有更新区段状态的外联潜在客户页面。](../../assets/catalog/crm/outreach/outreach-prospect.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关以下方面的详细信息： [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据治理概述](/help/data-governance/home.md).

## 错误和疑难解答 {#errors-and-troubleshooting}

检查数据流运行时，您可能会看到以下错误消息： `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![显示错误请求错误的平台UI屏幕截图。](../../assets/catalog/crm/outreach/error.png)

要修复此错误，请验证 [!UICONTROL 映射Id] 您在Platform中提供的 [!DNL Outreach] 区段有效并存在于中 [!DNL Outreach].

## 其他资源 {#additional-resources}

此 [[!DNL Outreach] 文档](https://api.outreach.io/api/v2/docs/) 的详细信息 [错误响应](https://api.outreach.io/api/v2/docs#error-responses) 可用于调试任何问题。
