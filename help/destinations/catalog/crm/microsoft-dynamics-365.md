---
keywords: crm;CRM;CRM目标；Microsoft Dynamics 365;Microsoft Dynamics 365 CRM目标
title: Microsoft Dynamics 365连接
description: 利用Microsoft Dynamics 365目标，可导出帐户数据，并在Microsoft Dynamics 365中激活该数据，以满足您的业务需求。
source-git-commit: 12af2ee40d355119104d741630654d2847df6cc5
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 1%

---


# [!DNL Microsoft Dynamics 365] 连接

## 概述 {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/) 是一个基于云的业务应用程序平台，它将企业资源规划(ERP)和客户关系管理(CRM)与生产力应用程序和AI工具结合在一起，从而实现端到端更顺畅、更受控制的操作、更好的增长潜力和降低成本。

此 [!DNL Adobe Experience Platform] [目标](/help/destinations/home.md) 利用 [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1)，用于将区段内的标识更新为 [!DNL Dynamics 365].

[!DNL Dynamics 365] 使用具有授权授权的OAuth 2作为验证机制与 [!DNL Contact Entity Reference API]. 验证的说明 [!DNL Dynamics 365] 实例位于下面的 [对目标进行身份验证](#authenticate) 中。

## 用例 {#use-cases}

作为营销人员，您可以根据用户Adobe Experience Platform用户档案的属性，向用户提供个性化体验。 您可以根据离线数据构建区段，并将这些区段发送到 [!DNL Dynamics 365]，以便在Adobe Experience Platform中更新区段和配置文件后，立即在用户信息源中显示。

## 先决条件 {#prerequisites}

### Experience Platform先决条件 {#prerequisites-in-experience-platform}

在将数据激活到 [!DNL Dynamics 365] 目标，您必须具有 [模式](/help/xdm/schema/composition.md), a [数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)和 [区段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 创建于 [!DNL Experience Platform].

有关信息，请参阅Adobe的文档 [区段成员资格详细信息架构字段组](/help/xdm/field-groups/profile/segmentation.md) 如果您需要有关区段状态的指导，请执行以下操作：

### [!DNL Microsoft Dynamics 365] 先决条件 {#prerequisites-destination}

请注意 [!DNL Dynamics 365]，以便将数据从Platform导出到 [!DNL Dynamics 365] 帐户：

#### 你需要 [!DNL Microsoft Dynamics 365] 帐户 {#prerequisites-account}

转到 [!DNL Dynamics 365] [试用](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) 页面以注册和创建帐户（如果尚未注册）。

#### 在中创建字段 [!DNL Dynamics 365] {#prerequisites-custom-field}

创建类型的自定义字段 `Simple` 将字段数据类型设置为 `Single Line of Text` 用于更新 [!DNL Dynamics 365].
请参阅 [!DNL Dynamics 365] 文档 [创建字段（属性）](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) 如果您需要其他指导，请执行以下操作。

中的设置示例 [!DNL Dynamics 365] 如下所示：
![Dynamics 365 UI屏幕截图，显示自定义字段。](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### 在Azure Active Directory中注册应用程序和应用程序用户 {#prerequisites-app-user}

启用 [!DNL Dynamics 365] 要访问您登录时需要的资源，请执行以下操作： [!DNL Azure Account] to [[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) 并创建以下内容：
* 安 [!DNL Azure Active Directory] 应用程序
* 服务主体
* 应用程序密钥

您还需要 [创建应用程序用户](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) in [!DNL Azure Active Directory] 并将其与新创建的应用程序关联。

#### 收集 [!DNL Dynamics 365] 凭据 {#gather-credentials}

在验证到 [!DNL Dynamics 365] CRM目标：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `Client ID` | 的 [!DNL Dynamics 365] 您的客户端ID [!DNL Azure Active Directory] 应用程序。 请参阅 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) 以获取指导。 | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | 的 [!DNL Dynamics 365] 您的客户端密钥 [!DNL Azure Active Directory] 应用程序。 您将在 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options). | `abcde~abcdefghijklmnopqrstuvwxyz12345678` 以获取指导。 |
| `Tenant ID` | 的 [!DNL Dynamics 365] 您的租户ID [!DNL Azure Active Directory] 应用程序。 请参阅 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) 以获取指导。 | `1234567-aaaa-12ab-ba21-1234567890` |
| `Environment URL` | 请参阅 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) 以获取指导。 | 如果 [!DNL Dynamics 365] 域如下所示，您需要突出显示的值。<br> *`org57771b33`.crm.dynamics.com* |

## 护栏 {#guardrails}

的 [请求限制和分配](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) 页面详细信息 [!DNL Dynamics 365] 与 [!DNL Dynamics 365] 许可证。 您需要确保数据和有效负载在这些限制内。

## 支持的身份 {#supported-identities}

[!DNL Dynamics 365] 支持更新下表所述的身份。 详细了解 [标识](/help/identity-service/namespaces.md).

| Target标识 | 示例 | 描述 | 注意事项 |
|---|---|---|---|
| `contactId` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | 联系人的唯一标识符。 | **必需**. 请参阅 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) 以了解更多详细信息。 |

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于用户档案]** | <ul><li>您正在导出区段的所有成员，以及所需的架构字段 *(例如：电子邮件地址、电话号码、姓氏)*，则会根据字段映射。</li><li> 每个区段状态位于 [!DNL Dynamics 365] 会根据 **[!UICONTROL 映射ID]** 值 [区段计划](#schedule-segment-export-example) 中。</li></ul> |
| 导出频度 | **[!UICONTROL 流]** | <ul><li>流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两节中列出的字段。

在 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 搜索 [!DNL Dynamics 365]. 或者，您也可以在 **[!UICONTROL CRM]** 类别。

### 对目标进行身份验证 {#authenticate}

要对目标进行身份验证，请选择 **[!UICONTROL 连接到目标]**.
![Platform UI屏幕截图，其中显示了如何进行身份验证。](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

填写以下必填字段。 请参阅 [收集Dynamics 365凭据](#gather-credentials) 部分。
* **[!UICONTROL 客户端ID]**:的 [!DNL Dynamics 365] 您的客户端ID [!DNL Azure Active Directory] 应用程序。
* **[!UICONTROL 租户ID]**:的 [!DNL Dynamics 365] 您的租户ID [!DNL Azure Active Directory] 应用程序。
* **[!UICONTROL 客户端密钥]**:的 [!DNL Dynamics 365] 您的客户端密钥 [!DNL Azure Active Directory] 应用程序。
* **[!UICONTROL 环境URL]**:您的 [!DNL Dynamics 365] 环境URL。

如果提供的详细信息有效，UI会显示 **[!UICONTROL 已连接]** 状态为绿色复选标记。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写以下必填和可选字段。 UI中字段旁边的星号表示该字段为必填字段。
![Platform UI屏幕截图，显示目标详细信息。](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

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

要将受众数据从Adobe Experience Platform正确发送到 [!DNL Dynamics 365] 目标，您需要完成字段映射步骤。 映射包括在Platform帐户中的体验数据模型(XDM)架构字段与目标目标中相应的对等字段之间创建一个链接。 要将XDM字段正确映射到 [!DNL Dynamics 365] 目标字段，请执行以下步骤：

1. 在 **[!UICONTROL 映射]** 步骤，选择 **[!UICONTROL 添加新映射]**. 您将在屏幕上看到一个新的映射行。
   ![Platform UI中“添加新映射”的屏幕截图示例。](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. 在 **[!UICONTROL 选择源字段]** 窗口，选择 **[!UICONTROL 选择身份命名空间]** 类别和选择 `contactId`.
   ![Platform UI源映射的屏幕截图示例。](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. 在 **[!UICONTROL 选择目标字段]** 窗口，选择要将源字段映射到的目标字段类型。
   * **[!UICONTROL 选择身份命名空间]**:选择此选项可将源字段从列表中映射到标识命名空间。
      ![Platform UI屏幕截图，其中显示了contactId的Target映射。](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * 在XDM配置文件架构和 [!DNL Dynamics 365] 实例： |XDM配置文件架构|[!DNL Dynamics 365] Instance|必填| |—|—|—| |`contactId`|`contactId`|是 |

   * **[!UICONTROL 选择自定义属性]**:选择此选项可将源字段映射到您在中定义的自定义属性 **[!UICONTROL 属性名称]** 字段。 请参阅 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) ，以获取受支持属性的完整列表。
      ![平台UI屏幕截图，其中显示了LastName的Target映射。](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-lastname.png)

      >[!IMPORTANT]
      >
      >如果您的日期或时间戳源字段映射到 [!DNL Dynamics 365] [日期或时间戳](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) 目标字段中，请确保映射的值不为空。 如果传递的值为空，您将会遇到 *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* 错误消息和数据将不会更新。 这是 [!DNL Dynamics 365] 限制。

   * 例如，根据要更新的值，在XDM配置文件架构和 [!DNL Dynamics 365] 实例： |XDM配置文件架构|[!DNL Dynamics 365] 实例| |—|—| |`person.name.firstName`|`FirstName`| |`person.name.lastName`|`LastName`| |`personalEmail.address`|`Email`|

   * 使用这些映射的示例如下所示：
      ![平台UI屏幕截图示例，其中显示了目标映射。](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### 计划区段导出和示例 {#schedule-segment-export-example}

在 [[!UICONTROL 计划区段导出]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 在激活工作流的步骤中，您必须手动将Platform区段映射到 [!DNL Dynamics 365].

为此，请选择每个区段，然后输入 [!DNL Dynamics 365] 在 **[!UICONTROL 映射ID]** 字段。

>[!IMPORTANT]
>
>用于 **[!UICONTROL 映射ID]** 应与 [!DNL Dynamics 365]. 请参阅 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) 如果您需要有关查找自定义字段属性的指导。

示例如下所示：
![Platform UI屏幕截图示例显示了计划区段导出。](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## 验证数据导出 {#exported-data}

要验证您是否已正确设置目标，请执行以下步骤：

1. 选择 **[!UICONTROL 目标]** > **[!UICONTROL 浏览]** 导航到目标列表。
   ![显示浏览目标的平台UI屏幕截图。](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. 选择目标并验证状态是否为 **[!UICONTROL 已启用]**.
   ![Platform UI屏幕截图，其中显示了目标数据流运行。](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. 切换到 **[!DNL Activation data]** ，然后选择区段名称。
   ![Platform UI屏幕截图示例，其中显示了目标激活数据。](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. 监控区段摘要，并确保配置文件计数与区段内创建的计数相对应。
   ![平台UI屏幕截图示例，其中显示了区段。](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. 登录到 [!DNL Dynamics 365] 网站，然后导航到 [!DNL Customers] > [!DNL Contacts] 页面，并检查是否已添加区段中的用户档案。 您可以在 [!DNL Dynamics 365] 更新时，会根据 **[!UICONTROL 映射ID]** 值 [区段计划](#schedule-segment-export-example) 中。
   ![Dynamics 365 UI屏幕截图显示了区段状态已更新的“联系人”页面。](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](/help/data-governance/home.md).

## 错误和疑难解答 {#errors-and-troubleshooting}

### 将事件推送到目标时遇到未知错误 {#unknown-errors}

检查数据流运行时，如果收到以下错误消息： `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![显示错误请求错误的平台UI屏幕截图。](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

要修复此错误，请验证 **[!UICONTROL 映射ID]** 您在 [!DNL Dynamics 365] ，且该区段在 [!DNL Dynamics 365].

## 其他资源 {#additional-resources}

来自 [[!DNL Dynamics 365] 文档](https://docs.microsoft.com/en-us/dynamics365/) 如下所示：
* [IOrganizationService.Update(Entity)方法](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [使用Web API更新和删除表行](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)