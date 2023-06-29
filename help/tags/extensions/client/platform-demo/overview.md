---
title: Adobe Experience Platform演示扩展概述
description: 了解Adobe Experience Platform中的Adobe Experience Platform Demo扩展。
exl-id: 4bafa132-0d21-4140-ab46-f09cc20bce6f
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 72%

---

# Adobe Experience Platform 演示扩展

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

>[!NOTE]
>
>此扩展已被弃用，取而代之的是 [Adobe Experience Platform Web SDK](../web-sdk/overview.md).

此扩展的功能将移植到新扩展上。以下是当前功能的快速比较。

| Platform演示扩展 | 平台Web SDK |
| ------------------ | ----------- |
| 支持自定义客户 ID | 支持自定义客户 ID |
| XDM的客户端映射UI | 在 ECID 中构建（无需 visitor.js） |
| 能够创建流连接 | 选择加入支持 |
| | XDM 支持作为数据元素 |
| | 第一方域支持 |
| | 内置调试工具 |
| | 自动收集浏览器上下文 |
| | 完全开放源 |


## 配置 Adobe Experience Platform 扩展

此部分提供有关配置 Adobe Experience Platform 扩展时可用的选项的参考。

如果尚未安装Adobe Experience Platform扩展，请打开您的资产，然后选择 **[!UICONTROL “扩展”>“目录”]**，将鼠标悬停在Adobe Experience Platform扩展上，然后选择 **[!UICONTROL 安装]**.

要配置该扩展，请打开 [!UICONTROL 扩展] 选项卡，将鼠标悬停在该扩展上，然后选择 **[!UICONTROL 配置]**.

![](../../../images/adobe-experience-platform-extension-configuration.png)

### 流连接

要开始将数据流式传输到 Adobe Experience Platform，第一步便是选择一个流连接。您可以从流连接组合框中选择一个。流连接为必填字段。如果尚未创建任何流连接，则可以通过选择 **[!UICONTROL 创建流连接]** 按钮。

如果您选择 **[!UICONTROL 创建流连接]** 此时将显示一个模式窗口。

![](../../../images/adobe-experienc-platform-create-streaming-connection.png)

该模式窗口中包含预先填充了值的字段，您可以根据需要更改这些值。如果您计划创建多个流连接，则应当注意 **[!UICONTROL 数据源]** 字段必须唯一。 尝试使用创建另一个流连接 **[!UICONTROL 数据源]** 已用于其他连接将失败。

选择流端点后，您将需要提供流端点 URL 和源。

![](../../../images/adobe-experience-platform-streaming-endpoint-selected.png)

## Adobe Experience Platform 扩展操作类型

此部分介绍 Adobe Experience Platform 扩展中可用的操作类型。

### Send Beacon {#send-beacon}

这是为将数据发送到 Adobe Experience Platform 而将使用的操作类型。

![](../../../images/adobe-experience-platform-send-beacon-dataset.png)

您首先需要选择一个将存储数据的数据集。通常，数据集表示将存储通过流连接发送的数据的表格。使用此操作类型前，您需要在 Adobe Experience Platform 中创建数据集。

![](../../../images/adobe-experience-platform-send-beacon-dataset-selected1.png)

在选择了将要存储数据的数据集后，您将会看到有关已链接到选定数据集的架构的详细信息。

### 架构映射

选择数据集后，您可以定义架构映射。

![](../../../images/adobe-experience-platform-send-beacon-schema-mapping.png)

源值字段可接受值或数据元素。您可以通过选择位于源值字段旁边的数据元素按钮来添加数据元素。

目标架构字段包含数据集架构中定义的XDM字段的路径。 对于在更深层架构层次结构中定义的字段，您可以使用圆点作为路径各部分之间的分隔符(例如 （例如 timeSeriesEvents.eventType）。

### 架构字段选择器

通过该扩展，还可以使用可视选择器来选择目标架构字段。如果选择位于目标架构字段输入旁边的目标按钮，则将显示一个模式窗口，您会在该窗口中看到数据集的架构树。您可以选择一个字段，然后选择 **Select** 按钮，此时目标架构字段输入将会更新，并包含正确的 XDM 路径。

![](../../../images/adobe-experience-platform-send-beacon-schema-field-selector.png)

### Adobe Experience Platform 内的标识字段

记录数据架构和时序数据架构可以包含一个或多个标识字段。 标识字段可拼合到一起组成一个主体的单一标识表示形式，这些字段中包含如下信息：CRM 标识符、Experience Cloud ID (ECID)、浏览器 Cookie、广告 ID 或不同域中的其他 ID 等等。

可以通过以下两种方式在架构内定义标识字段：

1. 记录架构和时序架构都包含一个名为 `xdm:identityMap` 的特殊字段，该字段中可以包含标识映射。
1. 可在架构内将键字段标记为“标识”字段。

### Adobe Experience Platform 扩展内的标识字段

对于每个定义为标识字段的架构字段，都将在架构映射部分中添加一个相应行。添加的每个行中都将包含已填充了相应 XDM 架构路径的目标架构字段。如果您在某个架构字段旁边看到配置文件图标，则可以识别该字段是否还属于标识字段。

![](../../../images/adobe-experience-platform-send-beacon-identity-field.png)

主标识字段始终是必填字段，因此不能从架构映射部分中删除包含这些字段的行。

如果某个架构字段被定义为非主标识字段，则会自动将该字段添加到架构映射部分，但源值输入可以保留为空。该字段可以删除。如果该字段对应的源值输入为空，则将丢弃该字段。

![](../../../images/adobe-experience-platform-send-beacon-identity-field-warning.png)

在每个不含值的非主标识字段旁边，您将看到一个警告图标。

如果您的架构中包含 `xdm:identityMap` 字段，则将显示一个标识部分。如果您希望使用 `xdm:identityMap` 发送与标识相关的数据，则可以使用此部分。

![](../../../images/adobe-experience-platform-send-beacon-identity-section.png)

标识映射部分可以包含多个行。每行可以定义一个特定标识类型。您可以为标识定义以下属性：类型、已验证状态、主标识和值。

如果标识映射部分中有多个标识，则只能将一个标识标记为主标识。

如果您的架构具有 `xdm:identityMap` 字段并同时另一个字段标记为主标识字段，则标识映射部分内的主列将不可见。

![](../../../images/adobe-experience-platform-send-beacon-identity-section-not-primary.png)

### 必填字段

某些架构将具有顶级必填字段。 最常见的顶级必填字段为 `timestamp` 和 `_id`。如果未定义这两个字段，信标将无法正常运行。您可以在架构映射部分中定义它们。

如果您的架构映射部分中未包含 `timestamp` 或 `_id`，但数据集架构需要使用这两个字段，则 Adobe Experience Platform 扩展将发送包含自动生成值的信标，以便信标可以正常运行。仅当未在架构映射部分中定义这两个字段时，才会将自动生成的值添加到信标数据中。
