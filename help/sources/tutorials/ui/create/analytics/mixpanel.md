---
title: 在UI中创建Mixpanel源连接
description: 了解如何使用Adobe Experience Platform UI创建Mixpanel源连接。
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 9%

---

# 创建 [!DNL Mixpanel] UI中的源连接

本教程提供了用于创建 [!DNL Mixpanel] 源连接，使用Adobe Experience Platform Platform用户界面。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

### 收集所需的凭据

为了连接 [!DNL Mixpanel] 到Platform时，必须提供以下连接属性的值：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| 用户名 | 与您的对应的服务帐户用户名 [!DNL Mixpanel] 帐户。 请参阅 [[!DNL Mixpanel] 服务帐户文档](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) 以了解更多信息。 | `Test8.6d4ee7.mp-service-account` |
| 密码 | 与您的帐户对应的服务帐户密码 [!DNL Mixpanel] 帐户。 | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| 项目ID | 您的 [!DNL Mixpanel] 项目ID。 创建源连接需要此ID。 请参阅 [[!DNL Mixpanel] 项目设置文档](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 和 [[!DNL Mixpanel] 创建和管理项目指南](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) 以了解更多信息。 | `2384945` |
| 时区 | 与您的对应的时区 [!DNL Mixpanel] 项目。 创建源连接需要时区。 请参阅 [Mixpanel项目设置文档](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 以了解更多信息。 | `Pacific Standard Time` |

有关验证您的身份的详细信息 [!DNL Mixpanel] 源，请参见 [[!DNL Mixpanel] 源概述](../../../../connectors/analytics/mixpanel.md).

## 连接您的 [!DNL Mixpanel] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示了多种来源，您可以使用这些来源创建帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 *分析* 类别，选择 [!DNL Mixpanel]，然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

此 **[!UICONTROL 连接Mixpanel帐户]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL Mixpanel] 要用于创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后提供名称、可选描述和您的凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后等待一段时间以建立新连接。

![新建](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## 选择项目ID和时区 {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="为 Mixpanel 提取设置时区"
>abstract="时区必须与您的 Mixpanel 配置文件时区设置相同，因为 Platform 使用指定的项目时区来从 Mixpanel 提取相关数据。在将事件记录到 Mixpanel 数据存储之前，Mixpanel 将调整其时区以与您的项目时区协调。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html#project-id-and-timezone" text="请参阅文档以了解详情"

在您的源经过身份验证后，提供您的项目ID和时区，然后选择 **[!UICONTROL 选择]**.

摄取之前您指定的时区 [!DNL Mixpanel] 到Platform的数据必须与您的 [!DNL Mixpanel] 配置文件时区设置。 对数据时区所做的任何更改将仅适用于新事件，旧事件将保留在您之前指定的时区中。 [!DNL Mixpanel] 采用夏令时，并将相应地调整您的摄取时间戳。 欲了解时区如何影响数据的更多信息，请参见 [!DNL Mixpanel] 指南 [管理项目时区](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

片刻后，正确的界面将更新为预览面板，允许您在创建数据流之前检查架构。 完成后，选择 **[!UICONTROL 下一个]**.

![配置](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## 后续步骤

通过学习本教程，您已建立与的连接 [!DNL Mixpanel] 帐户。 您现在可以继续下一教程和 [配置数据流以将分析数据引入Platform](../../dataflow/analytics.md).

## 其他资源 {#additional-resources}

以下各节提供了在使用时，您可以参考的其他资源 [!DNL Mixpanel] 源。

### 验证 {#validation}

下面概述了验证是否成功连接 [!DNL Mixpanel] 来源和 [!DNL Mixpanel] 事件正在被摄取到Platform。

在Platform UI中，选择 **[!UICONTROL 数据集]** 从左侧导航栏访问 [!UICONTROL 数据集] 工作区。 此 [!UICONTROL 数据集活动] 屏幕显示执行的详细信息。

![数据集活动](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

接下来，选择要查看的数据流的数据流运行ID，以查看有关该数据流运行的特定详细信息。

![数据流监测](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

最后，选择 **[!UICONTROL 预览数据集]** 以显示所摄取的数据。

![预览数据集](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

您可以根据 [!DNL Mixpanel] > [!DNL Events] 页面。 请参阅 [[!DNL Mixpanel] 事件文档](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) 以了解更多信息。

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Mixpanel架构

下表列出了必须设置的受支持映射 [!DNL Mixpanel].

>[!TIP]
>
>请参阅 [事件导出API >下载](https://developer.mixpanel.com/reference/raw-event-export) 以了解有关API的更多信息。


| 来源 | 类型 |
|---|---|
| `distinct_id` | 字符串 |
| `event_name` | 字符串 |
| `import` | 布尔 |
| `insert_id` | 字符串 |
| `item_id` | 字符串 |
| `item_name` | 字符串 |
| `item_price` | 字符串 |
| `mp_api_endpoint` | 字符串 |
| `mp_api_timestamp_ms` | 整数 |
| `mp_processing_time_ms` | 整数 |
| `time` | 整数 |

### 限制 {#limits}

* 您每小时最多有100个并发查询和60个查询，如 [导出API速率限制](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).
