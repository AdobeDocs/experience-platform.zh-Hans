---
title: Splunk扩展概述
description: 了解在Adobe Experience Platform中用于事件转发的Splunk扩展。
source-git-commit: e6f0bdcdb11630730834e353064abb960d3d0ea1
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 1%

---

# Splunk扩展概述

[Splunk](https://www.splunk.com) 是一个可观性平台，可提供搜索、分析和可视化图表，以便对数据提供可操作的洞察。 苏普隆克 [事件转发](../../../ui/event-forwarding/overview.md) 扩展利用 [Splunk HTTP事件收集器REST API](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/HECRESTendpoints) 将事件从Adobe Experience Platform边缘网络发送到 [Splunk HTTP事件收集器](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector).

Splunk使用载体令牌作为身份验证机制与Splunk事件收集器API通信。

## 用例 {#use-cases}

营销团队可以将该扩展用于以下用例：

| 用例 | 描述 |
| --- | --- |
| 客户行为分析 | 组织可以从其网站中捕获客户交互事件数据，并将相关事件转发给Splunk。 然后，营销和分析团队可以在Splunk平台内执行后续分析，以了解关键用户交互和行为。 Splunk平台可用于生成图形、功能板或其他可视化图表，以告知业务利益相关方。 |
| 对大数据集的可缩放搜索 | 组织可以将事务性或会话性输入作为事件数据从网站中捕获，并将事件转发到Splunk。 然后，Analytics团队可以利用Splunk的可扩展索引化功能，过滤和处理大型数据集，从而得出任何业务分析并做出明智的决策。 |

{style=&quot;table-layout:auto&quot;}

## 先决条件 {#prerequisites}

您必须拥有Splunk帐户才能使用此扩展。 您可以在 [Splunk主页](https://www.splunk.com/page/sign_up).

>[!NOTE]
>
> Splunk扩展同时支持Splunk Cloud和Splunk企业实例。 本指南记录了使用 [Splunk云](https://www.splunk.com/en_us/products/splunk-cloud-platform.html) 作为参考。 的配置过程 [Splunk Enterprise](https://www.splunk.com/en_us/products/splunk-enterprise.html) 类似，但需要Splunk Enterprise管理员提供具体指导。

您还必须具有以下技术值才能配置扩展：

* 安 [事件收集器令牌](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector#Create_an_Event_Collector_token_on_Splunk_Cloud_Platform). 令牌通常采用UUIDv4格式，如下所示： `12345678-1234-1234-1234-1234567890AB`.
* 贵组织的Splunk平台实例地址和端口。 平台实例地址和端口通常具有以下格式： `mysplunkserver.example.com:443`.
   >[!IMPORTANT]
   >
   > 事件转发中引用的Splunk端点应仅使用端口 `443`. 事件转发实施当前不支持非标准端口。

## 安装Splunk扩展 {#install}

要在UI中安装Splunk事件收集器扩展，请导航到 **事件转发** ，然后选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的资产后，导航到 **扩展** > **目录**. 搜索“[!DNL Splunk]&quot;，然后选择 **[!DNL Install]** Splunk扩展上。

![在UI中选择的Splunk扩展的“安装”按钮](../../../images/extensions/splunk/install.png)

## 配置Splunk扩展 {#configure_extension}

>[!IMPORTANT]
>
>根据您的实施需求，您可能需要先创建架构、数据元素和数据集，然后再配置该扩展。 请在开始之前查看所有配置步骤，以确定您需要为用例设置哪些实体。

选择 **扩展** 中。 在 **已安装**，选择 **配置** Splunk扩展上。

![为在UI中选择的Splunk扩展配置按钮](../../../images/extensions/splunk/configure.png)

对于 **[!UICONTROL HTTP事件收集器URL]**，输入您的Splunk平台实例地址和端口。 在 **[!UICONTROL 访问令牌]**，输入 [!DNL Event Collector Token] 值。 完成后，选择 **[!UICONTROL 保存]**.

![在UI中填写的配置选项](../../../images/extensions/splunk/input.png)

## 配置事件转发规则 {#config_rule}

开始创建新的事件转发规则 [规则](../../../ui/managing-resources/rules.md) 并根据需要配置其条件。 为规则选择操作时，选择 [!UICONTROL Splunk] 扩展，然后选择 [!UICONTROL 创建事件] 操作类型。 显示其他控件以进一步配置Splunk事件。

![定义操作配置](../../../images/extensions/splunk/action-configurations.png)

下一步是将Splunk事件属性映射到您之前创建的数据元素。 下面提供了基于可设置的输入事件数据的支持的可选映射。 请参阅 [Splunk文档](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/FormateventsforHTTPEventCollector#Event_metadata) 以了解更多详细信息。

| 字段名称 | 描述 |
| --- | --- |
| [!UICONTROL 事件&#x200B;]<br><br>**（必需）** | 指示您希望如何提供事件数据。 事件数据可以分配给 `event` 键（在HTTP请求的JSON对象中），或者它可以是原始文本。 的 `event` 键值与元数据键位于JSON事件包中的相同级别。 在 `event` 键值大括号中，数据可以采用您所需的任何形式（例如字符串、数字、其他JSON对象等）。 |
| [!UICONTROL Host] | 您从中发送数据的客户端的主机名。 |
| [!UICONTROL 源类型] | 要分配给事件数据的源类型。 |
| [!UICONTROL 来源] | 要分配给事件数据的源值。 例如，如果您发送的是来自正在开发的应用程序的数据，请将此键值设置为应用程序的名称。 |
| [!UICONTROL 索引] | 事件数据索引的名称。 如果令牌设置了索引参数，则此处指定的索引必须位于允许的索引列表中。 |
| [!UICONTROL 时间] | 事件时间。 默认时间格式为UNIX时间(格式为 `<sec>.<ms>`)并取决于您的本地时区。 例如， `1433188255.500` 表示在纪元后1433188255秒和500毫秒，或2015年6月1日星期一7时:50:55 PM GMT。 |
| [!UICONTROL 字段] | 指定原始JSON对象或一组键值对，其中包含要在索引时定义的显式自定义字段。  的 `fields` 键不适用于原始数据。<br><br>包含的请求 `fields` 必须将资产发送到 `/collector/event` 端点，否则不会将其编入索引。 有关更多信息，请参阅 [索引字段提取](http://docs.splunk.com/Documentation/Splunk/8.2.5/Data/IFXandHEC). |

### 验证Splunk中的数据 {#validate}

创建并执行事件转发规则后，验证发送到Splunk API的事件是否按预期显示在Splunk UI中。 如果事件收集和Experience Platform集成成功，您将在Splunk控制台中看到如下事件：

![验证期间Splunk UI中显示的事件数据](../../../images/extensions/splunk/splunk-data.png)

## 后续步骤

本文档介绍了如何在UI中安装和配置Splunk事件转发扩展。 有关在Splunk中收集事件数据的更多信息，请参阅官方文档：

* [在Splunk Web中设置和使用HTTP事件收集器 ](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)
* [使用令牌设置身份验证](https://docs.splunk.com/Documentation/Splunk/8.2.5/Security/Setupauthenticationwithtokens#Prerequisites_for_activating_tokens)
* [HTTP事件收集器故障诊断](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector) (还列有 [可能的错误代码](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector#Possible_error_codes))
