---
title: 发行说明
description: Adobe Experience Platform中标记的最新发行说明。
source-git-commit: 7a6bec77895458cf1735bc7a00d16b78df9776a5
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 2%

---

# 发行说明

>[!NOTE]
>
>Adobe Experience Platform Launch正在Experience Platform中被重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../term-updates.md)。

## 2021 年 5 月 17 日

**更好地处理未保存的更改**  — 过去，每当您从设置视图（扩展、数据元素和规则组件）导航离开时，系统都会提示您是否要放弃更改。但确定这一点的逻辑并不好，因此大多数情况下，系统会提示您保存更改，即使没有更改。  已经修复了。  从现在开始，您只应在实际进行更改时看到该提示。

## 2021 年 5 月 10 日

**简化的发布**  — 不再需要构建到暂存环境。如果您拥有相应的权限，则可以完全跳过已提交状态，并直接从开发中发布，前提是您已成功构建并且上游没有其他库。

## 2021年4月22日

**在Adobe Experience Platform中收集数据**  — 将数据发送到Adobe不仅仅是将标记部署到网站或将配置部署到应用程序。使用Experience PlatformSDK和边缘网络需要访问其他平台功能。  过去，这需要登录到几个不同的工具，但现在它们在一起。

Platform中的数据收集包含六项功能，您新近简化的导航将只包含您的公司和用户帐户有权访问的项目。  某些功能名称也已更新，以匹配Experience Platform的命名模式。

* 客户端（以前作为客户端访问）
* 数据流（以前作为边缘配置访问）
* 服务器（以前作为服务器端访问）
* 应用程序配置
* 架构
* 标识

随着Experience Platform和数据收集的不断发展，期待进行更多更新。

## 2021年2月18日

* 更新了数据收集UI以反应频谱v3
* 已将扩展卡更新为最新的频谱模式
* 增加了整个应用程序中名称字段的大小

## 2021 年 1 月 13 日

**正式发布：事件** 转发将事件级别的数据发送到Adobe Experience Platform边缘网络，然后使用事件转发以较低的延迟，通过Adobe的服务器（而非客户端）来转换、扩充该数据，并将其发送到非Adobe端点。

有关更多信息，请参阅[事件转发概述](../ui/event-forwarding/overview.md)和[快速入门指南](../ui/event-forwarding/getting-started.md) 。
