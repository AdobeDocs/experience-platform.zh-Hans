---
keywords: linkedin连接；linkedin连接；linkedin目标；linkedin；
title: Linkedin匹配的受众连接
description: 根据散列电子邮件，激活LinkedIn营销活动的用户档案，以实现受众定位、个性化和抑制。
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 6b3b830f822cc02c78d6f593c0a949d3e19ada37
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 5%

---

# [!DNL LinkedIn Matched Audiences]连接

## 概述 {#overview}

根据散列电子邮件和移动ID，激活[!DNL LinkedIn]营销活动的配置文件，以实现受众定位、个性化和抑制。

Adobe Experience Platform UI中的![LinkedIn目标](../../assets/catalog/social/linkedin/catalog.png)

## 用例

为了帮助您更好地了解如何以及何时使用[!DNL LinkedIn Matched Audiences]目标，以下是Adobe Experience Platform客户可以使用此功能解决的用例。

一家软件公司组织了一次会议，并希望与与会者保持联系，并根据他们的会议出席情况向他们显示个性化的优惠。 公司可以将电子邮件地址或移动设备ID从自己的[!DNL CRM]摄取到Adobe Experience Platform中。 然后，他们可以从自己的离线数据构建受众，并将这些受众发送到[!DNL LinkedIn]社交平台，优化其广告支出。

## 支持的身份 {#supported-identities}

[!DNL LinkedIn Matched Audiences]支持激活下表中描述的标识。 了解有关[标识](/help/identity-service/features/namespaces.md)的更多信息。

>[!IMPORTANT]
>
>从2025年9月开始，您无法再将[!DNL IDFA]映射为目标标识，因为[!DNL IDFA]目标不再支持[!DNL LinkedIn Matched Audiences]。 有关详细信息，请参阅[!DNL LinkedIn Matched Audiences]集成[文档](https://learn.microsoft.com/en-us/linkedin/marketing/matched-audiences/create-and-manage-segment-users?view=li-lms-2025-07&tabs=http#idtypes)。 此更改是由于LinkedIn的要求而做出的，与任何Experience Platform目标服务升级无关。


| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 当源身份是GAID命名空间时，请选择此目标身份。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 请按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的说明进行操作，分别使用适当的命名空间处理纯文本和经过哈希处理的电子邮件。 当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以使[!DNL Experience Platform]在激活时自动对数据进行哈希处理。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 自定义上传 | ✓ | 受众[已从CSV文件将](../../../segmentation/ui/audience-portal.md#import-audience)导入Experience Platform。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出具有[!DNL LinkedIn Matched Audiences]目标中使用的标识符（姓名、电话号码等）的受众的所有成员。 |
| 导出频率 | **[!UICONTROL 正在流式传输]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## LinkedIn帐户先决条件 {#LinkedIn-account-prerequisites}

在使用[!UICONTROL LinkedIn匹配的受众]目标之前，请确保您的[!DNL LinkedIn Campaign Manager]帐户具有[!DNL Creative Manager]权限级别或更高。

要了解如何编辑您的[!DNL LinkedIn Campaign Manager]用户权限，请参阅LinkedIn文档中的[添加、编辑和删除Advertising帐户的用户权限](https://www.linkedin.com/help/lms/answer/5753)。

## ID匹配要求 {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences]要求不发送明确的个人身份信息(PII)。 因此，激活到[!DNL LinkedIn Matched Audiences]的受众可以脱离&#x200B;*哈希*&#x200B;标识符，例如电子邮件地址或移动设备ID。

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵守其相应的要求。

## 电子邮件哈希处理要求 {#email-hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform之前对其进行哈希处理，或者在Experience Platform中明确使用电子邮件地址，并在激活时对其进行[!DNL Experience Platform]哈希处理。

要了解如何在Experience Platform中摄取电子邮件地址，请参阅[批次摄取概述](/help/ingestion/batch-ingestion/overview.md)和[流式摄取概述](/help/ingestion/streaming-ingestion/overview.md)。

如果选择自己对电子邮件地址进行哈希处理，请确保符合以下要求：

* 修剪电子邮件字符串中的所有前导空格和尾随空格。 例如： `johndoe@example.com`，而不是`<space>johndoe@example.com<space>`；
* 在对电子邮件字符串进行哈希处理时，请确保对小写字符串进行哈希处理；
   * 示例： `example@email.com`，而不是`EXAMPLE@EMAIL.COM`；
* 确保散列字符串全部为小写
   * 示例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，而不是`55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`；
* 不要把字串加盐。

>[!NOTE]
>
>来自未经过哈希处理的命名空间的数据在激活时会由[!DNL Experience Platform]自动进行哈希处理。
>&#x200B;> 属性源数据不会自动进行哈希处理。
> 
> 在[标识映射](../../ui/activate-segment-streaming-destinations.md#mapping)步骤中，当源字段包含未哈希处理的属性时，请选中&#x200B;**[!UICONTROL 应用转换]**&#x200B;选项，以便在激活时让[!DNL Experience Platform]自动对数据进行哈希处理。
> 
> **[!UICONTROL 应用转换]**&#x200B;选项仅在您选择属性作为源字段时显示。 当您选择命名空间时，它不会显示。

![标识映射转换](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>若要连接到目标，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。 在配置目标工作流中，填写下面两个部分中列出的字段。

以下视频还演示了配置[!DNL LinkedIn Matched Audiences]目标和激活受众的步骤。

>[!VIDEO](https://video.tv.adobe.com/v/3411783/?quality=12&learn=on&captions=chi_hans)

>[!NOTE]
>
>Experience Platform用户界面经常更新，自从录制此视频以来，可能已经发生了变化。 有关最新信息，请参阅[目标配置教程](../../ui/connect-destination.md)。

### 验证目标 {#authenticate}

1. 在目标目录中找到[!DNL LinkedIn Matched Audiences]目标并选择&#x200B;**[!UICONTROL 设置]**。
2. 选择&#x200B;**[!UICONTROL 连接到目标]**。
   ![对LinkedIn进行身份验证](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. 输入您的LinkedIn凭据并选择&#x200B;**登录**。

### 刷新身份验证凭据 {#refresh-authentication-credentials}

LinkedIn令牌每60天过期一次。 您可以从&#x200B;**[[!UICONTROL 帐户]](../../ui/destinations-workspace.md#accounts)**&#x200B;或&#x200B;**[[!UICONTROL 浏览]](../../ui/destinations-workspace.md#browse)**&#x200B;选项卡中的&#x200B;**[!UICONTROL 帐户到期日期]**&#x200B;列监控您的令牌到期日期。

令牌过期后，数据导出到目标的操作将停止。 要防止出现这种情况，请执行以下步骤以重新进行身份验证：

1. 导航到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 帐户]**
2. （可选）使用页面上的可用过滤器以仅显示LinkedIn帐户。
   ![筛选以仅显示LinkedIn帐户](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-filters.png)
3. 选择要刷新的帐户，选择省略号并选择&#x200B;**[!UICONTROL 编辑详细信息]**。
   ![选择“编辑详细信息”控件](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-edit-details.png)
4. 在模式窗口中，选择&#x200B;**[!UICONTROL 重新连接OAuth]**&#x200B;并使用您的LinkedIn凭据重新进行身份验证。
   使用Reconnect OAuth选项的![模式窗口](/help/destinations/assets/catalog/social/linkedin/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>您的身份验证凭据已刷新，其过期时间将重置为60天。

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="帐户 ID"
>abstract="您的 LinkedIn Campaign 管理器帐户 ID。您可以在 LinkedIn Campaign 管理器帐户中找到此 ID。"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：您的[!DNL LinkedIn Campaign Manager Account ID]。 您可以在您的[!DNL LinkedIn Campaign Manager]帐户中找到此ID。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅目标警报的指南](../../ui/alerts.md)。

完成提供目标连接的详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。
>* 要导出&#x200B;*标识*，您需要&#x200B;**[!UICONTROL 查看标识图形]** [访问控制权限](/help/access-control/home.md#permissions)。<br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

有关将受众激活到此目标的说明，请参阅[将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md)。

## 导出的数据 {#exported-data}

成功激活意味着[!DNL LinkedIn]自定义受众是在[[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login)中以编程方式创建的。 当用户在激活的受众中符合资格或被取消资格时，会调整受众成员资格。

>[!TIP]
>
>Adobe Experience Platform与[!DNL LinkedIn Matched Audiences]之间的集成支持历史受众回填。 在将受众激活到目标时，所有历史受众资格都会发送到[!DNL LinkedIn]。
