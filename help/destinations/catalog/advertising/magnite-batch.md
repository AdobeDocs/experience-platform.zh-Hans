---
title: 菱形流批处理目标
description: 使用此目标可将AdobeCDP受众批量交付到Magnite流平台。
badgeBeta: label="Beta 版" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 1%

---


# 菱形流：批量连接 {#magnite-streaming-batch}

## 概述 {#overview}

本文档介绍了Magnite流：批量目标，并提供了示例用例，以帮助您更好地了解如何激活受众并将其导出到其中。

Adobe Real-Time CDP受众可以通过两种方式交付到Magnite：流式平台 — 它们可以每天交付一次，也可以实时交付：

1. 如果您每天只需和/或需要交付受众一次，则可以使用Magnite：流式批处理目标，该目标通过每日S3批处理文件交付将受众交付给Magnite：流式处理。 这些批量受众会无限期地存储在我们的平台中，这与仅存储两天的实时受众不同。

2. 但是，如果您希望和/或需要实时交付受众，则需要使用Magnite：流式实时目标。 在使用实时目标时，Magnite：流将实时接收受众，但我们只能暂时在我们的平台中存储实时受众，并且这些受众将在几天内从我们的系统中删除。 因此，如果您要使用Magnite：流式实时目标，您还需要使用Magnite：流式批处理目标 — 您激活到实时目标的每个受众，还需要激活到批处理目标。

回顾：如果您每天只想交付一次Adobe Real-Time CDP受众，您将只使用Magnite：流式批处理目标，并且每天将交付一次受众。 如果要实时交付Adobe Real-Time CDP受众，您将同时使用Magnite：流式批处理目标和Magnite：流式实时目标。 有关更多信息，请联系Magnite：流。


请继续阅读下文，了解有关Magnite：流式批处理目标、如何连接到该目标以及如何为其激活Adobe Real-Time CDP受众的更多信息。
有关实时目标的详细信息，请参阅 [本文档](magnite-streaming.md) 而是。

>[!IMPORTANT]
>
>此目标连接器为测试版，仅向部分客户提供。 要请求获取访问权限，请联系您的Adobe代表。
>
>目标连接器和文档页面由创建和维护 [!DNL Magnite] 团队。 如有任何查询或更新请求，请直接通过以下电子邮件联系他们： `adobe-tech@magnite.com`.

## 用例 {#use-cases}

为了帮助您更好地了解应如何以及何时使用Magnite流：批处理目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 用例#1 {#use-case-1}

您已在Magnite Streaming：实时目标上激活受众。

任何通过Magnite流：实时目标激活的受众还必须使用Magnite流：批量目标，因为批量交付的数据旨在替换/保留Magnite流平台中的实时交付数据。

### 用例#2 {#use-case-2}

您只想在Magnite流平台中以批量/每日节奏激活受众。

通过Magnite流激活的任何受众：批次目标将以批处理/每日节奏交付，然后可以在Magnite流平台中定位。

## 先决条件 {#prerequisites}

要在Adobe Experience Platform中使用Magnite目标，您必须首先拥有Magnite流帐户。 如果您拥有 [!DNL Magnite Streaming] 帐户，请联系您的 [!DNL Magnite] 要提供凭据以访问的帐户管理员 [!DNL Magnite's] 目标。 如果您没有 [!DNL Magnite Streaming] 帐户，请联系adobe-tech@magnite.com

## 支持的身份 {#supported-identities}

菱格流：批处理目标可以接收 *任意* 来自AdobeCDP的身份源。 目前，此目标具有三个目标标识字段可供您映射到。

>[!NOTE]
>
>*任何* 标识源可以映射到任何magnite_deviceId目标标识。

| 目标身份 | 描述 | 注意事项 |
|:--------------------------- |:------------------------------------------------------------------------------------------------ |:------------------------------------------------------------------------------------- |
| magnite_deviceId_GAID | GOOGLE ADVERTISING ID | 当源身份是GAID时，选择此目标身份 |
| magnite_deviceId_IDFA | 广告商的Apple ID | 当源身份为IDFA时，选择此目标身份 |
| magnite_deviceId_CUSTOM | 自定义/用户定义的ID | 当源标识不是GAID或IDFA，或者为自定义ID或用户定义的ID时，选择此目标标识 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

| 受众来源 | 支持 | 描述 |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ {\f13 } | 受众 [已导入](../../../segmentation/ui/audience-portal.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

| 项目 | 类型 | 注释 |
|-----------------------------|----------|----------|
| 导出类型 | 受众导出 | 您正在导出具有Magnite流：批处理目标中使用的标识符（姓名、电话号码或其他）的受众的所有成员。 |
| 导出频率 | 批次 | 批量目标以三、六、八、十二或二十四小时的增量将文件导出到下游平台。 阅读有关批次的更多信息 [基于文件的目标](/help/destinations/destination-types.md). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

目标使用情况获得批准且Magnite Streaming已共享您的凭据后，请按照以下步骤验证、映射和共享数据。

### 验证目标 {#authenticate}

在Adobe体验目录中找到Magnite流：批处理目标。 单击其他选项按钮(\...)，然后配置目标连接/实例。

如果您已经拥有现有帐户，则可以通过将“帐户类型”选项更改为“现有帐户”来查找该帐户。 否则，您将在下面创建一个帐户：

要创建新帐户并首次向目标验证帐户，请填写所需的“S3访问密钥”和“S3密钥”字段（通过帐户管理员提供），然后选择 **[!UICONTROL 连接到目标]**

![目标配置身份验证字段未填写](../../assets/catalog/advertising/magnite/destination-batch-config-auth-unfilled.png)

>[!NOTE]
>
>Magnite流的安全策略要求定期轮换S3密钥。 您以后应该会使用新的S3访问和S3密钥更新帐户。 您只需更新帐户本身 — 使用该帐户的目标会自动使用更新的密钥。 如果未能上传新密钥，则会导致数据无法发送到此目标。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

* **[!UICONTROL 名称]**：用于将来识别此目标连接/实例的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标连接/实例的描述。
* **[!UICONTROL 您的源合作伙伴的名称]**：您希望作为Magnite Streaming平台中的源使用的名称

![目标配置身份验证字段已填写](../../assets/catalog/advertising/magnite/destination-batch-config-auth-filled.png)

>[!NOTE]
>
>如果您计划发送多个ID类型（GAID、IDFA等） 使用批处理目标时，每个目标都需要新的目标连接/实例。 有关更多信息，请与您的Magnite客户代表联系。

然后，您可以通过选择 **[!UICONTROL 下一个]**

在标题为“治理策略和强制执行操作（可选）”的下一个屏幕上，您可以选择任意相关的数据治理策略。 通常，会为Magnite流批处理目标选择“数据导出”。

![可选的治理策略和实施行动](../../assets/catalog/advertising/magnite/destination-batch-config-grouping-policy.png)

选中后，或者如果要跳过此可选屏幕，请选择 **[!UICONTROL 创建]**

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

### 将区段激活到此目标 {#activate}

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射属性和身份 {#map}

在 **[!UICONTROL Source字段]**中，您可以选择设备的任意属性或标识。 在本例中，我们选择了一个名为“DeviceId”的自定义IdentityMap
![将所需的数据字段映射到device_id字段](../../assets/catalog/advertising/magnite/destination-batch-active-audience-field-mapping.png)

在 **[!UICONTROL 目标字段]**：
![选择适当的设备类型目标标识](../../assets/catalog/advertising/magnite/destination-batch-active-audience-select-device-type.png) 请参阅 [支持的身份](#supported-identities) 以了解更多信息。
在此示例中，我们已选择 **[!UICONTROL 目标字段]**：magnite_deviceId_CUSTOM，因为我们的 **[!UICONTROL Source字段]** 定义为自定义IdentityMap： DeviceID。

>[!NOTE]
>
>如果您计划发送/映射多个ID类型（GAID、IDFA等） 使用批处理目标时，每个目标都需要新的目标连接/实例。 有关更多信息，请与您的Magnite客户代表联系。


在“为每个受众配置文件名和导出计划”屏幕上，您现在必须为每个受众配置开始日期（必需）、结束日期（可选）和映射ID（必需）。

>[!IMPORTANT]
>
> 此目标需要映射ID或“NONE”。
>
> 当受众具有Magnite流先前已知的预先存在的区段ID时，应该提供映射ID。 否则，应使用“NONE”作为映射ID。
>
> 在为每个受众配置文件名时，请通过“自定义文本”字段包含映射ID以添加。 映射ID将附加为： `{previous_filename}\_\[MAPPING_ID\].` 如果此受众是Magnite Streaming的新受众，并且您不提供映射ID，则应在“自定义文本”字段中输入“NONE”。 在这种情况下，新文件名应为： `{previous_filename}\_\[NONE\]`.

## 导出的数据/验证数据导出 {#exported-data}

上传受众后，您可以验证受众是否已正确创建和上传。

* Magnite流批处理目标每天将S3文件交付给Magnite流。 投放和引入后，受众/区段预计会显示在Magnite流中，并可应用于交易。 您可以通过查找在Adobe Experience Platform中的激活步骤中共享的区段ID或区段名称来确认这一点。

>[!NOTE]
>
>激活/交付到Magnite流批处理目标的受众将 *replace* 通过Magnite流式实时目标激活/投放的受众。 如果您使用区段名称查找区段，则在Magnite流平台摄取并处理批次之前，可能无法实时找到该区段。

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

有关其他帮助文档，请访问 [菱镁矿帮助中心](https://help.magnite.com/help).
