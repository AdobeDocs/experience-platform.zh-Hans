---
title: PubMatic Connect
description: PubMatic通过提供面向未来的程序化数字营销供应链，最大程度地实现客户价值。 PubMatic Connect将平台技术和专用服务相结合，以增强库存和数据打包和事务处理的方式。
last-substantial-update: 2023-12-14T00:00:00Z
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 3%

---


# PubMatic Connect目标 {#pubmatic-connect}

## 概述 {#overview}

使用 [!DNL PubMatic Connect] 通过提供未来的程序化数字营销供应链，最大程度地实现客户价值。 [!DNL PubMatic Connect] 将平台技术和专用服务相结合，以增强库存和数据的打包和交易方式。

使用此目标可将受众数据发送到 [!DNL PubMatic Connect] 平台。

>[!IMPORTANT]
>
>目标连接器和文档页面由创建和维护 [!DNL PubMatic] 团队。 如有任何查询或更新请求，请直接通过以下电子邮件联系他们： `support@pubmatic.com`.

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用 [!DNL PubMatic Connect] 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 在移动、Web和CTV平台上定位用户 {#targeting}

发布者或数据提供商希望将受众从Adobe Experience Platform发送到 [!DNL PubMatic Connect] 使用大量标识符定位移动、Web和CTV平台上的用户。

## 先决条件 {#prerequisites}

与您的 [!DNL PubMatic] 客户经理，以确保您的帐户配置正确并支持载入受众区段。 他们还将确保您拥有使用此目标的所有相关详细信息，并在设置期间为您提供支持。

## 支持的身份 {#supported-identities}

[!DNL PubMatic Connect] 支持激活下表中描述的标识。 了解有关 [身份](/help/identity-service/namespaces.md).

| 目标身份 | 描述 | 注意事项 |
| --------------- | ------ | --- |
| GAID | Google广告ID | 当源身份是GAID命名空间时，选择GAID目标身份。 |
| IDFA | 广告商的Apple ID | 当源身份是IDFA命名空间时，选择IDFA目标身份。 |
| extern_id | 自定义用户标识 | 当源身份是自定义命名空间时，请选择此目标身份。 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

此部分介绍可将哪种类型的受众导出到此目标。

| 受众来源 | 受支持 | 描述 |
| --- | --------- | ------ |
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
| --- | --- | --- |
| 导出类型 | **[!UICONTROL 区段导出]** | 您正在导出具有PubMatic Connect目标中使用的标识符（名称、电话号码或其他）的区段（受众）的所有成员。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 当基于区段评估在Experience Platform中更新用户档案时，连接器将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
> 要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

![如何进行身份验证](../../assets/catalog/advertising/pubmatic/authenticate-destination.png)

- **[!UICONTROL 持有者令牌]**：填写持有者令牌以对目标进行身份验证。

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![目标详细信息](../../assets/catalog/advertising/pubmatic/destination-details.png)

- **[!UICONTROL 名称]**：将来用于识别此目标的名称。
- **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。
- **[!UICONTROL 数据合作伙伴ID]**：在中设置的数据合作伙伴ID [!DNL PubMatic] 帐户。
- **[!UICONTROL 默认国家/地区代码]**：默认国家/地区代码，如果未在配置文件中提供，则应用于所有身份。
- **[!UICONTROL 帐户ID]**：您的 [!DNL PubMatic Connect] 帐户ID。
- **[!UICONTROL 帐户类型]**：您的帐户类型 [!DNL PubMatic] 平台帐户。 与您的 [!DNL PubMatic] 如果您有任何问题需要选择，请咨询客户经理。 可用的选项为：
   - [!UICONTROL 发布者]
   - [!UICONTROL DEMAND_PARTNER]
   - [!UICONTROL 购买者]

### 启用警报 {#enable-alerts}

您可以启用警报，以接收有关发送到目标的数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅以下内容中的指南： [使用UI订阅目标警报](../../ui/alerts.md).

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
>
> - 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>
> - 要导出 _身份_，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](../../assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将配置文件和区段激活到流式区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射属性和身份 {#map}

选择源字段：

- 选择标识符（通常是IDFA或自定义ID命名空间等命名空间）。

选择目标字段：

- 与您的 [!DNL PubMatic] 客户经理，以获取有关哪种UID类型在此步骤中将被更正的信息。
- 选择 [!DNL PubMatic UID] 键入与您在第一个步骤中选择的标识符匹配的编号。

![映射属性和身份](../..//assets/catalog/advertising/pubmatic/export-identities-to-destination.png)

## 导出的数据/验证数据导出 {#exported-data}

此 [!DNL PubMatic] 通过UI，您可以检查数据是否已正确推送，以及区段是否可用。 在推送数据的过程中，最长可能需要24小时。 [!DNL PubMatic] 要更新的UI。

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](/help/data-governance/home.md).
