---
keywords: CRM;CRM;CRM目标；Salesforce CRM;Salesforce CRM目标
title: Salesforce CRM连接
description: 利用Salesforce CRM目标，可导出帐户数据，并在Salesforce CRM中激活该数据以满足您的业务需求。
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: edf49d8a52eeddea65a18c1dad0035ec7e5d2c12
workflow-type: tm+mt
source-wordcount: '3089'
ht-degree: 0%

---

# [!DNL Salesforce CRM] 连接

## 概述 {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) 是一个流行的客户关系管理(CRM)平台，支持以下功能：

* [潜在客户](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm)  — 潜在顾客是指对您销售的产品或服务可能（或可能不可能）感兴趣的个人或公司。
* [联系人](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm)  — 联系人是指您的一位代表已与其建立关系并有资格成为潜在客户的个人。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm)，它支持上述两种类型的用户档案。

When [激活区段](#activate)，您可以在潜在客户或联系人之间进行选择，并将属性和区段数据更新到 [!DNL Salesforce CRM].

[!DNL Salesforce CRM] 使用带有密码授予的OAuth 2作为验证机制，与Salesforce REST API通信。 验证的说明 [!DNL Salesforce CRM] 实例位于下面的 [对目标进行身份验证](#authenticate) 中。

## 用例 {#use-cases}

作为营销人员，您可以根据用户Adobe Experience Platform用户档案的属性，向用户提供个性化体验。 您可以从离线数据构建区段，并将这些区段发送到Salesforce CRM，以便在Adobe Experience Platform中更新区段和配置文件后立即在用户信息源中显示。

## 先决条件 {#prerequisites}

### Experience Platform中的先决条件 {#prerequisites-in-experience-platform}

在将数据激活到Salesforce CRM目标之前，您必须具有 [模式](/help/xdm/schema/composition.md), a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 创建于 [!DNL Experience Platform].

### 先决条件 [!DNL Salesforce CRM] {#prerequisites-destination}

请注意 [!DNL Salesforce CRM]，以便将数据从Platform导出到您的Salesforce帐户：

#### 你需要 [!DNL Salesforce] 帐户 {#prerequisites-account}

转到 [!DNL Salesforce] [试用](https://www.salesforce.com/in/form/signup/freetrial-sales/) 用于注册和创建页面 [!DNL Salesforce] 帐户（如果您还没有）。

#### 在中配置连接的应用程序 [!DNL Salesforce] {#prerequisites-connected-app}

首先，您需要配置 [[!DNL Salesforce] 连接的应用程序](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) 在 [!DNL Salesforce] 帐户（如果您还没有）。 [!DNL Salesforce CRM] 将利用连接的应用程序连接到 [!DNL Salesforce].

接下来，启用 [!DNL OAuth Settings for API Integration] 对于 [!DNL Salesforce connected app]. 请参阅 [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 文档以获取指导。

另外，请确保 [范围](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 选择以下 [!DNL Salesforce connected app].

* ``chatter_api``
* ``lightning``
* ``visualforce``
* ``content``
* ``openid``
* ``full``
* ``api``
* ``web``
* ``refresh_token``
* ``offline_access``

最后，确保 `password` 在 [!DNL Salesforce] 帐户。 请参阅 [!DNL Salesforce] [适用于特殊情况的OAuth 2.0用户名 — 密码流](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&amp;type=5) 文档。

>[!IMPORTANT]
>
>如果 [!DNL Salesforce] 帐户管理员对受信任IP范围的访问权限受限，您需要联系他们以获取 [Experience PlatformIP](/help/destinations/catalog/streaming/ip-address-allow-list.md) 列入允许列表。 请参阅 [!DNL Salesforce] [限制对已连接应用程序的受信任IP范围的访问](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 文档。

#### 在中创建自定义字段 [!DNL Salesforce] {#prerequisites-custom-field}

将区段激活到 [!DNL Salesforce CRM] 目标，则必须在 **[!UICONTROL 映射ID]** 字段中 **[区段计划](#schedule-segment-export-example)** 中。

[!DNL Salesforce CRM] 需要此值才能正确读取和解释来自Experience Platform的区段，并在 [!DNL Salesforce]. 请参阅Experience Platform文档，以了解 [区段成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关区段状态的指导，请执行以下操作：

对于从Platform激活到 [!DNL Salesforce CRM]，则需要创建类型的自定义字段 `Text Area (Long)` within [!DNL Salesforce]. 您可以根据业务要求定义256 - 131,072个字符之间任意大小的字段字符长度。 请参阅 [!DNL Salesforce] [自定义字段类型](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&amp;type=5) 文档页面，以了解有关自定义字段类型的其他信息。 另请参阅 [!DNL Salesforce] 文档 [创建自定义字段](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) 如果您需要有关字段创建的帮助。

>[!IMPORTANT]
>
>字段名称中不要包含空格字符。 请改用下划线 `(_)` 字符。
>在 [!DNL Salesforce] 您必须使用 **[!UICONTROL 字段名称]** 与 **[!UICONTROL 映射ID]** 每个激活的平台区段。 例如，下面的屏幕截图显示了一个名为 `crm_2_seg`. 在将区段激活到此目标时，添加 `crm_2_seg` as **[!UICONTROL 映射ID]** 将Experience Platform中的区段受众填充到此自定义字段中。

中的自定义字段创建示例 [!DNL Salesforce], *第1步 — 选择数据类型*，如下所示：
![显示自定义字段创建的Salesforce UI屏幕截图，第1步 — 选择数据类型。](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

中的自定义字段创建示例 [!DNL Salesforce], *第2步 — 输入自定义字段的详细信息*，如下所示：
![显示自定义字段创建的Salesforce UI屏幕截图，第2步 — 输入自定义字段的详细信息。](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* 区分用于Platform区段的自定义字段和 [!DNL Salesforce] 创建自定义字段时，您可以包含可识别的前缀或后缀。 例如， `test_segment`，使用 `Adobe_test_segment` 或 `test_segment_Adobe`
>* 如果您已在中创建其他自定义字段 [!DNL Salesforce]，则可以使用与平台区段相同的名称，以便在 [!DNL Salesforce].


>[!NOTE]
>
>* Salesforce中的对象限制为25个外部字段，请参阅 [自定义字段属性](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* 此限制意味着您在任何时候最多只能有25个Experience Platform区段成员关系处于活动状态。
>* 如果您在Salesforce中已达到此限制，则必须从Salesforce中删除自定义属性，这些属性用于针对Experience Platform中的旧区段存储区段状态，然后才能新建 **[!UICONTROL 映射ID]** 中。


#### 收集 [!DNL Salesforce CRM] 凭据 {#gather-credentials}

在验证到 [!DNL Salesforce CRM] 目标：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `Username` | 您的 [!DNL Salesforce] 帐户用户名。 |  |
| `Password` | 您的 [!DNL Salesforce] 帐户密码。 |  |
| `Security Token` | 您的 [!DNL Salesforce] 安全令牌，稍后您会将该令牌附加到 [!DNL Salesforce] 用于创建要用作 **[!UICONTROL 密码]** when [对目标进行身份验证](#authenticate).<br> 请参阅 [!DNL Salesforce] 文档 [重置安全令牌](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&amp;type=5) 学习如何从 [!DNL Salesforce] 界面。 |  |
| `Custom Domain` | 您的 [!DNL Salesforce] 域前缀。 <br> 请参阅 [[!DNL Salesforce] 文档](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) 了解如何从 [!DNL Salesforce] 界面。 | 如果 [!DNL Salesforce] 域<br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*,<br> 您需要 `d5i000000isb4eak-dev-ed` 作为值。 |
| `Client ID` | 您的销售人员 `Consumer Key`. <br> 请参阅 [[!DNL Salesforce] 文档](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 了解如何从 [!DNL Salesforce] 界面。 |  |
| `Client Secret` | 您的销售人员 `Consumer Secret`. <br> 请参阅 [[!DNL Salesforce] 文档](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 了解如何从 [!DNL Salesforce] 界面。 |  |

### 护栏 {#guardrails}

[!DNL Salesforce] 通过施加请求、费率和超时限制来平衡事务加载。 请参阅 [API请求限制和分配](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) 以了解详细信息。

如果 [!DNL Salesforce] 帐户管理员已强制实施IP限制，您需要添加 [Experience PlatformIP地址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 至 [!DNL Salesforce] 帐户的受信任IP范围。 请参阅 [!DNL Salesforce] [限制对已连接应用程序的受信任IP范围的访问](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 文档。

>[!IMPORTANT]
>
>When [激活区段](#activate) 必须选择 *联系人* 或 *商机* 类型。 您需要确保区段具有根据所选类型的相应数据映射。

## 支持的身份 {#supported-identities}

[!DNL Salesforce CRM] 支持更新下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 描述 | 注意事项 |
|---|---|---|
| `SalesforceId` | 的 [!DNL Salesforce CRM] 您通过区段导出或更新的联系人或潜在客户标识的标识符。 | 必需 |

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | <ul><li>您正在导出区段的所有成员，以及所需的架构字段 *(例如：电子邮件地址、电话号码、姓氏)*，则会根据字段映射。</li><li> 每个区段状态位于 [!DNL Salesforce CRM] 会根据 **[!UICONTROL 映射ID]** 值 [区段计划](#schedule-segment-export-example) 中。</li></ul> |
| 导出频度 | **[!UICONTROL 流]** | <ul><li>流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

在 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 搜索 [!DNL Salesforce CRM]. 或者，您也可以在 **[!UICONTROL CRM]** 类别。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请填写以下必填字段并选择 **[!UICONTROL 连接到目标]**. 请参阅 [收集 [!DNL Salesforce CRM] 凭据](#gather-credentials) 部分。
|凭据 |描述 | | — | — | | **[!UICONTROL 用户名]** |您的 [!DNL Salesforce] 帐户用户名。 | | **[!UICONTROL 密码]** |由 [!DNL Salesforce] 帐户密码附加了您的 [!DNL Salesforce] 安全令牌。<br>拼接值采用 `{PASSWORD}{TOKEN}`.<br> 请注意，请勿使用任何大括号或空格。<br>例如，如果 [!DNL Salesforce] 密码为 `MyPa$$w0rd123` 和 [!DNL Salesforce] 安全令牌为 `TOKEN12345....0000`，您将在 **[!UICONTROL 密码]** 字段 `MyPa$$w0rd123TOKEN12345....0000`. | | **[!UICONTROL 自定义域]** |您的 [!DNL Salesforce] 域前缀。 <br>例如，如果您的域为 *`d5i000000isb4eak-dev-ed`.my.salesforce.com*，您需要提供 `d5i000000isb4eak-dev-ed` 作为值。 | | **[!UICONTROL 客户端ID]** |您的 [!DNL Salesforce] 连接的应用程序 `Consumer Key`. | | **[!UICONTROL 客户端密钥]** |您的 [!DNL Salesforce] 连接的应用程序 `Consumer Secret`. |

![Platform UI屏幕截图，其中显示了如何进行身份验证。](../../assets/catalog/crm/salesforce/authenticate-destination.png)

如果提供的详细信息有效，UI会显示 **[!UICONTROL 已连接]** 状态中显示绿色复选标记，则可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
* **[!UICONTROL 名称]**:将来用于识别此目标的名称。
* **[!UICONTROL 描述]**:此描述将帮助您在将来确定此目标。
* **[!UICONTROL Salesforce ID类型]**:
   * 选择 **[!UICONTROL 联系人]** 如果要导出或更新的身份类型为 *联系人*.
   * 选择 **[!UICONTROL 商机]** 如果要导出或更新的身份类型为 *商机*.

![Platform UI屏幕截图，显示目标详细信息。](../../assets/catalog/crm/salesforce/destination-details.png)

### 启用警报 {#enable-alerts}

您可以启用警报以接收有关目标数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，请选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
>
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

读取 [激活用户档案和区段以流式传输区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射注意事项和示例 {#mapping-considerations-example}

要将受众数据从Adobe Experience Platform正确发送到 [!DNL Salesforce CRM] 目标，您需要完成字段映射步骤。 映射包括在Platform帐户中的体验数据模型(XDM)架构字段与目标目标中相应的对等字段之间创建一个链接。

在 **[!UICONTROL 目标字段]** 应完全按照属性映射表中所述的名称命名，因为这些属性将构成请求正文。

在 **[!UICONTROL 源字段]** 不要遵守任何此类限制。 您可以根据需要映射数据，但请根据 [[!DNL Salesforce] 文档](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5). 如果输入数据无效，则对 [!DNL Salesforce] 将失败，并且您的联系人/潜在客户将不会更新。

要将XDM字段正确映射到 [!DNL (API) Salesforce CRM] 目标字段，请执行以下步骤：

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**，则会在屏幕上看到一个新的映射行。
   ![Platform UI中“添加新映射”的屏幕截图示例。](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. 在 **[!UICONTROL 选择源字段]** 窗口，选择 **[!UICONTROL 选择属性]** 类别，然后选择XDM属性或 **[!UICONTROL 选择身份命名空间]** 并选择一个身份。
1. 在 **[!UICONTROL 选择目标字段]** 窗口，选择 **[!UICONTROL 选择身份命名空间]** 选择身份或选择 **[!UICONTROL 选择自定义属性]** 类别，然后选择属性或使用 **[!UICONTROL 属性名称]** 字段。 请参阅 [[!DNL Salesforce CRM] 文档](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) ，以获取有关受支持属性的指导。
   * 重复这些步骤，在XDM配置文件架构和 [!DNL (API) Salesforce CRM]:

   **使用联系人**

   * 如果您正在使用 *联系人* 在区段中，请参阅Salesforce中的对象引用，以获取 [联系人](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) 定义要更新的字段的映射。
   * 您可以通过搜索单词来识别必填字段 *必需*，在上述链接的字段描述中提及。
   * 根据要导出或更新的字段，添加XDM配置文件架构与 [!DNL (API) Salesforce CRM]: |源字段|目标字段|注释 | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. 联系人的姓氏，最多80个字符。 |\
      |`xdm: person.name.firstName`|`Attribute: FirstName`|联系人的名字最多40个字符。 | |`xdm: personalEmail.address`|`Attribute: Email`|联系人的电子邮件地址。 |

   * 使用这些映射的示例如下所示：
      ![平台UI屏幕截图示例，其中显示了目标映射。](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **使用潜在客户**

   * 如果您正在使用 *潜在客户* 在区段中，请参阅Salesforce中的对象引用，以获取 [商机](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) 定义要更新的字段的映射。
   * 您可以通过搜索单词来识别必填字段 *必需*，在上述链接的字段描述中提及。
   * 根据要导出或更新的字段，添加XDM配置文件架构与 [!DNL (API) Salesforce CRM]: |源字段|目标字段|注释 | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. 最多80个字符的前导的姓氏。 |\
      |`xdm: b2b.companyName`|`Attribute: Company`| `Mandatory`. 领导的公司。 | |`xdm: personalEmail.address`|`Attribute: Email`|潜在客户的电子邮件地址。 |

   * 使用这些映射的示例如下所示：
      ![平台UI屏幕截图示例，其中显示了目标映射。](../../assets/catalog/crm/salesforce/mappings-leads.png)



完成为目标连接提供映射后，请选择 **[!UICONTROL 下一个]**.

### 计划区段导出和示例 {#schedule-segment-export-example}

执行 [计划区段导出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 步骤您必须在 [!DNL Salesforce].

为此，请选择每个区段，然后输入 [!DNL Salesforce] 在 [!DNL Salesforce CRM] **[!UICONTROL 映射ID]** 字段。 请参阅 [在中创建自定义字段 [!DNL Salesforce]](#prerequisites-custom-field) 部分，以了解有关在 [!DNL Salesforce].

例如，如果 [!DNL Salesforce] 自定义字段 `crm_2_seg`，请在 [!DNL Salesforce CRM] **[!UICONTROL 映射ID]** 将Experience Platform中的区段受众填充到此自定义字段中。

中的自定义字段示例 [!DNL Salesforce] 如下所示：
![[!DNL Salesforce] 显示自定义字段的UI屏幕截图。](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

指示 [!DNL Salesforce CRM] **[!UICONTROL 映射ID]** 如下所示：
![Platform UI屏幕截图示例显示了计划区段导出。](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

如 [!DNL Salesforce] **[!UICONTROL 字段名称]** 与 [!DNL Salesforce CRM] **[!UICONTROL 映射ID]**.

根据您的用例，所有激活的区段都可以映射到相同的 [!DNL Salesforce] 自定义字段或其他 **[!UICONTROL 字段名称]** in [!DNL Salesforce CRM]. 基于上面所示图像的典型示例可能是。
| [!DNL Salesforce CRM] 区段名称 | [!DNL Salesforce] **[!UICONTROL 字段名称]** | [!DNL Salesforce CRM] **[!UICONTROL 映射ID]** | | — | — | — | | crm_1_seg | `crm_1_seg` | `crm_1_seg` | | crm_2_seg | `crm_2_seg` | `crm_2_seg` |

对每个激活的平台区段重复此部分。

## 验证数据导出 {#exported-data}

要验证您是否已正确设置目标，请执行以下步骤：

1. 选择 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 导航到目标列表。
   ![显示浏览目标的平台UI屏幕截图。](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. 选择目标并验证状态是否为 **[!UICONTROL 已启用]**.
   ![Platform UI屏幕截图，其中显示了目标数据流运行。](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. 切换到 **[!UICONTROL 激活数据]** ，然后选择区段名称。
   ![Platform UI屏幕截图示例，其中显示了目标激活数据。](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. 监控区段摘要，并确保配置文件计数与区段内创建的计数相对应。
   ![平台UI屏幕截图示例，其中显示了区段。](../../assets/catalog/crm/salesforce/segment.png)

1. 最后，登录到Salesforce网站，并验证是否已添加或更新区段中的用户档案。

   **使用联系人**

   * 如果已选择 *联系人* 在平台区段中，导航到 **[!DNL Apps]** > **[!DNL Contacts]** 页面。
      ![Salesforce CRM屏幕截图显示包含区段中用户档案的“联系人”页面。](../../assets/catalog/crm/salesforce/contacts.png)

   * 选择 *联系人* 并检查字段是否已更新。 您可以在 [!DNL Salesforce CRM] 更新时，会根据 **[!UICONTROL 映射ID]** 值 [区段计划](#schedule-segment-export-example).
      ![Salesforce CRM屏幕截图显示了具有更新区段状态的“联系人详细信息”页面。](../../assets/catalog/crm/salesforce/contact-info.png)

   **使用潜在客户**

   * 如果已选择 *潜在客户* ，然后导航到 **[!DNL Apps]** > **[!DNL Leads]** 页面。
      ![Salesforce CRM屏幕截图，其中显示了包含区段配置文件的“潜在客户”页面。](../../assets/catalog/crm/salesforce/leads.png)

   * 选择 *商机* 并检查字段是否已更新。 您可以在 [!DNL Salesforce CRM] 更新时，会根据 **[!UICONTROL 映射ID]** 值 [区段计划](#schedule-segment-export-example).
      ![Salesforce CRM屏幕截图显示了具有更新区段状态的“潜在客户详细信息”页面。](../../assets/catalog/crm/salesforce/lead-info.png)


## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](/help/data-governance/home.md).

## 错误和疑难解答 {#errors-and-troubleshooting}

### 将事件推送到目标时遇到未知错误 {#unknown-errors}

* 检查数据流运行时，您可能会遇到以下错误消息： `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

   ![显示错误的平台UI屏幕截图。](../../assets/catalog/crm/salesforce/error.png)

   * 要修复此错误，请验证 **[!UICONTROL 映射ID]** 激活工作流中提供的 [!DNL Salesforce CRM] 目标与您在中创建的自定义字段类型的值完全匹配 [!DNL Salesforce]. 请参阅 [在中创建自定义字段 [!DNL Salesforce]](#prerequisites-custom-field) 部分。

* 激活区段时，可能会收到一条错误消息： `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * 要修复此错误，请与 [!DNL Salesforce] 帐户管理员添加 [Experience PlatformIP地址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 至 [!DNL Salesforce] 帐户的受信任IP范围。 请参阅 [!DNL Salesforce] [限制对已连接应用程序的受信任IP范围的访问](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 文档。

## 其他资源 {#additional-resources}

来自 [Salesforce开发人员门户](https://developer.salesforce.com/) 如下所示：
* [快速入门](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [创建记录](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [自定义推荐受众](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [使用复合资源](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* 此目标可利用 [重新插入多个记录](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API，而不是 [重新插入单个记录](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) API调用。