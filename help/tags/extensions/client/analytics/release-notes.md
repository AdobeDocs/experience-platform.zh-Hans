---
title: Adobe Analytics扩展的发行说明
description: Adobe Experience Platform中的Adobe Analytics标记扩展的最新发行说明。
exl-id: 3c7b4ec0-4b81-4ef4-b15f-6ad102525840
source-git-commit: 5f4e157a39bf927b3821931d55f968862b2ed16d
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 65%

---

# Adobe Analytics扩展发行说明

以下是Adobe Analytics标记扩展的发行说明列表。

>[!NOTE]
>
>Analytics标记扩展(如果经常为响应[AppMeasurementJavaScript库](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hans)的更新而更新)。 有关下面提及的特定版本的详细信息，请参阅[AppMeasurement发行说明](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hans)。

## 2024年10月28日

**Adobe Analytics扩展1.9.6**

**功能**：

* 添加了新功能，允许用户查看和编辑[设置变量操作](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/tags/extensions/client/analytics/overview#set-variables)的JSON版本。 AdobeWeb SDK扩展还包括通过提供JSON [填充Analytics变量](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/tags/extensions/client/web-sdk/data-element-types)的操作。 通过将JSON数据从AA扩展复制到Web SDK扩展，迁移客户可以轻松地同时传输多个设置，而不是手动添加每个变量。

## 2024年8月12日

**Adobe Analytics扩展1.9.5**

**功能**：

* 已升级到[AppMeasurement到v2.27.0](https://github.com/adobe/appmeasurement/releases/tag/v2.27.0)。

## 2024年3月4日

**Adobe Analytics扩展1.9.4**

**功能**：

* 已升级到[AppMeasurement到v2.26.0](https://github.com/adobe/appmeasurement/releases/tag/v2.26.0)。

## 2023年9月15日

**Adobe Analytics扩展1.9.3**

**功能**：

* 已升级到[AppMeasurement到v2.25.0](https://github.com/adobe/appmeasurement/releases/tag/v2.25.0)。


## 2023年7月19日

**Adobe Analytics扩展1.9.2**

**功能**：

* 已升级到[AppMeasurementv2.24.0](https://github.com/adobe/appmeasurement/releases/tag/v2.24.0)。
* 添加了可选配置（`decodeLinkParameters`默认`false`），该配置对包含双字节编码字符的链接URL进行解码。

**错误修复**：

* 为具有错误的高熵[用户代理客户端提示](https://experienceleague.adobe.com/docs/analytics/technotes/client-hints.html?lang=zh-Hans) API的浏览器添加了其他错误处理。
* 已将[POST](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/POST) Content-Type标头更改为默认使用`x-www-form-urlencoded`。

## 2022年9月23日

**Adobe Analytics扩展1.9.1**

**功能**：

* 已升级到AppMeasurementv2.23.0。
* 扩展现在可以收集最新版本的AppMeasurement所支持的高熵[用户代理客户端提示](https://developer.mozilla.org/en-US/docs/Web/HTTP/Client_hints#user-agent_client_hints)。

## 2022年2月28日

**Adobe Analytics扩展1.9.0**

**错误修复**：

* 删除了AppMeasurement中的一些调试语句。

## 2021年11月29日

**Adobe Analytics扩展1.8.8**

**错误修复**：

* 已将AppMeasurement升级到v2.22.3。

## 2021 年 9 月 16 日

**Adobe Analytics扩展1.8.7**

**错误修复**：

* 已将AppMeasurement升级到v2.22.2。
* 删除已弃用的buildInfo.environment

## 2021年8月24日

**Adobe Analytics扩展1.8.6**

**错误修复**：

* 已将[AppMeasurement升级到v2.22.1](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hans)。
* 更新了回退linkName以镜像Activity Map逻辑而不是使用innerHTML。

## 2020 年 8 月 6 日

**Adobe Analytics扩展1.8.5**

**错误修复**：

* 将这个字段留空时，AAM 模块设置中设置的 Cookie 名称会不正确。此问题现已修复。

**功能**：

* [AppMeasurement 已更新至 2.22.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hans)。
* 少量 UI 发生了更改，为此，如今将以可折叠项的形式折叠显示其他设置，而并非显示在复选框中。

## 2020 年 6 月 2 日

**Adobe Analytics扩展1.8.4**

**错误修复**：

* 修复了事件下拉列表中未显示购物车事件（prodView、scAdd、scView 等）的错误。现在，所有这些内容都可以从下拉菜单中进行选择。

**功能**：

* 现在，您无需使用自定义代码即可关闭扩展中的 Activity Map。Activity Map 将作为单独的模块（与 AAM 模块很相似）加载，并且您可以根据需要将其关闭。
* 通过最小化层次结构变量和其他选项来清理 UI。
* 添加了一个字段，用于从扩展配置 UI 设置购买 ID。

## 2020 年 10 月 3 日

**Adobe Analytics扩展1.8.3**

**错误修复**：

* 修复了影响规则配置的错误，当您尝试设置变量时，如果您使用自定义库并且未在 Analytics 中配置报表包，则会引发该错误。
* 创建 eVar 时，出现以下错误：不向您显示用于从 prop 中“删除重复项”的选项，反之亦然。现在已修复此错误，以镜像早期版本中的行为。

**功能**：

* [将 AppMeasurement 更新为 2.20.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hans)

## 2020 年 3 月 2 日

**Adobe Analytics扩展1.8.2**

**错误修复**：

* 修复了对数字事件和序列化货币使用错误语法的问题

**功能**：

* [将 AppMeasurement 更新为 2.18.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hans)
* 将 Audience Manager 模块中的 DIL 库更新为 9.4
* 增加了扩展中输入字段的长度
* 扩展和操作配置中的 eVar 和 prop 现在显示 Analytics 中的友好名称
* 在扩展配置的“Cookie”部分添加了一个复选框，允许您编写安全 Cookie
* 向 Audience Manager 模块添加了三个新配置。添加了用于启用日志记录、启用 URL 目标和启用 Cookie 目标的设置

## 2019 年 11 月 13 日

**Adobe Analytics扩展1.8.1**

**错误修复**：

* 修复了高级 evar 和 prop 无法保存的错误。

## 2019 年 11 月 1 日

**Adobe Analytics扩展1.8.0**

**错误修复**：

* 修复了少数客户在下拉列表中看不到报表包选项的错误
* 修复了使用 ECID 时某些变量设置不正确的错误

**功能**：

* 在扩展视图中按数字对 evar、 prop 和事件进行排序
* 对后端架构进行了更改以支持 Magento 上下文数据

## 2019 年 9 月 6 日

**Adobe Analytics扩展1.7.8**

**错误修复**：

* 修复了某些用户在下拉菜单中看不到报表包选项的错误
* 修复了事件未正确触发的错误

## 2019 年 9 月 5 日

**Adobe Analytics扩展1.7.7**

**功能**：

* 将 AppMeasurement 更新为 2.17
* 更新了“受众管理”模块以支持 DIL 9.3。
* 更新了字段宽度，为您提供更多空间

**错误修复**：

* 修复了设置选择加入/退出的错误
* 修复了使用 ECID 时变量设置不正确的错误

## 2019 年 7 月 18 日

**Adobe Analytics扩展1.7.6**

**功能**：

* 更新了 Adobe Analytics 扩展，以支持用于 Audience Manager 的 DIL 9.2

* 更新了扩展以支持 [AppMeasurement 2.15.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hans#version-2.15.0)
* 移除了以下复选框（因为该复选框不再受支持）：“Do not attach the destination publishing IFRAME to the DOM or fire destinations”

## 2019 年 6 月 4 日

**Adobe Analytics扩展1.7.5**

**功能**：

* 已将 Adobe Analytics 扩展更新至 [AppMeasurement 2.14.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=zh-Hans#version-2.14.0)，该版本修复了一个已知的 clearVars 问题。
* 添加了指向扩展的 Exchange 链接。通过选择相应的下拉菜单并选取“extension info”，可访问 Exchange 列表

**错误修复**：

* 修复了以下错误：用户界面中显示的从列表中删除的 eVar 不正确
* 修复了以下错误：在尝试添加多个报表包时，系统要求使用 SSL 跟踪服务器。添加多个报表包时，虽然需要使用跟踪服务器，但 SSL 跟踪服务器字段是可选的。

## 2019 年 4 月 15 日

**Adobe Analytics扩展1.7.4**

**错误修复**：

* 在 AppMeasurement 2.13.0 中发现存在一个错误后，对扩展进行了回滚。AppMeasurement 2.13.0 会导致无法发送 ECID 的问题，因此如果您安装了 1.7.3，我们建议您升级到 1.7.4 以避免出现此问题。请注意，在发布 AppMeasurement 的更新版本之前，将继续使用 clearVars。

## 2019 年 4 月 12 日

**Adobe Analytics扩展1.7.3**

**错误修复**：

* 已将 Adobe Analytics 扩展更新到 AppMeasurement 2.13.0，该版本修复了已知的 clearVars 问题。

## 2019 年 3 月 21 日

**Adobe Analytics扩展1.7.2**

**功能**：

* 已将 Adobe Analytics 扩展更新到 DIL 9.1。
* 已将 Adobe Analytics 扩展更新到 AppMeasurement 2.12。
* 已将 Adobe Analytics 扩展视图升级为 React-Spectrum。
* 现在，在配置页面中配置报表包时，您将看到一个包含贵公司所有报表包的下拉菜单，以便您更加轻松地选择适当的报表包。

## 2019 年 3 月 7 日

**Adobe Analytics扩展1.7.1**

**错误修复**：

* 在 1.7 中发现存在一个错误后，将扩展回滚到了版本 1.6。

## 2019 年 2 月 11 日

**Adobe Analytics扩展1.6**

**功能**：

* 已将 Adobe Analytics 扩展更新到 DIL 9.0，该版本将支持选择启用。
* 已将 Adobe Analytics 扩展更新到 AppMeasurement 2.11，以支持选择启用。

**错误修复**：

* 修复了原型 JS 存在的冲突。Analytics 扩展现在将支持标准的 prototype.js 库。

## 2018 年 11 月 9 日

**Adobe Analytics扩展1.5.1**

**错误修复**：

* 已将 DIL 模块降级为 7.0，以修复导致 Analytics 信标无法触发的问题

## 2018 年 11 月 5 日

**Adobe Analytics扩展1.5**

**功能**：

* 更新了 Adobe Analytics 扩展，以支持 Audience Manager 中的 DIL 8.0
* 已将“Serialize from value”字段分为“Event ID”和“Event Value”两个字段。这将修复不序列化事件而是分配值的问题
   * 请注意：如果您使用当前字段通过字符串（例如，Event7=3:abc123）添加 ID，则需要更新输入，以便在“Event ID”字段中反映该 ID

**错误修复**：

* 修复了阻止货币代码正确填充的错误

## 2018 年 10 月 11 日

**Adobe Analytics扩展1.4**

**功能**：

* 已将跟踪 Cookie 名称迁移到扩展配置。

**错误修复**：

* 修复了一个错误，以便在没有可用的 trackerProperties 对象时设置变量不会崩溃。

## 2018 年 6 月 5 日

**Adobe Analytics扩展1.3**

**功能**：

* 更新了 Adobe Analytics 扩展以支持 AppMeasurement 2.9。
* 在 Adobe Analytics 扩展中新增了“使跟踪器可全局访问”功能，该功能可在 `windows.s` 下将跟踪器的范围设为全局。

**错误修复**：

* 修复了导致从详细信息视图返回时重置列表视图的错误
* 修复了若干错误，进而改进了修订版本选择器中的资源加载
* 修复了 Adobe Analytics 扩展中多个规则覆盖 s.events 的错误

## 2018 年 3 月 20 日

**Adobe Analytics扩展1.2**

**功能**：

* 已将 AppMeasurement.js 更新到 2.8.0
* 增加了对服务器端转发的支持

## 2018 年 2 月 8 日

**Adobe Analytics扩展1.1**

**功能**：

* 已将 AppMeasurement 更新到版本 2.6
* 现在，在Adobe Experience Platform标记扩展中，已初始化的Analytics跟踪器将通过共享模块公开，这样，其他扩展就可以包含用于与之交互的代码。

**错误修复**：

* 修复了 Adobe Analytics 扩展中导致“错误，AppMeasurement 初始化中缺少报表包 ID”显示在浏览器控制台中的错误。
