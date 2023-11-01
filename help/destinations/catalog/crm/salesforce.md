---
keywords: crm；CRM；CRM目标；salesforce crm；salesforce crm目标
title: Salesforce CRM连接
description: Salesforce CRM目标允许您导出帐户数据，并在Salesforce CRM中激活该数据，以满足您的业务需求。
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '3117'
ht-degree: 0%

---

# [!DNL Salesforce CRM] 连接

## 概述 {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) 是一个流行的客户关系管理(CRM)平台，它支持以下内容：

* [潜在客户](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm)  — 潜在客户是可能对您销售的产品或服务感兴趣（也可能不感兴趣）的个人或公司的名称。
* [联系人](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm)  — 联系人是您的代表之一已建立关系并已被鉴定为潜在客户的个人。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm)，它支持上述两种类型的用户档案。

时间 [激活区段](#activate)，您可以在潜在客户或联系人之间进行选择，并将属性和受众数据更新到 [!DNL Salesforce CRM].

[!DNL Salesforce CRM] 使用带有密码授予的OAuth 2作为身份验证机制，与Salesforce REST API进行通信。 向您的验证的说明 [!DNL Salesforce CRM] 实例位于 [向目标进行身份验证](#authenticate) 部分。

## 用例 {#use-cases}

作为营销人员，您可以根据用户的Adobe Experience Platform配置文件中的属性，为其提供个性化体验。 您可以从离线数据构建受众，并将这些受众发送到Salesforce CRM，以便在Adobe Experience Platform中更新受众和配置文件后立即显示在用户的馈送中。

## 先决条件 {#prerequisites}

### Experience Platform中的先决条件 {#prerequisites-in-experience-platform}

在将数据激活到Salesforce CRM目标之前，您必须拥有 [架构](/help/xdm/schema/composition.md)， a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)、和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) 创建于 [!DNL Experience Platform].

### 中的先决条件 [!DNL Salesforce CRM] {#prerequisites-destination}

请注意中的以下先决条件 [!DNL Salesforce CRM]，以便将数据从Platform导出到您的Salesforce帐户：

#### 您需要拥有 [!DNL Salesforce] 帐户 {#prerequisites-account}

转到 [!DNL Salesforce] [试用版](https://www.salesforce.com/in/form/signup/freetrial-sales/) 页面以注册和创建 [!DNL Salesforce] 帐户（如果还没有帐户）。

#### 在中配置连接的应用程序 [!DNL Salesforce] {#prerequisites-connected-app}

首先，您需要配置 [[!DNL Salesforce] 连接的应用程序](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) 在您的 [!DNL Salesforce] 帐户（如果还没有帐户）。 [!DNL Salesforce CRM] 将利用连接的应用程序连接到 [!DNL Salesforce].

下一步，启用 [!DNL OAuth Settings for API Integration] 对于 [!DNL Salesforce connected app]. 请参阅 [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 指导文档。

此外，确保 [范围](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 以下提及的已选为 [!DNL Salesforce connected app].

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

最后，确保 `password` 授权已在以下位置启用： [!DNL Salesforce] 帐户。 请参阅 [!DNL Salesforce] [适用于特殊方案的OAuth 2.0用户名 — 密码流程](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&amp;type=5) 文档（如果您需要指南）。

>[!IMPORTANT]
>
>如果您的 [!DNL Salesforce] 帐户管理员限制了对受信任IP范围的访问，您需要联系他们以获取 [EXPERIENCE PLATFORMIP](/help/destinations/catalog/streaming/ip-address-allow-list.md) 已列入允许列表 请参阅 [!DNL Salesforce] [限制对连接应用程序的受信任IP范围的访问](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 文档（如果您需要其他指导）。

#### 在中创建自定义字段 [!DNL Salesforce] {#prerequisites-custom-field}

将受众激活到 [!DNL Salesforce CRM] 目标，则必须在 **[!UICONTROL 映射Id]** 每个已激活受众的字段，位于 **[受众计划](#schedule-segment-export-example)** 步骤。

[!DNL Salesforce CRM] 需要此值才能正确读取和解释从Experience Platform传入的受众，并在中更新其受众状态 [!DNL Salesforce]. 请参阅Experience Platform文档，了解 [受众成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关受众状态的指南。

对于从Platform激活的每个受众 [!DNL Salesforce CRM]，您需要创建类型的自定义字段 `Text Area (Long)` 范围 [!DNL Salesforce]. 您可以根据业务要求定义字段字符长度，长度不限，可为256 - 131,072个字符。 请参阅 [!DNL Salesforce] [自定义字段类型](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&amp;type=5) 文档页面，以了解有关自定义字段类型的更多信息。 另请参阅 [!DNL Salesforce] 文档目标 [创建自定义字段](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) 如果您在字段创建方面需要帮助。

>[!IMPORTANT]
>
>请勿在字段名称中包含空白字符。 请改用下划线 `(_)` 字符。
>范围 [!DNL Salesforce] 您必须创建自定义字段 **[!UICONTROL 字段名称]** 完全匹配 **[!UICONTROL 映射Id]** 每个已激活的Platform区段。 例如，下面的屏幕截图显示了一个名为的自定义字段 `crm_2_seg`. 将受众激活到此目标时，添加 `crm_2_seg` 作为 **[!UICONTROL 映射Id]** 用于将Experience Platform中的受众填充到此自定义字段中。

中的自定义字段创建示例 [!DNL Salesforce]， *第1步 — 选择数据类型*，如下所示：
![显示自定义字段创建的Salesforce UI屏幕截图，第1步 — 选择数据类型。](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

中的自定义字段创建示例 [!DNL Salesforce]， *第2步 — 输入自定义字段的详细信息*，如下所示：
![显示自定义字段创建的Salesforce UI屏幕截图，第2步 — 输入自定义字段的详细信息。](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* 区分用于Platform受众的自定义字段和中的其他自定义字段 [!DNL Salesforce] 创建自定义字段时，您可以包含可识别的前缀或后缀。 例如，而不是 `test_segment`，使用 `Adobe_test_segment` 或 `test_segment_Adobe`
>* 如果您已在中创建其他自定义字段 [!DNL Salesforce]，您可以使用与Platform区段相同的名称，以轻松地识别中的受众 [!DNL Salesforce].

>[!NOTE]
>
>* Salesforce中的对象限制为25个外部字段，请参阅 [自定义字段属性](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* 此限制意味着在任何时候，最多只能有25个处于活动状态的Experience Platform受众成员资格。
>* 如果您在Salesforce中达到了此限制，则必须先从Salesforce中删除用于存储Experience Platform中针对旧受众的受众状态的自定义属性，然后再存储新受众 **[!UICONTROL 映射Id]** 可以使用。

#### 收集 [!DNL Salesforce CRM] 凭据 {#gather-credentials}

在对进行身份验证之前，请记下以下各项 [!DNL Salesforce CRM] 目标：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `Username` | 您的 [!DNL Salesforce] 帐户用户名。 | |
| `Password` | 您的 [!DNL Salesforce] 帐户密码。 | |
| `Security Token` | 您的 [!DNL Salesforce] 安全令牌，您稍后会将其附加到您的令牌的末尾 [!DNL Salesforce] 用于创建要用作 **[!UICONTROL 密码]** 时间 [向目标进行身份验证](#authenticate).<br> 请参阅 [!DNL Salesforce] 文档目标 [重置您的安全令牌](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&amp;type=5) 学习如何从以下位置重新生成它： [!DNL Salesforce] 界面（如果您没有安全令牌）。 |  |
| `Custom Domain` | 您的 [!DNL Salesforce] 域前缀。 <br> 请参阅 [[!DNL Salesforce] 文档](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) 以了解如何从获取此值 [!DNL Salesforce] 界面。 | 如果您的 [!DNL Salesforce] 域为<br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*，<br> 您将需要 `d5i000000isb4eak-dev-ed` 作为值。 |
| `Client ID` | 您的Salesforce `Consumer Key`. <br> 请参阅 [[!DNL Salesforce] 文档](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 以了解如何从获取此值 [!DNL Salesforce] 界面。 | |
| `Client Secret` | 您的Salesforce `Consumer Secret`. <br> 请参阅 [[!DNL Salesforce] 文档](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 以了解如何从获取此值 [!DNL Salesforce] 界面。 | |

### 护栏 {#guardrails}

[!DNL Salesforce] 通过设置请求、速率和超时限制来平衡事务加载。 请参阅 [API请求限制和分配](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) 以了解详细信息。

如果您的 [!DNL Salesforce] 帐户管理员已强制实施IP限制，您需要添加 [Experience PlatformIP地址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 敬您的 [!DNL Salesforce] 帐户的受信任IP范围。 请参阅 [!DNL Salesforce] [限制对连接应用程序的受信任IP范围的访问](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 文档（如果您需要其他指导）。

>[!IMPORTANT]
>
>时间 [激活区段](#activate) 您必须选择以下任一选项 *联系人* 或 *商机* 类型。 您需要确保受众具有符合所选类型的相应数据映射。

## 支持的身份 {#supported-identities}

[!DNL Salesforce CRM] 支持更新下表中描述的标识。 了解有关 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| `SalesforceId` | 此 [!DNL Salesforce CRM] 通过区段导出或更新之联系人或潜在客户身份的标识符。 | 必需 |

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在导出区段的所有成员以及所需的架构字段 *（例如：电子邮件地址、电话号码、姓氏）*，根据您的字段映射。</li><li> 中的每个受众状态 [!DNL Salesforce CRM] 将根据 **[!UICONTROL 映射Id]** 值在 [受众调度](#schedule-segment-export-example) 步骤。</li></ul> |
| 导出频率 | **[!UICONTROL 流]** | <ul><li>流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

范围 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 搜索 [!DNL Salesforce CRM]. 或者，您可以将其定位到 **[!UICONTROL CRM]** 类别。

### 向目标进行身份验证 {#authenticate}

要向目标进行身份验证，请填写以下必填字段并选择 **[!UICONTROL 连接到目标]**. 请参阅 [收集 [!DNL Salesforce CRM] 凭据](#gather-credentials) 部分获取任何指导。
|凭据 |描述 | | — | — | | **[!UICONTROL 用户名]** |您的 [!DNL Salesforce] 帐户用户名。 | | **[!UICONTROL 密码]** |由 [!DNL Salesforce] 帐户密码已附加到您的 [!DNL Salesforce] 安全令牌。<br>连接的值采用以下形式 `{PASSWORD}{TOKEN}`.<br> 注意，请勿使用任何大括号或空格。<br>例如，如果您的 [!DNL Salesforce] 密码为 `MyPa$$w0rd123` 和 [!DNL Salesforce] 安全令牌为 `TOKEN12345....0000`，则您将在 **[!UICONTROL 密码]** 字段为 `MyPa$$w0rd123TOKEN12345....0000`. | | **[!UICONTROL 自定义域]** |您的 [!DNL Salesforce] 域前缀。 <br>例如，如果您的域是 *`d5i000000isb4eak-dev-ed`.my.salesforce.com*，您需要提供 `d5i000000isb4eak-dev-ed` 作为值。 | | **[!UICONTROL 客户端ID]** |您的 [!DNL Salesforce] 连接的应用程序 `Consumer Key`. | | **[!UICONTROL 客户端密码]** |您的 [!DNL Salesforce] 连接的应用程序 `Consumer Secret`. |

![显示如何进行身份验证的平台UI屏幕截图。](../../assets/catalog/crm/salesforce/authenticate-destination.png)

如果提供的详细信息有效，UI将显示 **[!UICONTROL 已连接]** 状态，带有绿色复选标记，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL Salesforce ID类型]**：
   * 选择 **[!UICONTROL 联系人]** 如果要导出或更新标识的类型为 *联系人*.
   * 选择 **[!UICONTROL 商机]** 如果要导出或更新标识的类型为 *商机*.

![显示目标详细信息的平台UI屏幕截图。](../../assets/catalog/crm/salesforce/destination-details.png)

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

要正确地将受众数据从Adobe Experience Platform发送到 [!DNL Salesforce CRM] 目标，您需要执行字段映射步骤。 映射包括在您的Platform帐户中的Experience Data Model (XDM)架构字段与其在目标目标中的相应等效字段之间创建链接。

中指定的属性 **[!UICONTROL 目标字段]** 应完全按照属性映射表中所述命名，因为这些属性将构成请求正文。

中指定的属性 **[!UICONTROL 源字段]** 请勿遵循任何此类限制。 您可以根据需要进行映射，但请确保输入数据的格式根据 [[!DNL Salesforce] 文档](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5). 如果输入数据无效，则更新调用 [!DNL Salesforce] 将失败，您的联系人/潜在客户将无法更新。

要将XDM字段正确映射到 [!DNL (API) Salesforce CRM] 目标字段，请执行以下步骤：

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**，您将在屏幕上看到一个新映射行。
   ![用于添加新映射的平台UI屏幕快照示例。](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. 在 **[!UICONTROL 选择源字段]** 窗口中，选择 **[!UICONTROL 选择属性]** 类别并选择XDM属性或选择 **[!UICONTROL 选择身份命名空间]** 并选择身份。
1. 在 **[!UICONTROL 选择目标字段]** 窗口中，选择 **[!UICONTROL 选择身份命名空间]** 并选择身份或选择 **[!UICONTROL 选择自定义属性]** 类别并选择属性，或者使用 **[!UICONTROL 属性名称]** 字段。 请参阅 [[!DNL Salesforce CRM] 文档](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) 以获取有关支持属性的指导。
   * 重复这些步骤以在XDM配置文件架构和 [!DNL (API) Salesforce CRM]：

   **使用联系人**

   * 如果您使用的是 *联系人* 在区段中，请参阅Salesforce中的对象引用，以了解 [联系人](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) 以定义要更新的字段的映射。
   * 您可以通过搜索单词来标识必填字段 *必填*，如上述链接中的字段描述中所述。
   * 根据要导出或更新字段，在XDM配置文件架构和之间添加映射 [!DNL (API) Salesforce CRM]： |源字段|目标字段|注释 | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. 联系人的姓氏，最多80个字符。 |\
     |`xdm: person.name.firstName`|`Attribute: FirstName`|联系人的名字，最多40个字符。 | |`xdm: personalEmail.address`|`Attribute: Email`|联系人的电子邮件地址。 |

   * 下面显示了使用这些映射的示例：
     ![显示Target映射的平台UI屏幕截图示例。](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **使用潜在客户**

   * 如果您使用的是 *潜在客户* 在区段中，请参阅Salesforce中的对象引用，以了解 [商机](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) 以定义要更新的字段的映射。
   * 您可以通过搜索单词来标识必填字段 *必填*，如上述链接中的字段描述中所述。
   * 根据要导出或更新字段，在XDM配置文件架构和之间添加映射 [!DNL (API) Salesforce CRM]： |源字段|目标字段|注释 | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. 潜在客户的姓氏最多为80个字符。 |\
     |`xdm: b2b.companyName`|`Attribute: Company`| `Mandatory`. 潜在客户的公司。 | |`xdm: personalEmail.address`|`Attribute: Email`|商机的电子邮件地址。 |

   * 下面显示了使用这些映射的示例：
     ![显示Target映射的平台UI屏幕截图示例。](../../assets/catalog/crm/salesforce/mappings-leads.png)

完成提供目标连接的映射后，选择 **[!UICONTROL 下一个]**.

### 计划受众导出和示例 {#schedule-segment-export-example}

执行 [计划受众导出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 步骤：您必须手动将从Platform激活的受众映射到中对应的自定义字段 [!DNL Salesforce].

要实现此目的，请选择每个区段，然后从中输入自定义字段名称 [!DNL Salesforce] 在 [!DNL Salesforce CRM] **[!UICONTROL 映射Id]** 字段。 请参阅 [在中创建自定义字段 [!DNL Salesforce]](#prerequisites-custom-field) 有关在中创建自定义字段的指导和最佳实践的部分 [!DNL Salesforce].

例如，如果您的 [!DNL Salesforce] 自定义字段为 `crm_2_seg`，请在 [!DNL Salesforce CRM] **[!UICONTROL 映射Id]** 用于将Experience Platform中的受众填充到此自定义字段中。

中的自定义字段示例 [!DNL Salesforce] 如下所示：
![[!DNL Salesforce] 显示自定义字段的UI屏幕快照。](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

一个示例，指示 [!DNL Salesforce CRM] **[!UICONTROL 映射Id]** 如下所示：
![显示计划受众导出的平台UI屏幕截图示例。](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

如上所示 [!DNL Salesforce] **[!UICONTROL 字段名称]** 与 [!DNL Salesforce CRM] **[!UICONTROL 映射Id]**.

根据您的用例，所有激活的受众都可以映射到相同的 [!DNL Salesforce] 自定义字段或其他 **[!UICONTROL 字段名称]** 在 [!DNL Salesforce CRM]. 基于上述图像的典型示例可能是。
| [!DNL Salesforce CRM] 区段名称 | [!DNL Salesforce] **[!UICONTROL 字段名称]** | [!DNL Salesforce CRM] **[!UICONTROL 映射Id]** | | — | — | — | | crm_1_seg | `crm_1_seg` | `crm_1_seg` | | crm_2_seg | `crm_2_seg` | `crm_2_seg` |

对每个激活的Platform区段重复此部分。

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 选择 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 导航到目标列表。
   ![显示浏览目标的平台UI屏幕截图。](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. 选择目标并验证状态为 **[!UICONTROL 已启用]**.
   ![显示目标数据流运行的平台UI屏幕快照。](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. 切换到 **[!UICONTROL 激活数据]** 选项卡，然后选择受众名称。
   ![显示目标激活数据的平台UI屏幕截图示例。](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. 监控受众摘要，并确保用户档案计数对应于在区段内创建的计数。
   ![显示区段的平台UI屏幕截图示例。](../../assets/catalog/crm/salesforce/segment.png)

1. 最后，登录Salesforce网站并验证受众中的配置文件是否已添加或更新。

   **使用联系人**

   * 如果您已选择 *联系人* 在您的Platform区段中，导航到 **[!DNL Apps]** > **[!DNL Contacts]** 页面。
     ![Salesforce CRM屏幕截图，其中显示了“联系人”页面及客户细分中的配置文件。](../../assets/catalog/crm/salesforce/contacts.png)

   * 选择 *联系人* 并检查字段是否已更新。 您可以在中看到每个受众状态 [!DNL Salesforce CRM] 已根据，从Platform更新了相应的受众状态 **[!UICONTROL 映射Id]** 值在 [受众调度](#schedule-segment-export-example).
     ![Salesforce CRM屏幕截图，其中显示了“联系人详细信息”页面以及更新的受众状态。](../../assets/catalog/crm/salesforce/contact-info.png)

   **使用潜在客户**

   * 如果您已选择 *潜在客户* 在您的Platform区段中，导航到 **[!DNL Apps]** > **[!DNL Leads]** 页面。
     ![Salesforce CRM屏幕截图，其中显示了“潜在客户”页面以及客户细分中的配置文件。](../../assets/catalog/crm/salesforce/leads.png)

   * 选择 *商机* 并检查字段是否已更新。 您可以在中看到每个受众状态 [!DNL Salesforce CRM] 已根据，从Platform更新了相应的受众状态 **[!UICONTROL 映射Id]** 值在 [受众调度](#schedule-segment-export-example).
     ![Salesforce CRM屏幕截图，其中显示具有更新受众状态的“潜在客户详细信息”页面。](../../assets/catalog/crm/salesforce/lead-info.png)

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据管理概述](/help/data-governance/home.md).

## 错误和故障排除 {#errors-and-troubleshooting}

### 将事件推送到目标时报告了未知错误 {#unknown-errors}

* 检查数据流运行时，您可能会遇到以下错误消息： `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![平台UI屏幕截图显示错误。](../../assets/catalog/crm/salesforce/error.png)

   * 要修复此错误，请验证 **[!UICONTROL 映射Id]** 您在激活工作流中提供的电子邮件至 [!DNL Salesforce CRM] 目标与您在中创建的自定义字段类型的值完全匹配 [!DNL Salesforce]. 请参阅 [在中创建自定义字段 [!DNL Salesforce]](#prerequisites-custom-field) 部分提供指导。

* 激活区段时，您可能会收到一条错误消息： `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * 要修复此错误，请联系贵机构的 [!DNL Salesforce] 要添加的客户管理员 [Experience PlatformIP地址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 敬您的 [!DNL Salesforce] 帐户的受信任IP范围。 请参阅 [!DNL Salesforce] [限制对连接应用程序的受信任IP范围的访问](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 文档（如果您需要其他指导）。

## 其他资源 {#additional-resources}

其他有用信息来自 [Salesforce开发人员门户](https://developer.salesforce.com/) 如下所示：
* [快速入门](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [创建记录](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [自定义推荐受众](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [使用复合资源](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* 此目标利用 [更新插入多个记录](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API而不是 [更新插入单个记录](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) API调用。