---
title: 使用Adobe Experience Platform Debugger测试Adobe Target实施
description: 了解如何使用Adobe Experience Platform Debugger来测试和调试已启用Adobe Target的网站。
source-git-commit: 1ce7ac78936040d76faa3a58b92333a737fbeb66
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 5%

---

# 使用Adobe Experience Platform Debugger测试Adobe Target实施

Adobe Experience Platform Debugger提供了一套有用的工具，用于测试和调试已通过Adobe Target实施进行工具处理的网站。 本指南介绍在启用了Target的网站上使用Platform Debugger的一些常见工作流程和最佳实践。

## 先决条件

要使用Platform Debugger for Target，网站必须使用 [at.js库](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) 版本1.x或更高版本。 不支持以前的版本。

## 初始化Platform Debugger

在浏览器中打开要测试的网站，然后打开Platform Debugger扩展。

选择 **[!DNL Target]** 中。 如果Platform Debugger检测到网站上运行了兼容版本的at.js，则会显示Adobe Target实施详细信息。

![在Platform Debugger中选择的Target视图，指示Adobe Target在当前查看的浏览器页面上处于活动状态](../images/solutions/target/target-initialized.png)

## 全局配置信息

有关实施全局配置的信息会显示在Platform Debugger中Target视图的顶部。

![Platform Debugger中突出显示了Target的全局配置信息](../images/solutions/target/global-config.png)

| 名称 | 描述 |
| --- | --- |
| 客户端代码 | 一个唯一ID，用于标识您的组织。 |
| 版本 | 网站上当前安装的Adobe Target库版本。 |
| 全局请求名称 | 的名称 [全局mbox](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) 对于Target实施，默认名称为 `target-global-mbox`. |
| 页面加载事件 | 一个布尔值，指示 [页面加载事件](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) 已经发生了。 at.js 2.x仅支持页面加载事件。对于不兼容的版本，此值默认为 `None`. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Network Requests] {#network}

选择 **[!DNL Network Requests]** 查看页面上发出的每个网络请求的摘要信息。

![的 [!DNL Network Requests] 部分来查找在Platform Debugger中选择的Target](../images/solutions/target/network-requests.png)

在页面上执行操作（包括重新加载页面）时，会自动将新列添加到表中，从而允许您查看操作顺序以及各个请求之间值的更改方式。

![的 [!DNL Network Requests] 部分来查找在Platform Debugger中选择的Target](../images/solutions/target/new-request.png)

捕获了以下值：

| 名称 | 描述 |
| --- | --- |
| [!DNL Page Title] | 启动此请求的页面的标题。 |
| [!DNL Page URL] | 发起请求的页面的URL。 |
| [!DNL URL] | 请求的原始URL。 |
| [!DNL Method] | 请求的HTTP方法。 |
| [!DNL Query String] | 从URL获取的请求的查询字符串。 |
| [!DNL POST Body] | 请求的正文(仅为POST请求设置)。 |
| [!DNL Pathname] | 请求URL的路径名。 |
| [!DNL Hostname] | 请求URL的主机名。 |
| [!DNL Domain] | 请求URL的域。 |
| [!DNL Timestamp] | 请求（或事件）在浏览器时区内发生的时间戳。 |
| [!DNL Time Since Page Load] | 自页面最初加载到请求时起经过的时间。 |
| [!DNL Initiator] | 请求的发起者。 换句话说，谁提出了这个要求？ |
| [!DNL clientCode] | Target可识别的贵组织帐户的标识符。 |
| [!DNL requestType] | 用于请求的API。 如果使用at.js 1.x，则值为 `/json`. 如果使用at.js 2.x，则值为 `delivery`. |
| [!DNL Audience Manager Blob] | 提供有关称为“blob”的加密Audience Manager元数据的信息。 |
| [!DNL Audience Location Hint] | 数据收集区域 ID。这是用于标识特定 ID 服务数据中心的地理位置的数字标识符。有关更多信息，请参阅Audience Manager文档 [DCS区域ID、位置和主机名](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=zh-Hans) 和上的Experience CloudIdentity Service指南 [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html?lang=en#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | 浏览器高度（以像素为单位）。 |
| [!DNL Browser Time Offset] | 与浏览器时区关联的时间偏移。 |
| [!DNL Browser Width] | 浏览器宽度（以像素为单位）。 |
| [!DNL Color Depth] | 屏幕的颜色深度。 |
| [!DNL context] | 一个对象，其中包含有关用于发出请求的浏览器的上下文信息，包括屏幕尺寸和客户端平台。 |
| [!DNL prefetch] | 在 `prefetch` 正在处理。 |
| [!DNL execute] | 在 `execute` 正在处理。 |
| [!DNL Experience Cloud Visitor ID] | 如果检测到一个，则提供 [Experience CloudID(ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) 分配给当前网站访客的URL。 |
| [!DNL experienceCloud] | 包含此特定用户会话的Experience CloudID:a4T [补充数据ID](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?#section_2C1F745A2B7D41FE9E30915539226E3A)和 [访客ID(ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html). |
| [!DNL id] | 的 [Target ID](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) 对访客。 |
| [!DNL Mbox Host] | 的 [主机](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Target请求所针对的问题。 |
| [!DNL Mbox PC] | 封装 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 会话ID和 [Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934) 位置提示。 at.js会使用此值以确保会话和边缘位置保持粘滞状态。 |
| [!DNL Mbox Referrer] | 特定 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 请求。 |
| [!DNL Mbox URL] | 的URL [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 服务器。 |
| [!DNL Mbox Version] | 的版本 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 正在使用。 |
| [!DNL mbox3rdPartyId] | 的 [`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) 分配给当前访客。 |
| [!DNL mboxRid] | 的 [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) 请求ID。 |
| [!DNL requestId] | 请求的唯一ID。 |
| [!DNL Screen Height] | 屏幕的高度（以像素为单位）。 |
| [!DNL Screen Width] | 屏幕的宽度（以像素为单位）。 |
| [!DNL Supplemental Data ID] | 系统生成的ID，用于将访客与相应的Adobe Target和Adobe Analytics调用进行匹配。 请参阅 [A4T疑难解答指南](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?#section_75002584FA63456D8D9086172925DD8D) 以了解更多信息。 |
| [!DNL vst] | 的 [Experience Cloud标识服务API配置](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html). |
| [!DNL webGLRenderer] | 提供有关页面上使用的WebGL渲染器的信息（如果适用）。 |

{style=&quot;table-layout:auto&quot;}

要查看特定网络事件中参数的详细信息，请选择相关的表单元格。 此时会出现一个弹出窗口，提供有关参数的更多信息，包括描述及其值。 如果值是JSON对象，则该对话框将包含该对象结构的完全可导航视图。

![的 [!DNL Network Requests] 部分来查找在Platform Debugger中选择的Target](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

选择 **[!DNL Configuration]** 可为Target启用或禁用一系列其他调试工具。

![的 [!DNL Configuration Requests] 部分来查找在Platform Debugger中选择的Target](../images/solutions/target/configuration.png)

| 调试工具 | 描述 |
| --- | --- |
| [!DNL Target Console Logging] | 启用后，允许您在浏览器的控制台选项卡中访问at.js日志。 此功能还可以通过添加 `mboxDebug` 查询参数（包含任何值）到浏览器URL。 |
| [!DNL Target Diable] | 启用后，页面上会禁用所有Target功能。 这可用于确定特定于Target的选件是否是导致页面上出现问题的原因。 |
| [!DNL Target Trace] | **注意**:您必须登录才能启用此功能。<br><br>启用后，跟踪令牌将随每次请求一起发送，并在每次响应中返回一个跟踪对象。 `at.js` 解析响应 `window.__targetTraces`. 每个跟踪对象包含与[[!DNL Network Requests] 选项卡，但添加了以下内容：<ul><li>配置文件快照，允许您查看请求前后的属性。</li><li>匹配和不匹配 [活动](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html)，显示当前用户档案没有或没有资格参与特定活动的原因。<ul><li>这有助于确定某个用户档案在给定时间符合哪些受众条件以及原因。</li><li>Target文档包含有关不同活动类型的更多信息</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
