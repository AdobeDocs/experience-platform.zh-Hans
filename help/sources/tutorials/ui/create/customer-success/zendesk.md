---
keywords: Experience Platform;Zendesk；源；连接器；源连接器；源SDK;SDK;Zendesk;Zendesk
title: 在UI中创建Zendesk源连接
description: 了解如何使用Adobe Experience Platform UI创建Zendesk源连接。
exl-id: 75d303b0-2dcd-4202-987c-fe3400398d90
source-git-commit: 795c98fb555f79afd7a7035a23a9989cc734a1e1
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 6%

---

# （测试版）创建 [!DNL Zendesk] UI中的源连接

>[!NOTE]
>
>的 [!DNL Zendesk] 来源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

本教程提供了创建 [!DNL Zendesk] 源连接。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

### 收集所需的凭据

为了访问 [!DNL Zendesk] 帐户，必须为以下凭据提供值：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| Subdomain | 在注册过程中创建的特定于您帐户的唯一域。 | `yoursubdomain` |
| 访问令牌 | Zendesk API令牌。 | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

有关对 [!DNL Zendesk] 来源，请参阅 [[!DNL Zendesk] 源概述](../../../../connectors/customer-success/zendesk.md).

![Zendesk API令牌](../../../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

### 为创建平台模式 [!DNL Zendesk]

在创建 [!DNL Zendesk] 源连接时，还必须确保首先创建要用于源的平台架构。 请参阅 [创建平台模式](../../../../../xdm/schema/composition.md) 有关如何创建架构的完整步骤。

有关 [!DNL Zendesk] 所需架构 [!DNL Zendesk Search API]，请参阅 [限制](#limits) 部分。

![创建架构](../../../../images/tutorials/create/zendesk/schema.png)

## 连接 [!DNL Zendesk] 帐户

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 *客户成功* 类别，选择 **[!UICONTROL 曾代克]**，然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/zendesk/catalog.png)

的 **[!UICONTROL 连接Zendesk帐户]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 *曾代克* 创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/zendesk/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后提供名称、可选描述和您的凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后，再留出一些时间建立新连接。

![新建](../../../../images/tutorials/create/zendesk/new.png)

### 选择数据

在您的源进行身份验证后，该页面会更新到交互式架构树中，以便您探索和检查数据的层次结构。 选择 **[!UICONTROL 下一个]** 以继续。

![select-data](../../../../images/tutorials/create/zendesk/select-data.png)

## 后续步骤

通过本教程，您已通过身份验证，并在 [!DNL Zendesk] 帐户和平台。 您现在可以继续下一个教程和 [创建数据流以将客户成功数据引入平台](../../dataflow/customer-success.md).

## 其他资源

以下部分提供了在使用 [!DNL Zendesk] 来源。

### 验证 {#validation}

以下概述了验证您是否已成功连接可采取的步骤 [!DNL Zendesk] 来源和 [!DNL Zendesk] 用户档案将被摄取到平台。

在平台UI中，选择 **[!UICONTROL 数据集]** 从左侧导航访问 [!UICONTROL 数据集] 工作区。 的 [!UICONTROL 数据集活动] 屏幕可显示执行的详细信息。

![活动页面](../../../../images/tutorials/create/zendesk/dataset-activity.png)

接下来，选择要查看的数据流的数据流运行ID，以查看该数据流运行的特定详细信息。

![“数据流”页](../../../../images/tutorials/create/zendesk/dataflow-monitoring.png)

最后，选择 **[!UICONTROL 预览数据集]** 以显示摄取的数据。

![Zendesk数据集](../../../../images/tutorials/create/zendesk/preview-dataset.png)

您还可以根据 [!DNL Zendesk] > [!DNL Customers] 页面。

![zendesk-customers](../../../../images/tutorials/create/zendesk/zendesk-customers.png)

### Zendesk模式

下表列出了必须为Zendesk设置的支持映射。

>[!TIP]
>
>请参阅 [Zendesk搜索API >导出搜索结果](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) 以了解有关API的更多信息。

| 来源 | 类型 |
|---|---|
| `results.active` | 布尔型 |
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
| `results.moderator` | 布尔型 |
| `results.name` | 字符串 |
| `results.notes` | 字符串 |
| `results.only_private_comments` | 布尔型 |
| `results.organization_id` | 整数 |
| `results.phone` | 字符串 |
| `results.photo` | 字符串 |
| `results.report_csv` | 布尔型 |
| `results.restricted_agent` | 布尔型 |
| `results.result_type` | 字符串 |
| `results.role` | 字符串 |
| `results.role_type` | 整数 |
| `results.shared` | 布尔型 |
| `results.shared_agent` | 布尔型 |
| `results.shared_phone_number` | 布尔型 |
| `results.signature` | 字符串 |
| `results.suspended` | 布尔型 |
| `results.ticket_restriction` | 字符串 |
| `results.time_zone` | 字符串 |
| `results.two_factor_auth_enabled` | 布尔型 |
| `results.updated_at` | 字符串 |
| `results.url` | 字符串 |
| `results.verified` | 布尔型 |

{style=&quot;table-layout:auto&quot;}

### 限制 {#limits}

* 的 [Zendesk搜索API >导出搜索结果](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) 每页最多返回1000条记录。
   * 的值 ``filter[type]`` 参数设置为 ``user`` 因此，Zendesk连接仅返回用户。
   * 每页的结果数由 ``page[size]`` 参数。 值设置为 ``100``. 这样做是为了减少Zendesk设置的速度减少限制的影响。
   * 请参阅 [限制](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#limits) 和 [分页](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#pagination-1).
   * 您还可以参阅 [使用光标分页在列表中分页](https://developer.zendesk.com/documentation/developer-tools/pagination/paginating-through-lists-using-cursor-pagination/).
