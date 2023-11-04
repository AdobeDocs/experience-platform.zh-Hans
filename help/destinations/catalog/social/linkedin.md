---
keywords: linkedin连接；linkedin连接；linkedin目标；linkedin；
title: Linkedin匹配的受众连接
description: 基于哈希电子邮件激活LinkedIn营销活动的配置文件，以实现受众定位、个性化和抑制。
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 4%

---

# [!DNL LinkedIn Matched Audiences] 连接

## 概述 {#overview}

激活您的配置文件 [!DNL LinkedIn] 基于哈希电子邮件和移动ID的受众定位、个性化和抑制的营销活动。

![Adobe Experience Platform UI中的LinkedIn目标](../../assets/catalog/social/linkedin/catalog.png)

## 用例

为了帮助您更好地了解如何以及何时使用 [!DNL LinkedIn Matched Audiences] 目标，以下是Adobe Experience Platform客户可以使用此功能解决的用例。

一家软件公司组织了一次会议，并希望与与会者保持联系，并根据他们的会议出席情况向他们显示个性化的优惠。 公司可以从自己的电子邮件地址或移动设备ID中摄取 [!DNL CRM] 到Adobe Experience Platform。 然后，他们可以根据自己的离线数据构建受众，并将这些受众发送到 [!DNL LinkedIn] 社交平台，优化广告支出。

## 支持的身份 {#supported-identities}

[!DNL LinkedIn Matched Audiences] 支持激活下表中描述的标识。 了解有关 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google广告ID | 当源身份是GAID命名空间时，请选择此目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，请选择此目标身份。 |
| email_lc_sha256 | 使用SHA256算法进行哈希处理的电子邮件地址 | Adobe Experience Platform支持纯文本和SHA256哈希电子邮件地址。 请按照 [ID匹配要求](#id-matching-requirements-id-matching-requirements) 部分，并分别为纯文本和经过哈希处理的电子邮件使用相应的命名空间。 当源字段包含未哈希处理的属性时，请检查 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 受支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正使用 [!DNL LinkedIn Matched Audiences] 目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## linkedIn帐户先决条件 {#LinkedIn-account-prerequisites}

在使用 [!UICONTROL linkedIn匹配的受众] 目标，确保 [!DNL LinkedIn Campaign Manager] 帐户具有 [!DNL Creative Manager] 权限级别或更高。

要了解如何编辑您的 [!DNL LinkedIn Campaign Manager] 用户权限，请参阅 [添加、编辑和删除广告帐户的用户权限](https://www.linkedin.com/help/lms/answer/5753) 请参阅LinkedIn文档。

## ID匹配要求 {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] 要求不发送明确的个人身份信息(PII)。 因此，受众激活到 [!DNL LinkedIn Matched Audiences] 可以中断连接 *哈希* 标识符，例如电子邮件地址或移动设备ID。

根据您摄取到Adobe Experience Platform中的ID类型，您必须遵守其相应的要求。

## 电子邮件哈希处理要求 {#email-hashing-requirements}

您可以在将电子邮件地址摄取到Adobe Experience Platform之前对其进行哈希处理，或者在Experience Platform中使用清晰的电子邮件地址，并且您可以 [!DNL Platform] 激活时对其进行哈希处理。

要了解如何在Experience Platform中引入电子邮件地址，请参阅 [批量摄取概述](/help/ingestion/batch-ingestion/overview.md) 和 [流式摄取概述](/help/ingestion/streaming-ingestion/overview.md).

如果选择自己对电子邮件地址进行哈希处理，请确保符合以下要求：

* 修剪电子邮件字符串中的所有前导空格和尾随空格。 例如： `johndoe@example.com`，不是 `<space>johndoe@example.com<space>`；
* 在对电子邮件字符串进行哈希处理时，请确保对小写字符串进行哈希处理；
   * 示例： `example@email.com`，不是 `EXAMPLE@EMAIL.COM`；
* 确保散列字符串全部为小写
   * 示例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，不是 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`；
* 不要把字串加盐。

>[!NOTE]
>
>来自未经过哈希处理的命名空间的数据自动进行哈希处理 [!DNL Platform] 激活时。
> 属性源数据不会自动进行哈希处理。
> 
> 时段 [标识映射](../../ui/activate-segment-streaming-destinations.md#mapping) 步骤，当源字段包含未散列属性时，选中 **[!UICONTROL 应用转换]** 选项，拥有 [!DNL Platform] 在激活时自动散列数据。
> 
> 此 **[!UICONTROL 应用转换]** 选项仅在选择属性作为源字段时显示。 当您选择命名空间时，它不会显示。

![标识映射转换](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 连接到目标 {#connect}

>[!IMPORTANT]
> 
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

以下视频还演示了配置 [!DNL LinkedIn Matched Audiences] 目标和激活受众。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform用户界面经常更新，自从录制此视频以来，该界面可能已发生更改。 有关最新信息，请参阅 [目标配置教程](../../ui/connect-destination.md).

### 验证目标 {#authenticate}

1. 查找 [!DNL LinkedIn Matched Audiences] 目标目录中的目标并选择 **[!UICONTROL 设置]**.
2. 选择 **[!UICONTROL 连接到目标]**.
   ![对LinkedIn进行身份验证](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. 输入您的LinkedIn凭据并选择 **登录**.

### 填写目标详细信息 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="帐户 ID"
>abstract="您的 LinkedIn Campaign 管理器帐户 ID。您可以在 LinkedIn Campaign 管理器帐户中找到此 ID。"

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 帐户ID]**：您的 [!DNL LinkedIn Campaign Manager Account ID]. 您可以在您的网站中找到此ID [!DNL LinkedIn Campaign Manager] 帐户。

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 激活此目标的受众 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

请参阅 [将受众数据激活到流式受众导出目标](../../ui/activate-segment-streaming-destinations.md) 有关将受众激活到此目标的说明。

## 导出的数据 {#exported-data}

成功激活意味着 [!DNL LinkedIn] 自定义受众将以编程方式创建于 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). 由于用户符合或不符合激活受众的资格，因此将添加和删除受众成员资格。

>[!TIP]
>
>Adobe Experience Platform与之间的集成 [!DNL LinkedIn Matched Audiences] 支持历史受众回填。 所有历史受众资格都将被发送到 [!DNL LinkedIn] 将受众激活到目标时。
