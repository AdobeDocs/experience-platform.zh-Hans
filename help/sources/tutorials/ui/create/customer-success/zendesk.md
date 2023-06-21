---
title: 在UI中创建Zendesk源连接
description: 了解如何使用Adobe Experience Platform UI创建Zendesk源连接。
exl-id: 75d303b0-2dcd-4202-987c-fe3400398d90
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 6%

---

# 创建 [!DNL Zendesk] UI中的源连接

本教程提供了用于创建 [!DNL Zendesk] 源连接(使用Adobe Experience Platform用户界面)。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

### 收集所需的凭据

要访问您的 [!DNL Zendesk] 帐户，则必须提供以下凭据的值：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| Subdomain | 注册过程中创建的特定于您帐户的唯一域。 | `yoursubdomain` |
| 访问令牌 | Zendesk API令牌。 | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

有关验证的详细信息 [!DNL Zendesk] 源，请参见 [[!DNL Zendesk] 源概述](../../../../connectors/customer-success/zendesk.md).

![Zendesk API令牌](../../../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

### 为创建平台架构 [!DNL Zendesk]

创建之前 [!DNL Zendesk] 源连接时，还必须确保首先创建用于源的Platform架构。 请参阅上的教程 [创建平台架构](../../../../../xdm/schema/composition.md) 以了解有关如何创建架构的全面步骤。

欲知对贵机构的其他指导， [!DNL Zendesk] 架构是 [!DNL Zendesk Search API]，请参阅 [限制](#limits) 部分。

![创建架构](../../../../images/tutorials/create/zendesk/schema.png)

## 连接您的 [!DNL Zendesk] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 以访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 *客户成功* 类别，选择 **[!UICONTROL Zendesk]**，然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/zendesk/catalog.png)

此 **[!UICONTROL 连接Zendesk帐户]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 *Zendesk* 要用于创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/zendesk/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后提供名称、可选描述和您的凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后留出一些时间来建立新连接。

![新](../../../../images/tutorials/create/zendesk/new.png)

### 选择数据

在您的源通过身份验证后，页面将更新为交互式架构树，允许您浏览和检查数据的层次结构。 选择 **[!UICONTROL 下一个]** 以继续。

![select-data](../../../../images/tutorials/create/zendesk/select-data.png)

## 后续步骤

按照本教程，您已验证并创建了源连接，该连接位于 [!DNL Zendesk] 帐户和平台。 您现在可以继续下一教程和 [创建数据流以将客户成功数据引入Platform](../../dataflow/customer-success.md).

## 其他资源

以下部分提供了在使用时可以参考的其他资源 [!DNL Zendesk] 源。

### 验证 {#validation}

下面概述了验证是否成功连接 [!DNL Zendesk] 来源和 [!DNL Zendesk] 配置文件正在被摄取到Platform。

在Platform UI中，选择 **[!UICONTROL 数据集]** 从左侧导航访问 [!UICONTROL 数据集] 工作区。 此 [!UICONTROL 数据集活动] 屏幕显示执行的详细信息。

![活动页面](../../../../images/tutorials/create/zendesk/dataset-activity.png)

接下来，选择要查看的数据流的数据流运行ID，以查看有关该数据流运行的特定详细信息。

![数据流页面](../../../../images/tutorials/create/zendesk/dataflow-monitoring.png)

最后，选择 **[!UICONTROL 预览数据集]** 以显示所摄取的数据。

![Zendesk数据集](../../../../images/tutorials/create/zendesk/preview-dataset.png)

您还可以根据以下网站上的数据验证Platform数据： [!DNL Zendesk] > [!DNL Customers] 页面。

![zendesk-customers](../../../../images/tutorials/create/zendesk/zendesk-customers.png)

### Zendesk架构

下表列出了必须为Zendesk设置的受支持映射。

>[!TIP]
>
>参见 [Zendesk搜索API >导出搜索结果](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) 以了解有关API的更多信息。

| 来源 | 类型 |
|---|---|
| `results.active` | 布尔值 |
| `results.alias` | 字符串 |
| `results.created_at` | 字符串 |
| `results.custom_role_id` | 整数 |
| `results.default_group_id` | 整数 |
| `results.details` | 字符串 |
| `results.email` | 字符串 |
| `results.external_id` | 整数 |
| `results.iana_time_zone` | 字符串 |
| `results.id` | 整数 |
| `results.last_login_at` | 字符串 |
| `results.locale` | 字符串 |
| `results.locale_id` | 整数 |
| `results.moderator` | 布尔值 |
| `results.name` | 字符串 |
| `results.notes` | 字符串 |
| `results.only_private_comments` | 布尔值 |
| `results.organization_id` | 整数 |
| `results.phone` | 字符串 |
| `results.photo` | 字符串 |
| `results.report_csv` | 布尔值 |
| `results.restricted_agent` | 布尔型 |
| `results.result_type` | 字符串 |
| `results.role` | 字符串 |
| `results.role_type` | 整数 |
| `results.shared` | 布尔值 |
| `results.shared_agent` | 布尔型 |
| `results.shared_phone_number` | 布尔型 |
| `results.signature` | 字符串 |
| `results.suspended` | 布尔值 |
| `results.ticket_restriction` | 字符串 |
| `results.time_zone` | 字符串 |
| `results.two_factor_auth_enabled` | 布尔值 |
| `results.updated_at` | 字符串 |
| `results.url` | 字符串 |
| `results.verified` | 布尔值 |

{style="table-layout:auto"}

### 限制 {#limits}

* 此 [Zendesk搜索API >导出搜索结果](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) 每页最多返回1000条记录。
   * 的值 ``filter[type]`` 参数设置为 ``user`` 因此，Zendesk连接仅返回用户。
   * 每页的结果数由 ``page[size]`` 参数。 该值设置为 ``100``. 这样做是为了减少Zendesk设置的减速限制的影响。
   * 参见 [限制](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#limits) 和 [分页](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#pagination-1).
   * 您还可以参阅 [使用光标分页来分页列表](https://developer.zendesk.com/documentation/developer-tools/pagination/paginating-through-lists-using-cursor-pagination/).
