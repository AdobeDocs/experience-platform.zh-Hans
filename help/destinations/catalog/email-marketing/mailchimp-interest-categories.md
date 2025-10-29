---
title: Mailchimp兴趣类别
description: Mailchimp（也称为Intuit Mailchimp）是一种流行的营销自动化平台和电子邮件营销服务，企业使用它来管理联系人（客户、客户或其他利益相关方），并使用邮件列表和电子邮件营销活动与其交谈。 使用此连接器可以根据联系人的兴趣和偏好对他们进行排序。
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: bdce8295-7305-4d54-81c1-7fa3e580ce70
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 3%

---

# [!DNL Mailchimp Interest Categories]连接

[[!DNL Mailchimp]](https://mailchimp.com)是一种流行的营销自动化平台和电子邮件营销服务，企业使用它来管理联系人&#x200B;*（客户、客户或其他相关方）*，并使用邮件列表和电子邮件营销活动与其交谈。 使用此连接器可以根据联系人的兴趣和偏好对他们进行排序。

[!DNL Mailchimp Interest Categories]使用[受众](https://mailchimp.com/help/getting-started-audience/)、[组](https://mailchimp.com/help/getting-started-with-groups/)和兴趣类别&#x200B;*（也称为组名或组标题）*。 每个[!DNL Mailchimp]组都是感兴趣类别的列表。 当联系人通过您网站上的注册表单订阅一个或多个兴趣类别时，他们就会与兴趣类别相关联。 在受众中，您还可以将联系人组织到组中，并将其与兴趣类别关联，然后可以使用这些组来创建区段。 您可以使用这些受众向订阅的联系人广播定向的活动电子邮件。

<!--
Compared to [!DNL Mailchimp Tags] which you would use for internal classification, [!DNL Mailchimp Interest Categories] is meant to manage subscriptions to topics of interest that your contacts might be interested in. *Note, Experience Platform also has a connection for [!DNL Mailchimp Tags], you can check it out on the [[!DNL Mailchimp Tags]](/help/destinations/catalog/email-marketing/mailchimp-tags.md) page.*
-->

此[!DNL Adobe Experience Platform] [目标](/help/destinations/home.md)使用[[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) API创建[兴趣类别](https://mailchimp.com/developer/marketing/api/interest-categories/)，然后将每个选定Experience Platform受众的联系人添加到相应的兴趣类别中。 您可以&#x200B;**添加新联系人**&#x200B;或&#x200B;**更新现有[!DNL Mailchimp]联系人的信息**，然后在新区段中激活现有联系人&#x200B;**受众后，在所需群组**&#x200B;中添加或删除联系人[!DNL Mailchimp]。 [!DNL Mailchimp Interest Groups]在[!DNL Mailchimp]中将从Experience Platform中选择的受众名称用作兴趣类别。

## 用例 {#use-cases}

为了帮助您更好地了解您应如何以及何时使用[!DNL Mailchimp Interest Categories]目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 向营销活动的联系人发送电子邮件 {#use-case-send-emails}

一家体育用品网站的销售部希望向一连串自称对足球感兴趣的熟人广播一个基于电子邮件的营销活动。 联系人列表在从网站开发团队收到的数据导出中分批显示，因此需要对其进行跟踪。 团队识别现有[!DNL Mailchimp]受众，并开始构建Experience Platform受众，每个列表中的联系人都添加到这些受众中。 将这些受众发送给[!DNL Mailchimp Interest Categories]后，如果所选[!DNL Mailchimp]受众中不存在任何联系人，则会将这些联系人添加到具有联系人所属受众名称的组中。 如果[!DNL Mailchimp]受众或组中已存在任何联系人，则会更新其信息。 将数据发送到[!DNL Mailchimp Interest Categories]后，销售团队可以选择营销活动电子邮件并将其发送到[!DNL Mailchimp]受众中的足球兴趣组。

## 先决条件 {#prerequisites}

请参阅以下部分，了解需要在Experience Platform和[!DNL Mailchimp]中设置的任何先决条件，以及在使用[!DNL Mailchimp Interest Categories]目标之前必须收集的信息。

### Experience Platform中的先决条件 {#prerequisites-in-experience-platform}

在将数据激活到[!DNL Mailchimp Interest Categories]目标之前，您必须在[中创建一个](/help/xdm/schema/composition.md)架构[、](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)数据集[和](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)区段[!DNL Experience Platform]。

### [!DNL Mailchimp Interest Categories]目标的先决条件 {#prerequisites-destination}

请注意以下先决条件，以便将数据从Experience Platform导出到您的[!DNL Mailchimp]帐户：

#### 您必须拥有[!DNL Mailchimp]帐户 {#prerequisites-account}

在创建[!DNL Mailchimp Interest Categories]目标之前，您必须首先确保您拥有[!DNL Mailchimp]帐户。 如果您还没有帐户，请访问[[!DNL Mailchimp] 注册页面](https://login.mailchimp.com/signup/)以注册并创建帐户。

#### 收集[!DNL Mailchimp] API密钥 {#gather-credentials}

您需要您的[!DNL Mailchimp] **API密钥**&#x200B;来针对您的[!DNL Mailchimp Interest Categories]帐户验证[!DNL Mailchimp]目标。 当您&#x200B;**对目标**&#x200B;进行身份验证时，**API密钥**&#x200B;将用作[密码](#authenticate)。

如果您没有&#x200B;**API密钥**，请登录您的帐户并参阅[[!DNL Mailchimp] 生成API密钥](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key)文档以创建一个。

API密钥的示例为`0123456789abcdef0123456789abcde-us14`。

>[!IMPORTANT]
>
>如果您生成&#x200B;**API密钥**，请将其写下，因为生成后您将无法访问它。

#### 识别[!DNL Mailchimp]数据中心 {#identify-data-center}

接下来，您必须识别您的[!DNL Mailchimp]数据中心。 为此，请登录到您的[!DNL Mailchimp]帐户并导航到帐户的&#x200B;**API密钥部分**。

值是您在浏览器中看到的URL的第一部分。 如果URL是&#x200B;*https://`us14`.mailchimp.com/account/api/*，则数据中心是`us14`。

它还以&#x200B;*key-dc*&#x200B;的形式附加到API密钥；如果API密钥为`0123456789abcdef0123456789abcde-us14`，则数据中心为`us14`。

写下数据中心值&#x200B;*（在此示例中为`us14`）*，当您[填写目标详细信息](#destination-details)时需要此值。

如果需要进一步的指导，请参阅[[!DNL Mailchimp] 基础文档](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure)。

### 护栏 {#guardrails}

您的[!DNL Mailchimp]受众中每个受众最多可以包含60个组名（或兴趣类别），这些组名可以位于单个组中，也可以跨同一受众内的多个组。 有关所需的任何说明，请参阅[!DNL Mailchimp] [组](https://mailchimp.com/help/getting-started-with-groups/)。 达到此限制后，您会从`400 BAD_REQUEST Cannot have more than 60 interests per list (Across all categories)` API收到[!DNL Mailchimp]消息作为错误响应。

此外，有关[!DNL Mailchimp] API施加的限制的详细信息，请参阅[ ](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits)速率限制[!DNL Mailchimp]。

## 支持的身份 {#supported-identities}

[!DNL Mailchimp]支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 联系人电子邮件地址 | 必需 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Profile-based]** | <ul><li>您正在根据字段映射导出区段的所有成员，以及所需的架构字段&#x200B;*（例如：电子邮件地址、电话号码、姓氏）*。</li><li> 对于Experience Platform中的每个选定受众，相应的[!DNL Mailchimp Interest Categories]区段状态将从Experience Platform中更新为其受众状态。</li></ul> |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 当基于受众评估在Experience Platform中更新用户档案时，连接器会将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

在&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**&#x200B;内，搜索[!DNL Mailchimp Interest Categories]。 或者，您可以在&#x200B;**[!UICONTROL Email marketing]**&#x200B;类别下找到它。

### 验证目标 {#authenticate}

要验证目标，请填写下面的必填字段并选择&#x200B;**[!UICONTROL Connect to destination]**。

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL Username]** | 您的[!DNL Mailchimp Interest Categories]用户名。 |
| **[!UICONTROL Password]** | 您的[!DNL Mailchimp] **API密钥**，您已在[收集 [!DNL Mailchimp] 凭据](#gather-credentials)部分中记录该密钥。<br>您的API密钥采用`{KEY}-{DC}`的形式，其中`{KEY}`部分引用[[!DNL Mailchimp] API密钥](#gather-credentials)部分中记下的值，而`{DC}`部分引用[[!DNL Mailchimp] 数据中心](#identify-data-center)。 <br>您可以提供`{KEY}`部分或整个表单。<br>例如，如果您的API密钥是&#x200B;<br>*`0123456789abcdef0123456789abcde-us14`*，<br>，则可以提供&#x200B;*`0123456789abcdef0123456789abcde`*或&#x200B;*`0123456789abcdef0123456789abcde-us14`*作为值。 |

{style="table-layout:auto"}

![Experience Platform UI屏幕截图显示如何进行身份验证。](../../assets/catalog/email-marketing/mailchimp-interest-categories/authenticate-destination.png)

如果提供的详细信息有效，则UI会显示&#x200B;**[!UICONTROL Connected]**&#x200B;状态并显示绿色复选标记。 然后，您可以继续执行下一步。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![Experience Platform UI屏幕截图显示目标详细信息。](../../assets/catalog/email-marketing/mailchimp-interest-categories/destination-details.png)

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL Name]** | 将来用于识别此目标的名称。 |
| **[!UICONTROL Description]** | 可帮助您以后识别此目标的描述。 |
| **[!UICONTROL Data center]** | 您的[!DNL Mailchimp]帐户`data center`。 有关任何指导，请参阅[识别 [!DNL Mailchimp] 数据中心](#identify-data-center)部分。 |
| **[!UICONTROL Audience Name (Please select Data center first)]** | 选择您的&#x200B;**[!UICONTROL Data center]**&#x200B;后，此下拉列表中将自动填充您的[!DNL Mailchimp]帐户中的受众名称。 选择要使用Experience Platform中的数据更新的受众。 |
| **[!UICONTROL Interest Category (Please select Data center and Audience Name first)]** | 选择您的&#x200B;**[!UICONTROL Audience Name]**&#x200B;后，此下拉列表将自动填充您的[!DNL Mailchimp]帐户中的兴趣组类别名称。 选择要使用Experience Platform中的数据更新的类别名称。 |

{style="table-layout:auto"}

>[!TIP]
>
> 如果您在&#x200B;**[!UICONTROL Password]**&#x200B;字段中提供的API密钥或&#x200B;**[!UICONTROL Data center]**&#x200B;值不正确，则UI会显示[!DNL Mailchimp] API错误响应： *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`*，如下所示。 在这种情况下，您无法从&#x200B;**[!UICONTROL Audience Name (Please select Data center first)]**&#x200B;字段中选择值。 要修复此错误，请提供正确的值。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL Next]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请阅读[将配置文件和受众激活到流式受众导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md)。

### 映射注意事项和示例 {#mapping-considerations-example}

要将受众数据从Adobe Experience Platform正确发送到[!DNL Mailchimp Interest Categories]目标，您必须完成字段映射步骤。 映射包括在Experience Platform帐户中的Experience Data Model (XDM)架构字段与其与目标中的相应等效字段之间创建链接。

要将XDM字段正确映射到[!DNL Mailchimp Interest Categories]目标字段，请执行以下步骤：

1. 在&#x200B;**[!UICONTROL Mapping]**&#x200B;步骤中，选择&#x200B;**[!UICONTROL Add new mapping]**。 您现在可以在屏幕上看到新的映射行。
1. 在&#x200B;**[!UICONTROL Select source field]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL Select attributes]**&#x200B;类别并选择XDM属性或选择&#x200B;**[!UICONTROL Select identity namespace]**&#x200B;并选择身份。
1. 在&#x200B;**[!UICONTROL Select target field]**&#x200B;窗口中，选择&#x200B;**[!UICONTROL Select identity namespace]**&#x200B;并选择身份，或选择&#x200B;**[!UICONTROL Select attributes]**&#x200B;类别并从从[!DNL Mailchimp] API填充的属性列表中选择。 *您添加到选定[!DNL Mailchimp]受众的任何自定义属性也可用作目标字段进行选择。*

   XDM配置文件架构与[!DNL Mailchimp Interest Categories]之间的可用映射如下：

   | 源字段 | 目标字段 | 注释 |
   | --- | --- | --- |
   | `IdentityMap: Email` | `Identity: email` | 必需：是 |
   | `xdm: person.name.firstName` | `Attribute: FNAME` | |
   | `xdm: person.name.lastName` | `Attribute: LNAME` | |
   | `xdm: person.birthDayAndMonth` | `Attribute: BIRTHDAY` | |

   此外，`ADDRESS`是您`merge field`受众中称为[!DNL Mailchimp]的特殊目标字段。 [[!DNL Mailchimp] 文档](https://mailchimp.com/developer/marketing/docs/merge-fields/)将必需键定义为`addr1`、`city`、`state`和`zip`，并将可选键定义为`addr2`和`country`。 这些字段的值必须为字符串。 如果存在任何`ADDRESS`字段映射，则目标会将`ADDRESS`对象传递到[!DNL Mailchimp] API进行更新。 除国家/地区默认为`ADDRESS`外，任何未映射的`NULL`字段的值均默认为`US`。

   `ADDRESS`字段可用的映射如下：

   | 源字段 | 目标字段 |
   | --- | --- |
   | `xdm: workAddress.street1` | `Attribute: ADDRESS.addr1` |
   | `xdm: workAddress.street2` | `Attribute: ADDRESS.addr2` |
   | `xdm: workAddress.city` | `Attribute: ADDRESS.city` |
   | `xdm: workAddress.state` | `Attribute: ADDRESS.state` |
   | `xdm: workAddress.postalCode` | `Attribute: ADDRESS.zip` |
   | `xdm: workAddress.country` | `Attribute: ADDRESS.country` |

   例如，您希望使用联系人的现有地址字段`country`、`addr1`、`city`和`state`的值更新`zip`的值，即`132, My Street, Kingston`、`New York`、`New York`和`12401`。 要更新`country`，您必须传递更改&#x200B;*（如果有）*&#x200B;的现有值和国家/地区的新值。 因此，数据集中的值应为`132, My Street, Kingston`、`New York`、`New York`、`12401`和`US`。 为了重申，如果您仅传递`country`并且不提供`addr1`、`city`、`state`和`zip`的值，则这些值将被`NULL`覆盖。

   下面显示了具有已完成映射的示例：
   ![显示字段映射的Experience Platform UI屏幕快照示例。](../../assets/catalog/email-marketing/mailchimp-interest-categories/mappings.png)

完成提供目标连接的映射后，请选择&#x200B;**[!UICONTROL Next]**。

## 验证数据导出 {#exported-data}

要验证您是否正确设置了目标，请执行以下步骤：

* 登录到您的[[!DNL Mailchimp]](https://login.mailchimp.com/)帐户。 然后，导航到&#x200B;**[!DNL Audience]**&#x200B;页面。 接下来，展开&#x200B;**[!DNL Manage Contacts]**&#x200B;菜单并选择&#x200B;**[!DNL Groups]**。

![显示“受众”组页面的Mailchimp UI屏幕截图。](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups.png)

* 选择组，然后检查所选受众是否使用Experience Platform中的受众名称作为类别创建，该受众名称后面可能会跟有一个自动生成的后缀。
   * 此目标使用[[!DNL Mailchimp] 添加兴趣类别API](https://mailchimp.com/developer/marketing/api/interest-categories/add-interest-category/)使用所选区段的名称创建兴趣类别。 如果您创建新目标并再次激活相同的受众，[!DNL Mailchimp]将添加后缀以区分现有区段和新区段。
* 其电子邮件不在群组中的联系人将添加到新创建的群组中。
* 对于组中已存在的联系人，属性字段数据将更新，联系人将添加到新创建的类别中。

![显示“受众”组类别的Mailchimp UI屏幕截图。](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups-category.png)

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](/help/data-governance/home.md)。

## 错误和故障排除 {#errors-and-troubleshooting}

### 如果[!DNL Mailchimp] API密钥或数据中心值不正确，则会遇到错误 {#incorrect-credentials-error}

如果您在&#x200B;**[!UICONTROL Password]**&#x200B;字段中提供的API密钥或&#x200B;**[!UICONTROL Data center]**&#x200B;值不正确，则UI会显示[!DNL Mailchimp] API错误响应： *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`*，如下所示。 在这种情况下，您无法从&#x200B;**[!UICONTROL Audience Name (Please select Data center first)]**&#x200B;字段中选择值。

![如果Mailchimp API密钥或数据中心值不正确，则Experience Platform UI屏幕截图显示错误。](../../assets/catalog/email-marketing/mailchimp-interest-categories/error.png)

要修复此错误并继续进行下一步，您必须提供正确的值。 请参阅[识别 [!DNL Mailchimp] 数据中心](#identify-data-center)和
如果需要指导，请[收集 [!DNL Mailchimp] API密钥](#gather-credentials)部分。

### 如果超过[!DNL Mailchimp]组名称限制，则会遇到错误 {#group-name-limits-error}

创建目标时，您可能会收到以下错误消息： *`Cannot have more than 60 interests per list (Across all categories)`*&#x200B;或&#x200B;*`400 BAD_REQUEST`*。 如[护栏](#guardrails)部分所述，在单个组中或同一受众限制内的多个组中超过60个组名称（或兴趣类别）时，会发生这种情况。 要修复此错误，请确保在[!DNL Mailchimp]中未超出组名限制。

### [!DNL Mailchimp]状态和错误代码

请参阅[[!DNL Mailchimp] 错误页面](https://mailchimp.com/developer/marketing/docs/errors/)，获取包含说明的状态和错误代码的完整列表。

## 其他资源 {#additional-resources}

[!DNL Mailchimp]文档中的其他有用信息如下：

* [开始使用 [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [受众入门](https://mailchimp.com/help/getting-started-audience/)
* [创建受众](https://mailchimp.com/help/create-audience/)
* [组入门](https://mailchimp.com/help/getting-started-with-groups/)
* [新建受众组](https://mailchimp.com/help/create-new-audience-group/)
* [兴趣类别](https://mailchimp.com/developer/marketing/api/interest-categories/)
* [营销API](https://mailchimp.com/developer/marketing/api/)
