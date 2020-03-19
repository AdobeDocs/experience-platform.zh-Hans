---
title: “目标：详细信息”页
seo-title: “目标：详细信息”页
description: '单个目标的详细信息页面提供了目标详细信息的概述，如目标名称、ID、映射到目标的区段以及用于编辑激活和启用数据流的控件。 '
seo-description: '单个目标的详细信息页面提供了目标详细信息的概述，如目标名称、ID、映射到目标的区段以及用于编辑激活和启用数据流的控件。 '
translation-type: tm+mt
source-git-commit: b784b67092ea8d30ad00cda9a40779b3890862fd

---


# “目标详细信息”页 {#destinations-details-page}

单个目标的详细信息页面提供了目标详细信息的概述，如目标名称、ID、映射到目标的区段以及用于编辑激活和启用数据流的控件。 要查看这些详细信息，请转 **到“目标** ”>“浏 **览** ”，然后单击要处理的目标的名称。

单个目标的核心组件有：

* 1 —— 目标名称和ID
* 2 —— 激活到目标的区段
* 3 —— 右侧边栏信息
* 4 —— 用于编辑激活和启用／禁用数据流的控件

![目标页面编号](/help/rtcdp/destinations/assets/destination-page-numbered.png)

导航到单个目标页面，以获取目标详细信息的概述，例如：

## 1.目标名称和ID

您可以在页面标题中查看目标名称，在页面URL中查看目标ID。

## 2.已激活到目标的区段

此部分显示当前映射到目标的区段，以及这些区段的更多信息。 有关更多信息，请参见下表：

| 项目 | 描述 |
---------|----------|
| 区段名称 | 您的区段名称。 |
| 区段描述 | 区段的描述。 |
| 开始日期 | 将这些区段激活到目标的日期。 |
| 结束日期 | 这些区段停止激活到目标的日期。 |
| 映射ID | *不适用于电子邮件营销目标*。 指示在目标平台中区段的已知ID。 |

## 3.右边栏信息

右边栏包含有关目标的信息。 有关详细信息，请参阅下表：

| 项目 | 描述 |
---------|----------|
| 平台 | 表示受众被发送到的目标平台。 有关更 [多信息，请参阅目](/help/rtcdp/destinations/destinations-catalog.md) 标目录。 |
| 描述 | 您可以编辑目标流的描述。 |
| 类别 | 指示目标的类型。 有关更 [多信息，请参阅目](/help/rtcdp/destinations/destinations-catalog.md) 标目录。 |
| 连接类型 | 指示将受众以哪种形式发送到目标。 可以是 **Cookie** ，也 **可以是基于Profile**。 |
| 频度 | 指示将受众发送到目标的频率。 可以是 **流** 或 **批**。 |
| 身份 | 表示目标接受的标识命名空间。 例如，“标识”字段可以是GAID、IDFA、电子邮件。 有关所有已接受的标识命名空间，请参阅标识命名空间概 [述中的标准命名空间](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md)。 |
| 创建者 | 指示创建此目标流的用户。 |
| 已创建 | 指示创建此目标流的UTC日期和时间。 |

## 4.用于编辑激活和启用／禁用数据流的控件

编辑激活控件允许您编辑映射到目标的区段。 按编辑激活以打开区段 [激活工作流](/help/rtcdp/destinations/activate-destinations.md)。

使用“ **启用／禁用** ”切换开始和暂停数据导出到目标。