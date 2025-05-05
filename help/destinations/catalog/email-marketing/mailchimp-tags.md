---
title: Mailchimp标记
description: 通过Mailchimp标记目标，可导出帐户数据并在Mailchimp中激活以与联系人接洽。
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0f278ca8-4fcf-4c47-b538-9cffa45a3d90
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 2%

---

# [!DNL Mailchimp Tags]连接

[[!DNL Mailchimp]](https://mailchimp.com) *（也称为[!DNL Intuit Mailchimp]）*&#x200B;是一种流行的营销自动化平台和电子邮件营销服务，企业使用它来管理和联系联系人&#x200B;*（客户、客户或其他相关方）*，使用邮件列表和电子邮件营销活动。

[!DNL Mailchimp Tags]使用[受众](https://mailchimp.com/help/getting-started-audience/)和[标记](https://mailchimp.com/help/getting-started-tags/)管理您的联系信息。 标记是一些标签，您可以使用这些标签来组织联系人，并在[!DNL Mailchimp]中将其标记为内部分类。

与根据联系人的兴趣和偏好对联系人进行排序的[!DNL Mailchimp Interest Categories]相比，[!DNL Mailchimp Tags]用于管理您的联系人可能感兴趣的主题订阅。 *请注意，Experience Platform也具有[!DNL Mailchimp Interest Categories]的连接，您可以在[[!DNL Mailchimp Interest Categories]](/help/destinations/catalog/email-marketing/mailchimp-interest-categories.md)页面上将其签出。*

此[!DNL Adobe Experience Platform] [目标](/help/destinations/home.md)利用[[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/)终结点。 在激活现有[!DNL Mailchimp]受众中的现有[!DNL Mailchimp]联系人&#x200B;**后，您可以**&#x200B;添加新联系人&#x200B;**或**&#x200B;更新这些联系人的标记。 [!DNL Mailchimp Tags]使用从Experience Platform中选择的受众名称作为[!DNL Mailchimp]中的标记名称。

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL Mailchimp Tags]目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 向营销活动的联系人发送电子邮件 {#use-case-send-emails}

组织的销售部门希望向精心策划的联系人列表广播基于电子邮件的营销活动。 联系人列表是从不同的离线来源批量接收的，因此需要对其进行跟踪。 团队识别现有[!DNL Mailchimp]受众，并开始构建Experience Platform受众，每个列表中的联系人都添加到这些受众中。 将这些受众发送给[!DNL Mailchimp Tags]后，如果所选[!DNL Mailchimp]受众中不存在任何联系人，则会添加一个关联的标记，其中包含该联系人所属的受众名称。 如果[!DNL Mailchimp]受众中已存在任何联系人，则会添加一个包含该受众名称的新标记。 由于标签在[!DNL Mailchimp]中可见，脱机源很容易识别。 将数据发送到[!DNL Mailchimp]后，他们将营销活动电子邮件发送给受众。

## 先决条件 {#prerequisites}

请参阅以下部分，了解需要在Experience Platform和[!DNL Mailchimp]中设置的任何先决条件，以及在使用[!DNL Mailchimp Tags]目标之前需要收集的信息。

### Experience Platform中的先决条件 {#prerequisites-in-experience-platform}

在将数据激活到[!DNL Mailchimp Tags]目标之前，您必须在[!DNL Experience Platform]中创建一个[架构](/help/xdm/schema/composition.md)、[数据集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=zh-Hans)和[受众](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html?lang=zh-Hans)。

### [!DNL Mailchimp Tags]目标的先决条件 {#prerequisites-destination}

请注意以下先决条件，以便将数据从Experience Platform导出到您的[!DNL Mailchimp Tags]帐户：

#### 您需要拥有[!DNL Mailchimp]帐户 {#prerequisites-account}

在创建[!DNL Mailchimp Tags]目标之前，您必须首先确保您拥有[!DNL Mailchimp]帐户。 如果您还没有用户访问[[!DNL Mailchimp] 注册页面](https://login.mailchimp.com/signup/)来注册和创建您的帐户。

#### 收集[!DNL Mailchimp] API密钥 {#gather-credentials}

您需要您的[!DNL Mailchimp] **API密钥**&#x200B;来针对您的[!DNL Mailchimp]帐户验证[!DNL Mailchimp Interest Categories]目标。 当您[对目标](#authenticate)进行身份验证时，**API密钥**&#x200B;将用作&#x200B;**密码**。

如果您没有&#x200B;**API密钥**，请登录您的[!DNL Mailchimp]帐户，并参阅[!DNL Mailchimp]文档，了解如何生成[API密钥](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key)。

API密钥的示例为`0123456789abcdef0123456789abcde-us14`。

>[!IMPORTANT]
>
>如果您生成&#x200B;**API密钥**，请将其写下，因为生成后您将无法访问它。

#### 识别您的[!DNL Mailchimp]数据中心 {#identify-data-center}

接下来，您必须识别您的[!DNL Mailchimp]数据中心。 为此，请登录到您的[!DNL Mailchimp]帐户并导航到帐户的&#x200B;**API密钥部分**。

数据中心ID是您在浏览器中看到的URL的第一部分。 如果URL是&#x200B;*https://`us14`.mailchimp.com/account/api/*，则数据中心是`us14`。

数据中心ID还以&#x200B;*key-dc*&#x200B;的形式附加到API密钥中；例如，如果API密钥为`0123456789abcdef0123456789abcde-us14`，则数据中心为`us14`。

写下数据中心值&#x200B;*（在此示例中为`us14`）*。 当您[填写目标详细信息](#destination-details)时，您将需要此值。

如果需要进一步的指导，请参阅[[!DNL Mailchimp] 基础文档](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure)。

### 护栏 {#guardrails}

有关[!DNL Mailchimp] API施加的限制的详细信息，请参阅[!DNL Mailchimp] [速率限制](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits)。

## 支持的身份 {#supported-identities}

[!DNL Mailchimp]支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 联系人的电子邮件地址。 | 必需 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 基于配置文件]** | <ul><li>您正在导出受众的所有成员，以及所需的架构字段&#x200B;*（例如：电子邮件地址、电话号码、姓氏）*（根据字段映射）。</li><li> 对于在Experience Platform中选择的每个受众，相应的[!DNL Mailchimp Tags]区段状态将通过Experience Platform中的受众状态进行更新。</li></ul> |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

在&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**&#x200B;中，搜索[!DNL Mailchimp Tags]。 或者，您可以在&#x200B;**[!UICONTROL 电子邮件营销]**&#x200B;类别下找到它。

### 验证目标 {#authenticate}

要验证到目标，请填写下面的必填字段，然后选择&#x200B;**[!UICONTROL 连接到目标]**。

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL 用户名]** | 您的[!DNL Mailchimp]用户名。 |
| **[!UICONTROL 密码]** | 您的[!DNL Mailchimp] **API密钥**，您已在[收集 [!DNL Mailchimp] 凭据](#gather-credentials)部分中记录该密钥。<br>您的API密钥采用`{KEY}-{DC}`的形式，其中`{KEY}`部分引用[[!DNL Mailchimp] API密钥](#gather-credentials)部分中记下的值，而`{DC}`部分引用[[!DNL Mailchimp] 数据中心](#identify-data-center)。 <br>您可以提供`{KEY}`部分或整个表单。<br>例如，如果您的API密钥是&#x200B;<br>*`0123456789abcdef0123456789abcde-us14`*，<br>，则可以提供&#x200B;*`0123456789abcdef0123456789abcde`*或&#x200B;*`0123456789abcdef0123456789abcde-us14`*作为值。 |

{style="table-layout:auto"}

![Experience Platform UI屏幕截图显示如何进行身份验证。](../../assets/catalog/email-marketing/mailchimp-tags/authenticate-destination.png)

如果提供的详细信息有效，则UI会显示&#x200B;**[!UICONTROL 已连接]**&#x200B;状态，并带有绿色复选标记。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![Experience Platform UI屏幕截图显示目标详细信息。](../../assets/catalog/email-marketing/mailchimp-tags/destination-details.png)

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 将来用于识别此目标的名称。 |
| **[!UICONTROL 描述]** | 可帮助您以后识别此目标的描述。 |
| **[!UICONTROL 数据中心]** | 您的[!DNL Mailchimp]帐户`data center`。 有关任何指导，请参阅[识别 [!DNL Mailchimp] 数据中心](#identify-data-center)部分。 |
| **[!UICONTROL 受众名称（请先输入数据中心）]** | 输入&#x200B;**[!UICONTROL 数据中心]**&#x200B;后，此下拉列表将自动填充[!DNL Mailchimp]帐户中的受众名称。 选择要使用Experience Platform中的数据更新的受众。 |

{style="table-layout:auto"}

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将受众激活到流式目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射注意事项和示例 {#mapping-considerations-example}

要将受众数据从Adobe Experience Platform正确发送到[!DNL Mailchimp Tags]目标，您需要完成字段映射步骤。 映射包括在Experience Platform帐户中的Experience Data Model (XDM)架构字段与其与目标中的相应等效字段之间创建链接。

要将XDM字段正确映射到[!DNL Mailchimp Tags]目标字段，请执行以下步骤：

1. 在&#x200B;**[!UICONTROL 映射]**&#x200B;步骤中，选择&#x200B;**[!UICONTROL 添加新映射]**。 您将在屏幕上看到一个新映射行。
1. 在&#x200B;**[!UICONTROL 选择源字段]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL 选择身份命名空间]**&#x200B;并选择`Email`身份命名空间。

   ![Experience Platform UI屏幕截图，其中Source字段为来自身份命名空间的电子邮件。](../../assets/catalog/email-marketing/mailchimp-tags/source-field.png)

1. 在&#x200B;**[!UICONTROL 选择目标字段]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL 选择身份命名空间]**&#x200B;并选择`Email`身份命名空间。

   ![Experience Platform UI屏幕截图，其中Target字段为来自身份命名空间的电子邮件。](../../assets/catalog/email-marketing/mailchimp-tags/target-field.png)

   XDM配置文件架构与[!DNL Mailchimp Tags]之间的映射将如下所示：

   | 源字段 | 目标字段 | 必需 |
   | --- | --- | --- |
   | `IdentityMap: Email` | `Identity: Email` | 是 |

   下面显示了具有已完成映射的示例：
   ![显示字段映射的Experience Platform UI屏幕快照示例。](../../assets/catalog/email-marketing/mailchimp-tags/mappings.png)

完成提供目标连接的映射后，请选择&#x200B;**[!UICONTROL 下一步]**。

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

1. 登录到您的[[!DNL Mailchimp]](https://login.mailchimp.com/)帐户。 然后导航到&#x200B;**[!DNL Audience]** > **[!DNL All Contacts]**&#x200B;页面，并检查受众中的联系人是否已添加以及受众中的联系人是否已使用受众名称进行更新。
   ![显示“受众”页面的Mailchimp UI屏幕截图。](../../assets/catalog/email-marketing/mailchimp-tags/contacts.png)

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。

## 错误和故障排除 {#errors-and-troubleshooting}

请参阅[[!DNL Mailchimp] 错误页面](https://mailchimp.com/developer/marketing/docs/errors/)，获取包含说明的状态和错误代码的完整列表。

## 其他资源 {#additional-resources}

[!DNL Mailchimp]文档中的其他有用信息如下：
* [开始使用 [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [受众入门](https://mailchimp.com/help/getting-started-audience/)
* [创建受众](https://mailchimp.com/help/create-audience/)
* [标记快速入门](https://mailchimp.com/help/getting-started-tags/)
* [营销API](https://mailchimp.com/developer/marketing/api/)
