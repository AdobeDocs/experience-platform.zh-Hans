---
keywords: destinations;destination;destinations detail page;destinations details page
title: “目标：详细信息”页
seo-title: “目标：详细信息”页
description: '单个目标的详细信息页面提供了目标详细信息的概述，如目标名称、ID、映射到目标的区段，以及用于编辑激活和启用和禁用数据流的控件。 '
seo-description: '单个目标的详细信息页面提供了目标详细信息的概述，如目标名称、ID、映射到目标的区段，以及用于编辑激活和启用和禁用数据流的控件。 '
translation-type: tm+mt
source-git-commit: 9bd893820c7ab60bf234456fdd110fb2fbe6697c
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 1%

---


# 目标详细信息页 {#destinations-details-page}

单个目标的详细信息页面提供了目标详细信息的概述，如目标名称、ID、映射到目标的区段，以及用于编辑激活和启用和禁用数据流的控件。 要视图这些详细信息， **[!UICONTROL 请转到]** “目 **[!UICONTROL 标]** ”>“浏览”，然后单击要处理的目标的名称。

单个目标的核心组件有：

* 1 —— 目标名称和ID
* 2 —— 已激活到目标的区段
* 3 —— 右边栏信息
* 4 —— 用于编辑激活和启用／禁用数据流的控件

![目标页面编号](/help/rtcdp/destinations/assets/destination-page-numbered.png)

导航到单个目标页面，以获得目标详细信息的概述，例如：

## 1.目标名称和ID

您可以在页面标题中看到目标名称，在页面URL中看到目标ID。

## 2.已激活至目标的区段

此部分显示当前映射到目标的区段，以及有关这些区段的更多信息。 有关更多信息，请参见下表：

| 项目 | 描述 |
---------|----------|
| 区段名称 | 区段的名称。 |
| 区段描述 | 区段的描述。 |
| 开始日期 | 将这些区段激活到目标的日期。 |
| 结束日期 | 这些区段停止激活到目标的日期。 |
| 映射ID | *不适用于电子邮件营销目标*。 指示在目标平台中区段的已知ID。 |

## 3.右边栏信息

右边栏包含有关目标的信息。 有关更多信息，请参阅下表：

| 项目 | 描述 |
---------|----------|
| 平台 | 表示受众被发送到的目标平台。 请参 [阅目标目录](/help/rtcdp/destinations/destinations-catalog.md) ，了解更多信息。 |
| 描述 | 您可以编辑目标流的描述。 |
| 类别 | 指示目标的类型。 请参 [阅目标目录](/help/rtcdp/destinations/destinations-catalog.md) ，了解更多信息。 |
| 连接类型 | 指示将受众发送到目标的表单。 可以是 [!UICONTROL Cookie] 或 [!UICONTROL 基于用户档案]。 |
| 频度 | 指示受众发送到目标的频率。 可以是 [!UICONTROL 流] 或 [!UICONTROL 批处理]。 |
| 身份 | 表示目标接受的标识命名空间。 例如，“身份”字段可以是GAID、IDFA、电子邮件。 有关所有已接受的身份命名空间，请参阅“身份命名空间”概 [述中的标准命名空间](../../identity-service/namespaces.md)。 |
| 创建者 | 指示创建此目标流的用户。 |
| 已创建 | 指示创建此目标流的UTC日期和时间。 |

## 4.用于编辑激活和启用／禁用数据流的控件

编辑激活控件允许您编辑映射到目标的区段。 按编辑激活以打开段 [激活工作流](/help/rtcdp/destinations/activate-destinations.md)。

使用启 **用／禁用** 切换到开始，并暂停数据导出到目标。