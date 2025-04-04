---
title: 使用Adobe Experience Platform Debugger测试Adobe Target实施
description: 了解如何使用Adobe Experience Platform Debugger测试和调试通过Adobe Target启用的网站。
exl-id: f99548ff-c6f2-4e99-920b-eb981679de2d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 2%

---

# 使用Adobe Experience Platform Debugger测试Adobe Target实施

Adobe Experience Platform Debugger提供了一套有用的工具，可用于测试和调试使用Adobe Target实施进行工具的网站。 本指南介绍了在启用了Target的网站上使用Experience Platform Debugger的一些常见工作流程和最佳实践。

## 先决条件

要使用Experience Platform Debugger for Target，网站必须使用[at.js库](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/)版本1.x或更高版本。 不支持以前的版本。

## 初始化Experience Platform Debugger

在浏览器中打开要测试的网站，然后打开Experience Platform Debugger扩展。

在左侧导航中选择&#x200B;**[!DNL Target]**。 如果Experience Platform Debugger检测到网站上正在运行兼容版本的at.js，则会显示Adobe Target实施详细信息。

![在Experience Platform Debugger中选择的Target视图，表示Adobe Target在当前查看的浏览器页面上处于活动状态](../images/solutions/target/target-initialized.png)

## 全局配置信息

在Experience Platform Debugger中，有关实施全局配置的信息显示在Target视图的顶部。

![Experience Platform Debugger中高亮显示的Target全局配置信息](../images/solutions/target/global-config.png)

| 名称 | 描述 |
| --- | --- |
| 客户端代码 | 用于标识贵组织的唯一ID。 |
| 版本 | 网站上当前安装的Adobe Target库的版本。 |
| 全局请求名称 | Target实施的[全局mbox](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?)的名称，默认名称为`target-global-mbox`。 |
| 页面加载事件 | 布尔值，指示是否已发生[页面加载事件](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams)。 只有at.js 2.x支持页面加载事件。对于不兼容的版本，此值默认为`None`。 |

{style="table-layout:auto"}

## [!DNL Network Requests] {#network}

选择&#x200B;**[!DNL Network Requests]**&#x200B;以查看页面上发出的每个网络请求的摘要信息。

![在Experience Platform Debugger中选择的Target的[!DNL Network Requests]部分](../images/solutions/target/network-requests.png)

当您在页面上执行操作（包括重新加载页面）时，新列将自动添加到表中，允许您查看操作的顺序以及每个请求之间值的更改方式。

![在Experience Platform Debugger中选择的Target的[!DNL Network Requests]部分](../images/solutions/target/new-request.png)

捕获以下值：

| 名称 | 描述 |
| --- | --- |
| [!DNL Page Title] | 发起此请求的页面的标题。 |
| [!DNL Page URL] | 发起请求的页面的URL。 |
| [!DNL URL] | 请求的原始URL。 |
| [!DNL Method] | 请求的HTTP方法。 |
| [!DNL Query String] | 请求的查询字符串，获取自URL。 |
| [!DNL POST Body] | 请求正文（仅为POST请求设置）。 |
| [!DNL Pathname] | 请求URL的路径名。 |
| [!DNL Hostname] | 请求URL的主机名。 |
| [!DNL Domain] | 请求URL的域。 |
| [!DNL Timestamp] | 请求（或事件）在浏览器时区中发生的时间戳。 |
| [!DNL Time Since Page Load] | 自页面在请求时首次加载以来经过的时间。 |
| [!DNL Initiator] | 请求的发起者。 换句话说，是谁提出这个请求的？ |
| [!DNL clientCode] | 贵组织帐户的标识符，由Target识别。 |
| [!DNL requestType] | 用于请求的API。 如果使用at.js 1.x，则值为`/json`。 如果使用at.js 2.x，则值为`delivery`。 |
| [!DNL Audience Manager Blob] | 提供有关加密的Audience Manager元数据（称为“blob”）的信息。 |
| [!DNL Audience Location Hint] | 数据收集区域 ID。这是用于标识特定ID服务数据中心的地理位置的数字标识符。 有关详细信息，请参阅[DCS区域ID、位置和主机名](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=zh-Hans)上的Audience Manager文档以及[`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html#reference-a761030ff06c4439946bb56febf42d4c)上的Experience Cloud Identity Service指南。 |
| [!DNL Browser Height] | 浏览器高度（像素）。 |
| [!DNL Browser Time Offset] | 浏览器与其时区关联的时间偏移。 |
| [!DNL Browser Width] | 浏览器宽度（像素）。 |
| [!DNL Color Depth] | 屏幕的颜色深度。 |
| [!DNL context] | 一个对象，其中包含有关用于发出请求的浏览器的上下文信息，包括屏幕维度和客户端平台。 |
| [!DNL prefetch] | 在`prefetch`处理期间使用的参数。 |
| [!DNL execute] | `execute`处理期间使用的参数。 |
| [!DNL Experience Cloud Visitor ID] | 如果检测到一个，请提供有关分配给当前网站访客的[Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hans)的信息。 |
| [!DNL experienceCloud] | 保存此特定用户会话的Experience Cloud ID：A4T [补充数据ID](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?#section_2C1F745A2B7D41FE9E30915539226E3A)和[访客ID (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hans)。 |
| [!DNL id] | 访客的[目标ID](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID)。 |
| [!DNL Mbox Host] | 发出Target请求的[主机](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html)。 |
| [!DNL Mbox PC] | 一个字符串，用于封装[`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/)会话ID和[Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934)位置提示。 at.js使用此值来确保会话和Edge位置保持粘性。 |
| [!DNL Mbox Referrer] | 特定[`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/)请求的URL反向链接。 |
| [!DNL Mbox URL] | [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/)服务器的URL。 |
| [!DNL Mbox Version] | 正在使用的[`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/)版本。 |
| [!DNL mbox3rdPartyId] | 分配给当前访客的[`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html)。 |
| [!DNL mboxRid] | [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/)请求编号。 |
| [!DNL requestId] | 请求的唯一ID。 |
| [!DNL Screen Height] | 屏幕的高度（像素）。 |
| [!DNL Screen Width] | 屏幕的宽度（像素）。 |
| [!DNL Supplemental Data ID] | 系统生成的ID，用于将访客与相应的Adobe Target和Adobe Analytics调用进行匹配。 有关详细信息，请参阅[A4T疑难解答指南](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?#section_75002584FA63456D8D9086172925DD8D)。 |
| [!DNL vst] | [Experience Cloud Identity服务API配置](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html)。 |
| [!DNL webGLRenderer] | 提供页面上使用的WebGL渲染器的相关信息（如果适用）。 |

{style="table-layout:auto"}

要查看特定网络事件上某个参数的详细信息，请选择相关表单元格。 此时会出现一个弹出窗口，其中提供了有关该参数的更多信息，包括描述及其值。 如果值是JSON对象，则该对话框包含对象结构的完全可导航视图。

![在Experience Platform Debugger中选择的Target的[!DNL Network Requests]部分](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

选择&#x200B;**[!DNL Configuration]**&#x200B;以启用或禁用Target的其他调试工具选择。

![在Experience Platform Debugger中选择的Target的[!DNL Configuration Requests]部分](../images/solutions/target/configuration.png)

| 调试工具 | 描述 |
| --- | --- |
| [!DNL Target Console Logging] | 启用后，允许您在浏览器的控制台选项卡中访问at.js日志。 还可通过向浏览器URL添加`mboxDebug`查询参数（具有任何值）来启用此功能。 |
| [!DNL Target Disable] | 启用后，页面上的所有Target功能都将禁用。 这可用于确定特定于Target的选件是否是导致页面上出现问题的原因。 |
| [!DNL Target Trace] | **注意**：您必须登录才能启用此功能。<br><br>启用后，跟踪令牌将随每次请求一起发送，并且在每次响应中返回跟踪对象。 `at.js`解析响应`window.__targetTraces`。 每个跟踪对象包含的信息与[[!DNL Network Requests]选项卡]相同，还包含以下附加内容：<ul><li>配置文件快照，允许您查看请求之前和请求之后的属性。</li><li>匹配和不匹配的[活动](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html)，显示当前配置文件符合或不符合特定活动资格的原因。<ul><li>这有助于确定在给定时间配置文件符合哪些受众资格及其原因。</li><li>Target文档包含有关不同活动类型的更多信息</li></ul></li></ul> |

{style="table-layout:auto"}
