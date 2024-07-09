---
title: Magnite流实时目标连接
description: 使用此目标可将AdobeCDP受众实时交付到Magnite流平台。
badgeBeta: label="Beta 版" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 1%

---


# (Beta) Magnite流：实时目标连接

## 概述 {#overview}

此 [!DNL Magnite Streaming: Real-Time] 和Magnite Streaming：Adobe Experience Platform中的批量目标可帮助您映射和导出受众，以便在Magnite Streaming平台上定位和激活。

将受众激活到 [!DNL Magnite Streaming] 平台是一个两步流程，需要您同时使用Magnite Streaming： Real-Time和Magnite Streaming： Batch目标。

要将受众激活到 [!DNL Magnite Streaming]，您必须：

* 激活上的受众 [!DNL Magnite Streaming: Real-Time] 目标，如本页所示。
* 在Magnite流：批处理目标上激活相同受众。 此 [!DNL Magnite Streaming: Batch] 目标为必需组件。 无法激活上的受众 [!DNL Magnite Streaming] 批处理目标将导致集成失败，并且不会激活您的受众。

注意：使用实时目标时， [!DNL Magnite: Streaming] 将实时接收受众，但我们只能暂时将实时受众存储在我们的平台中，并且这些受众将在几天内从我们的系统中删除。 因此，如果您要使用Magnite：流实时目标，您将 *另外* 需要使用Magnite流：批处理目标 — 您激活到实时目标的每个受众，还需要激活到批处理目标。

>[!IMPORTANT]
>
>此目标连接器为测试版，仅向部分客户提供。 要请求获取访问权限，请联系您的Adobe代表。
>
>目标连接器和文档页面由创建和维护 [!DNL Magnite] 团队。 如有任何查询或更新请求，请直接通过以下电子邮件联系他们： `adobe-tech@magnite.com`.

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用 [!DNL Magnite Streaming: Real-Time] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 激活和定位 {#activation-and-targeting}

与Magnite的这种集成允许客户将其CDP受众从Adobe Experience Platform传递到Magnite以进行广告定位。 可在Magnite中选择正确定位和负确定位（抑制）的受众。

## 先决条件 {#prerequisites}

要使用 [!DNL Magnite] Adobe Experience Platform中的目标，您必须首先拥有 [!DNL Magnite Streaming] 帐户。 如果您拥有 [!DNL Magnite Streaming] 帐户，请联系您的 [!DNL Magnite] 要提供凭据以访问的帐户管理员 [!DNL Magnite's] 目标。
如果您没有 [!DNL Magnite Streaming] 帐户，请联系adobe-tech@magnite.com

## 支持的身份 {#supported-identities}

此 [!DNL Magnite Streaming: Real-Time] 目标支持激活下表中描述的标识。 了解有关 [身份](/help/identity-service/features/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
|-------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| device_id | 设备或身份的唯一标识符。 我们接受任何设备ID和第一方ID，而不管类型如何。 | 我们支持的身份类型包括但不限于PPUID、GAID、IDFA和电视设备ID。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 支持 | 描述 |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ {\f13 } | 受众 [已导入](../../../segmentation/ui/audience-portal.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您正在导出区段（受众）的所有成员以及中使用的标识符（姓名、电话号码或其他）。 [!DNL Magnite Streaming: Real-Time] 目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据区段评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 查看目标]** 和 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在配置目标工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

![目标配置身份验证字段未填写](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-unfilled.png)

* **[!UICONTROL 用户名]**：由向您提供的用户名 [!DNL Magnite].
* **[!UICONTROL 密码]**：为您提供的密码，由 [!DNL Magnite].

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
* **[!UICONTROL 您的源合作伙伴的名称]**：您的客户/公司名称。 仅受支持 [!DNL Magnite Streaming] 客户端可供选择。

![目标配置身份验证字段已填写](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-filled.png)

完成后，选择 **[!UICONTROL 创建]** 按钮。

![可选的治理策略和实施行动](../../assets/catalog/advertising/magnite/destination-realtime-config-grouping-policy.png)

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
>
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将配置文件和区段激活到流式区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

创建目标连接后，您可以进入受众激活流程。 以下部分将介绍如何使用实时目标激活受众。

### 映射属性和身份 {#map}

下一步是将源标识符映射到Magnite device_id标识符。

* 您可以通过选择来添加所需数量的映射 **[!UICONTROL 添加新映射]**.

此使用实时目标的示例显示了一行，该行包含映射到Magnite device_id目标字段的通用deviceId源标识符。 使用映射时，选择 [!UICONTROL 下一个].

![将所需的数据字段映射到device_ID字段](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-field-mapping.png)

请确保将映射ID设置为所有激活的受众，如果没有映射ID，则设置为“无”。

![请确保将映射ID设置为所有激活的受众，如果没有映射ID，则设置为“无”](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-mappingid.png)

您现在必须为每个受众配置开始日期（必需）、结束日期（可选）和映射ID。

**映射Id**

* 使用 **[!UICONTROL 映射Id]** 当受众具有Magnite以前已知的预先存在的区段ID时的字段。

* 添加 **[!UICONTROL 映射Id]** 对于某个受众，请分别选择每个受众行，然后在右侧列中输入数据（请参阅上图）。 如果您不想添加映射ID，请在映射ID字段中输入NONE。

选择 **[!UICONTROL 下一个]** 并最终确定激活流程。

![选择下一步并完成激活流程。](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-review.png)

## 导出的数据/验证数据导出 {#exported-data}

上传受众后，您可以使用以下步骤验证受众是否已正确创建和上传：

<!--

* In 95% of cases, audiences will be delivered to Magnite Streaming in under 10 minutes. The actual receipt and processing of the events within Magnite Streaming depends on the shared data volume.

-->

* 在Post摄取中，受众应显示在 [!DNL Magnite Streaming] 几分钟内，并且可以应用于交易。 您可以通过查找在Adobe Experience Platform中的激活步骤中共享的区段ID来确认这一点。

## 通过激活相同的受众 [!DNL Magnite Streaming: Batch]目标

受众共享对象 [!DNL Magnite Streaming] 还需要使用Magnite Streaming：批处理目标共享使用实时目标。 正确配置后，中的区段名称 [!DNL Magnite Streaming] UI将进行更新，以反映Adobe Experience Platform每日更新后使用的那些。

最后，如果尚未为您的集成配置批处理目标，请立即通过Magnite Streaming：批处理目标文档进行设置。

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

有关其他帮助文档，请访问 [菱镁矿帮助中心](https://help.magnite.com/help).
