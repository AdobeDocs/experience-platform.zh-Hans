---
title: Splunk扩展概述
description: 了解Adobe Experience Platform中用于事件转发的Splunk扩展。
exl-id: 653b5897-493b-44f2-aeea-be492da2b108
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 1%

---

# Splunk扩展概述

[Splunk](https://www.splunk.com)是一个可观察性平台，可提供针对您的数据的可操作洞察的搜索、分析和可视化图表。 Splunk [事件转发](../../../ui/event-forwarding/overview.md)扩展利用[Splunk HTTP事件收集器REST API](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/HECRESTendpoints)将事件从Adobe Experience Platform Edge Network发送到[Splunk HTTP事件收集器](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)。

Splunk使用持有者令牌作为身份验证机制，与Splunk事件收集器API进行通信。

## 用例 {#use-cases}

营销团队可以将该扩展用于以下用例：

| 用例 | 描述 |
| --- | --- |
| 客户行为分析 | 组织可以从其网站中捕获客户互动事件数据，并将相关事件转发给Splunk。 接下来，营销和分析团队可以在Splunk平台内执行后续分析，以了解关键用户交互和行为。 Splunk平台可用于生成图形、仪表板或其他可视化图表，以告知业务利益相关者。 |
| 对大型数据集进行可扩展搜索 | 组织可以从网站中捕获事务性或对话性输入作为事件数据，并将事件转发到Splunk。 然后，Analytics团队可以利用Splunk的可扩展索引功能筛选和处理大型数据集，以获得任何业务见解并做出明智决策。 |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

您必须拥有Splunk帐户才能使用此扩展。 您可以在[Splunk主页](https://www.splunk.com/page/sign_up)上注册Splunk帐户。

>[!NOTE]
>
> Splunk扩展同时支持Splunk Cloud和Splunk Enterprise实例。 本指南记录使用[Splunk Cloud](https://www.splunk.com/en_us/products/splunk-cloud-platform.html)作为参考的实施。 [Splunk Enterprise](https://www.splunk.com/en_us/products/splunk-enterprise.html)的配置过程类似，但需要Splunk Enterprise管理员的具体指导。

要配置扩展，您还必须具有以下技术值：

* [事件收集器令牌](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector#Create_an_Event_Collector_token_on_Splunk_Cloud_Platform)。 令牌通常为UUIDv4格式，如下所示： `12345678-1234-1234-1234-1234567890AB`。
* 贵组织的Splunk平台实例地址和端口。 平台实例地址和端口通常具有以下格式： `mysplunkserver.example.com:443`。

  >[!IMPORTANT]
  >
  > 在事件转发中引用的Splunk终结点应仅使用端口`443`。 当前事件转发实施不支持非标准端口。

## 安装Splunk扩展 {#install}

要在UI中安装Splunk事件收集器扩展，请导航到&#x200B;**事件转发**&#x200B;并选择要将扩展添加到的属性，或改为创建新属性。

选择或创建所需的属性后，导航到&#x200B;**扩展** > **目录**。 搜索“[!DNL Splunk]”，然后在Splunk扩展中选择&#x200B;**[!DNL Install]**。

在UI中选择的Splunk扩展的![安装按钮](../../../images/extensions/server/splunk/install.png)

## 配置Splunk扩展 {#configure_extension}

>[!IMPORTANT]
>
>根据您的实施需求，您可能需要在配置扩展之前创建架构、数据元素和数据集。 请在开始之前查看所有配置步骤，以确定需要为用例设置哪些实体。

在左侧导航中选择&#x200B;**扩展**。 在&#x200B;**Installed**&#x200B;下，选择Splunk扩展上的&#x200B;**Configure**。

在UI中选择的Splunk扩展的![配置按钮](../../../images/extensions/server/splunk/configure.png)

对于&#x200B;**[!UICONTROL HTTP Event Collector URL]**，输入您的Splunk平台实例地址和端口。 在&#x200B;**[!UICONTROL Access Token]**&#x200B;下，输入您的[!DNL Event Collector Token]值。 完成后，选择&#x200B;**[!UICONTROL Save]**。

在UI中填写了![配置选项](../../../images/extensions/server/splunk/input.png)

## 配置事件转发规则 {#config_rule}

开始创建新的事件转发规则[规则](../../../ui/managing-resources/rules.md)，并根据需要配置其条件。 为规则选择操作时，选择[!UICONTROL Splunk]扩展，然后选择[!UICONTROL Create Event]操作类型。 其他控件似乎可用于进一步配置Splunk事件。

![定义操作配置](../../../images/extensions/server/splunk/action-configurations.png)

下一步是将Splunk事件属性映射到您之前创建的数据元素。 下面提供了基于可设置的输入事件数据的受支持的可选映射。 有关详细信息，请参阅[Splunk文档](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/FormateventsforHTTPEventCollector#Event_metadata)。

| 字段名称 | 描述 |
| --- | --- |
| [!UICONTROL Event]<br><br>**（必需）** | 指示您要如何提供事件数据。 事件数据可以分配给HTTP请求中JSON对象内的`event`键，也可以是原始文本。 `event`键与元数据键在JSON事件数据包中的级别相同。 在`event`键值大括号内，数据可以采用您需要的任何形式（例如字符串、数字、其他JSON对象等）。 |
| [!UICONTROL Host] | 从中发送数据的客户端的主机名。 |
| [!UICONTROL Source Type] | 要分配给事件数据的源类型。 |
| [!UICONTROL Source] | 要分配给事件数据的源值。 例如，如果您从正在开发的应用程序发送数据，请将此键设置为应用程序的名称。 |
| [!UICONTROL Index] | 事件数据的索引的名称。 如果令牌设置了索引参数，则此处指定的索引必须在允许的索引列表中。 |
| [!UICONTROL Time] | 事件时间。 默认时间格式为UNIX时间（格式为`<sec>.<ms>`），具体取决于您的本地时区。 例如，`1433188255.500`表示新纪元后的1433188255秒和500毫秒，或2015年6月1日星期一晚上7:50:55 GMT。 |
| [!UICONTROL Fields] | 指定原始JSON对象或一组包含要在索引时定义的显式自定义字段的键值对。  `fields`键不适用于原始数据。包含<br><br>属性的请求必须发送到`fields`终结点，否则将不会对它们编制索引。 `/collector/event`有关详细信息，请参阅有关[索引字段提取](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/IFXandHEC)的Splunk文档。 |

### 验证Splunk中的数据 {#validate}

创建并执行事件转发规则后，验证发送到Splunk API的事件是否按Splunk UI中的预期方式显示。 如果事件收集和Experience Platform集成成功，您将在Splunk控制台中看到如下事件：

![事件数据在验证期间出现在Splunk UI中](../../../images/extensions/server/splunk/splunk-data.png)

## 后续步骤

本文档介绍了如何在UI中安装和配置Splunk事件转发扩展。 有关在Splunk中收集事件数据的更多信息，请参阅官方文档：

* [在Splunk Web中设置并使用HTTP事件收集器](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)
* [使用令牌设置身份验证](https://docs.splunk.com/Documentation/Splunk/8.2.5/Security/Setupauthenticationwithtokens#Prerequisites_for_activating_tokens)
* [HTTP事件收集器故障排除](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector)（还列出了[可能错误代码](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector#Possible_error_codes)的汇编）
