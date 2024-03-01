---
title: Gainsight PX连接
description: 使用Gainsight PX目标将分段信息发送到Gainsight PX平台。
last-substantial-update: 2024-02-20T00:00:00Z
source-git-commit: dff460f0b0d365d3d643744544642d9f9488e18a
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 3%

---


# Gainsight PX连接 {#gainsight-px}

## 概述 {#overview}

[[!DNL Gainsight PX]](https://www.gainsight.com/product-experience/) 是一个产品体验平台，它使产品团队能够了解用户如何使用其产品、收集反馈和创建应用程序内参与，如产品演练，以推动用户入门和产品采用。

>[!IMPORTANT]
>
>目标连接器和文档页面由创建和维护 *Gainsight PX* 团队。 如有任何查询或更新请求，请直接通过以下电子邮件联系他们： *`pxsupport@gainsight.com`*.

## 用例 {#use-cases}

为了帮助您更好地了解您应该如何以及何时使用 *Gainsight PX* 目标，以下是Adobe Experience Platform客户可以使用此目标解决的示例用例。

### 定位应用程序内参与 {#targeting-in-app-engagements}

SaaS公司希望通过基于Gainsight PX构建的应用程序内指南吸引客户。 已在Adobe Experience Platform上构建要接收此预订的受众。 Gainsight PX目标接收受众，并在Gainsight PX环境中提供该受众。

## 先决条件 {#prerequisites}

* 联系 [!DNL Gainsight] 支持团队并要求为您的订阅激活外部区段功能。
* 使用为您的PX订阅生成OAuth密钥值 **[!UICONTROL 生成新密码]** 按钮底部的 [公司详细信息页面](https://app.aptrinsic.com/settings/subscription)
  ![Gainsight PX中的“公司详细信息”屏幕，其中显示“生成新密钥”按钮](../../assets/catalog/analytics/gainsight-px/generate_oauth_secret.png)

## 支持的身份 {#supported-identities}

Gainsight PX支持激活下表中描述的标识。 了解有关 [身份](../../../identity-service/features/namespaces.md).

| 目标身份 | 描述 |
|---|----|
| 标识ID | 在Gainsight PX和Adobe Experience Platform中唯一标识用户的通用用户标识符 |

{style="table-layout:auto"}

## 支持的受众 {#supported-audiences}

本节介绍可导出到此目标的受众类型。

| 受众来源 | 受支持 | 描述 |
|---|---|---|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | X | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---|---|---|
| 导出类型 | **[!UICONTROL 区段导出]** | 您正使用 [!DNL Gainsight PX] 目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 当基于受众评估在Experience Platform中更新用户档案时，连接器将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 连接到目标 {#connect}

>[!IMPORTANT]
>
>要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要连接到此目标，请按照 [目标配置教程](../../ui/connect-destination.md). 在目标配置工作流中，填写下面两个部分中列出的字段。

### 验证目标 {#authenticate}

要向目标进行身份验证，请填写必填字段并选择 **[!UICONTROL 连接到目标]**.

![身份验证屏幕截图](../../assets/catalog/analytics/gainsight-px/auth-screen.png)

* **[!UICONTROL 密码]**：用于登录的密码 [[!DNL Gainsight PX]](https://app.aptrinsic.com)
* **[!UICONTROL 客户端ID]**：上的Gainsight PX订阅ID [公司详细信息页面](https://app.aptrinsic.com/settings/subscription)
* **[!UICONTROL 客户端密码]**：在底部生成的OAuth密钥 [公司详细信息页面](https://app.aptrinsic.com/settings/subscription) 在 [!DNL Gainsight PX] UI。
* **[!UICONTROL 用户名]**：用于登录到 [[!DNL Gainsight PX]](https://app.aptrinsic.com) UI

### 填写目标详细信息 {#destination-details}

要配置目标的详细信息，请填写下面的必需和可选字段。 UI中字段旁边的星号表示该字段为必填字段。

![Experience Platform用户界面中的目标详细信息屏幕，显示如何填写名称和描述字段](../../assets/catalog/analytics/gainsight-px/destination_details.png)

* **[!UICONTROL 名称]**：将来用于识别此目标的名称。
* **[!UICONTROL 描述]**：可帮助您将来识别此目标的描述。

完成提供目标连接的详细信息后，选择 **[!UICONTROL 下一个]**.

## 将区段激活到此目标 {#activate}

>[!IMPORTANT]
>
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

读取 [将配置文件和区段激活到流式区段导出目标](/help/destinations/ui/activate-segment-streaming-destinations.md) 有关将受众区段激活到此目标的说明。

### 映射身份 {#map}

此目标支持配置文件属性和身份命名空间的映射。 目标映射必须始终为 **[!UICONTROL IDENTIFY_ID]** 身份命名空间。

请参阅下面的示例，以更好地了解如何配置映射。

#### 映射配置文件属性 {#map-profile-attribute}

在以下显示的示例中，源字段是XDM配置文件属性，该属性被映射到IDENTIFY_ID目标命名空间。

![身份命名空间示例映射屏幕，其中显示如何选择源值和目标值](../../assets/catalog/analytics/gainsight-px/mapping_attribute.png)

#### 映射身份命名空间 {#map-identity-namespace}

在以下示例中，源字段是身份命名空间(**[!UICONTROL ECID]**)映射到的 **[!UICONTROL IDENTIFY_ID]** 目标命名空间。

![属性示例映射屏幕，显示如何选择源值和目标值](../../assets/catalog/analytics/gainsight-px/mapping_identities.png)

## 导出的数据/验证数据导出 {#exported-data}

分段数据将从Experience Platform流式传输到Gainsight PX。

区段元数据在 [!DNL Gainsight PX] UI。

![Gainsight PX中的区段列表屏幕显示外部区段。](../../assets/catalog/analytics/gainsight-px/segment_metadata.png)

区段成员资格信息在Audience Explorer屏幕的“区段”选项卡上可见。 [!DNL Gainsight PX] UI。

![Gainsight PX中的Audience Explorer屏幕显示用户的关联区段。](../../assets/catalog/analytics/gainsight-px/PX_Segments.png)

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 实施数据管理，请阅读 [数据管理概述](/help/data-governance/home.md).
