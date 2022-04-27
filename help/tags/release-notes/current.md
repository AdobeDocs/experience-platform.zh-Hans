---
title: 标记发行说明
description: Adobe Experience Platform 中的标记的最新发行说明。
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: a15b5525d3a2fa034715803c83dc22a94915347e
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 7%

---

# Adobe Experience Platform中标记的发行说明

>[!NOTE]
>
>Adobe Experience Platform Launch正在Experience Platform中被重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../term-updates.md)。

## 2021 年 11 月 15 日

**在标记中接受ES6代码**  — 现在，可在标记中使用包含ES6代码的扩展和自定义代码。 在扩展目录中，您将在每个包含ES6代码的扩展的卡片中看到一个ES6+标签。 IE10和IE11不支持ES6代码。 在标记库中使用ES6代码之前，请尽量缩短。

**将Terser用作JavaScript压缩程序** - Uglifier已被替换为Terser。 从此版本开始，所有标记库都将由Terser缩小。

## 2021 年 10 月 21 日

**在事件转发中向经过验证的端点发送数据**  — 使用密钥，您可以向需要以下身份验证协议的端点发送数据：

* **[!UICONTROL 令牌]**:表示身份验证令牌值的单个字符串。
* **[!UICONTROL 简单HTTP]**:包含用户名和密码的两个字符串属性。
* **[!UICONTROL OAuth2]**:包含多个属性以支持 [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749) 规范。

有关更多信息，请参阅 [在数据收集UI中管理密钥](../ui/event-forwarding/secrets.md) 或 [在Reactor API中管理密钥](../api/guides/secrets.md).

## 2021 年 7 月 19 日

**对“管理资产”权限的调整** - “管理属性”权限遇到一个问题，即用户有权创建新属性，但在创建后却无法看到该属性（如社区线程中所述） [此处](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/technical-advisory-adjustments-to-the-manage-properties/ba-p/399176))。 现在，已实施修复，并按照文章中所述强制实施权限。

>[!NOTE]
>
>如果您将新的“编辑属性”权限分配给用户组，则UI将不会更新，以启用属性配置屏幕中的字段。 此问题的修复将在即将发布的版本中实施。

## 2021 年 5 月 17 日

**更好地处理未保存的更改**  — 过去，每当您离开设置视图（扩展、数据元素和规则组件）时，系统都会提示您是否要放弃更改。 但确定这一点的逻辑并不好，因此大多数情况下，系统会提示您保存更改，即使没有更改。  已经修复了。  从现在开始，您只应在实际进行更改时看到该提示。

## 2021 年 5 月 10 日

**简化的发布**  — 不再需要构建到暂存环境。  如果您拥有相应的权限，则可以完全跳过已提交状态，并直接从开发中发布，前提是您已成功构建并且上游没有其他库。

## 2021年4月22日

**在Adobe Experience Platform中收集数据**  — 向Adobe发送数据不仅仅是将标记部署到您的网站或将配置部署到应用程序。  使用Experience PlatformSDK和边缘网络需要访问其他平台功能。  过去，这需要登录到几个不同的工具，但现在它们在一起。

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

**正式发布：事件转发** 将事件级数据发送到Adobe Experience Platform边缘网络，然后使用事件转发以较低的延迟，通过Adobe的服务器（而非客户端）来转换、扩充该数据，并将其发送到非Adobe端点。

请参阅 [事件转发概述](../ui/event-forwarding/overview.md) 和 [入门指南](../ui/event-forwarding/getting-started.md) 以了解更多信息。
