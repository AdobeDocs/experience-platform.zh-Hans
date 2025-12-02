---
title: “摘要”选项卡
description: 了解如何使用Adobe Experience Platform Debugger中的“摘要”选项卡。
keywords: debugger;experience Platform Debugger 扩展程序;chrome;扩展程序;摘要;调试;请求;摘要屏幕;解决方案;信息;analytics;target;dtm;audience manager;launch;id 服务
seo-description: Experience Platform Debugger Summary Screen
seo-title: Summary Tab
uuid: 46b17eaa-b611-43cf-8c6a-67b2e9b9d940
exl-id: 91234125-15c4-4111-9ee4-f3af093a3c4d
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 85%

---

# “摘要”选项卡

要运行Adobe Experience Platform Debugger，请在浏览器中打开要检查的页面，然后选择浏览器栏上的图标(![](images/start-icon.jpg))。 扩展将在&#x200B;**摘要**&#x200B;选项卡上打开。

![](images/summary.jpg)

这个屏幕可显示有关每个 Adobe Experience Cloud 解决方案的信息。所显示的信息因解决方案而异，但通常包括的信息有：解决方案库和版本（例如“AppMeasurement v2.9”），以及帐户标识符（例如 Analytics 报表包 ID、Target 客户端代码、Audience Manager 合作伙伴 ID 等）

## Experience Platform Debugger 中显示的信息

Experience Platform Debugger 将显示每个解决方案的以下信息：

**Adobe Analytics**

<table id="table_BEB9CC58E59D4D86BC895A8A51D84A2C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>报表包 </p> </td> 
   <td colname="col2"> <p><a href="https://experiencecloud.adobe.com/resources/help/zh_CN/reference/report_suites_admin.html" format="html" scope="external">报表包</a>可以针对选定的一个网站、一组网站或网页的子集，定义完整、独立的报表 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>版本 </p> </td> 
   <td colname="col2"> <p>为页面定义的 <a href="https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hans" format="html" scope="external">AppMeasurement</a> 版本 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>访客版本 </p> </td> 
   <td colname="col2"> <p><a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html?lang=zh-Hans" format="html" scope="external">访客 ID</a> 库的版本。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>页面名称 </p> </td> 
   <td colname="col2"> <p>发送到 Analytics 的包含网站用户友好名称的 <a href="https://experiencecloud.adobe.com/resources/help/zh_CN/sc/implement/pageName.html" format="html" scope="external"> pageName</a> 变量。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>模块 </p> </td> 
   <td colname="col2"> <p>Adobe Analytics 加载的模块 </p> </td> 
  </tr> 
 </tbody> 
</table>

**Audience Manager**

<table id="table_784AEABADBDA4D14BB9A7A9CB9EF07C3"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>合作伙伴 </p> </td> 
   <td colname="col2"> <p>DIL 实例的<a href="https://experiencecloud.adobe.com/resources/help/zh_CN/aam/r_dil_get_partner.html" format="html" scope="external">合作伙伴名称</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>版本 </p> </td> 
   <td colname="col2"> <p>DIL 实例的<a href="https://experiencecloud.adobe.com/resources/help/zh_CN/aam/r_api_return_versions_dil.html" format="html" scope="external">版本号</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>UUID </p> </td> 
   <td colname="col2"> <p>与 DIL 实例关联的<a href="https://experiencecloud.adobe.com/resources/help/zh_CN/aam/ids-in-aam.html" format="html" scope="external">唯一用户 ID</a> </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Platform标记**

<table id="table_E9574975444A407887E26514D1BB1601"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>名称 </p> </td> 
   <td colname="col2"> <p>标记<a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=zh-Hans" format="https" scope="external">属性</a>的名称 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>版本 </p> </td> 
   <td colname="col2"> <p>Turbine</a>的版本 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>内部版本发布日期 </p> </td> 
   <td colname="col2"> <p>标记<a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html?lang=zh-Hans" format="https" scope="external">库</a>生成日期 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>环境 </p> </td> 
   <td colname="col2"> <p>标记库使用的<a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=zh-Hans#" format="https" scope="external">环境</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>扩展 </p> </td> 
   <td colname="col2"> <p>页面上使用的扩展 </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Platform Web SDK**

<table id="table_DC76D63FA6EF4891906B9E1D3E4A8A6C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>库版本 </p> </td> 
   <td colname="col2"> <p>Adobe Experience Platform Web SDK <a href="/help/collection/js/release-notes.md" format="html" scope="external">库版本</a>的编号 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>命名空间</p> </td> 
   <td colname="col2"> <p>扩展中标识的名称</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>资产 ID </p> </td> 
   <td colname="col2"> <p>扩展中指定的标记属性的名称 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>边缘域 </p> </td> 
   <td colname="col2"> <p>Adobe Experience Platform 扩展发送和接收数据的域 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>IMS 组织 ID </p> </td> 
   <td colname="col2"> <p>您希望将数据发送到的 Adobe 组织（在扩展中指定） </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>已启用日志记录 </p> </td> 
   <td colname="col2"> <p>指定是否已为此资产启用日志记录</p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Cloud ID 服务**

<table id="table_274CFCEFA8F34D16BB546B4669EC0209"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Experience Cloud 组织 ID </p> </td> 
   <td colname="col2"> <p>您的<a href="https://experiencecloud.adobe.com/resources/help/zh_CN/mcvid/" format="https" scope="external">组织 ID</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>版本 </p> </td> 
   <td colname="col2"> <p><a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html?lang=zh-Hans" format="html" scope="external">访客 ID</a> 库的版本 </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Target**

<table id="table_D30E0CD20FB04E41862B22655136E043"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>客户端代码 </p> </td> 
   <td colname="col2"> <p>您的 Target <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/deploy-at-js/implementing-target-without-a-tag-manager.html?lang=zh-Hans" format="html" scope="external">客户端代码</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>版本 </p> </td> 
   <td colname="col2"> <p>您当前的 <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/target-atjs-versions.html?lang=zh-Hans" format="html" scope="external">at.js</a> 或 mbox.js 版本 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>全局请求名称 </p> </td> 
   <td colname="col2"> <p><a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html?lang=zh-Hans" format="html" scope="external">全局 Mbox</a> 是指在您实施的 Target 中，每个网页顶部发出的单个服务器调用 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>页面加载事件 </p> </td> 
   <td colname="col2"> <p>页面加载时触发的<a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html?lang=zh-Hans" format="html" scope="external">事件</a>类型 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>请求名称 </p> </td> 
   <td colname="col2"> <p>页面上某个<a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html?lang=zh-Hans" format="html" scope="external">位置</a>周围的请求名称。仅当您在代码或标签管理器中实施调试事件侦听器，并在 Target UI 中打开必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans" format="html" scope="external">响应令牌</a>时，才能在无需进行身份验证的情况下可用。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>活动名称 </p> </td> 
   <td colname="col2"> <p>Target <a href="https://experienceleague.adobe.com/docs/target/using/activities/activities.html?lang=zh-Hans" format="html" scope="external">营销活动或活动</a>的名称。仅当您在代码或标签管理器中实施调试事件侦听器，并在 Target UI 中打开必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans" format="html" scope="external">响应令牌</a>时，才能在无需进行身份验证的情况下可用。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>活动 ID </p> </td> 
   <td colname="col2"> <p>Target 活动的 ID。仅当您在代码或标签管理器中实施调试事件侦听器，并在 Target UI 中打开必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans" format="html" scope="external">响应令牌</a>时，才能在无需进行身份验证的情况下可用。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>体验名称 </p> </td> 
   <td colname="col2"> <p>Target <a href="https://experienceleague.adobe.com/docs/target/using/experiences/experiences.html?lang=zh-Hans" format="html" scope="external">体验</a>的名称。仅当您在代码或标签管理器中实施调试事件侦听器，并在 Target UI 中打开必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans" format="html" scope="external">响应令牌</a>时，才能在无需进行身份验证的情况下可用。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>体验 ID </p> </td> 
   <td colname="col2"> <p>Target 体验的 ID。仅当您在代码或标签管理器中实施调试事件侦听器，并在 Target UI 中打开必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans" format="html" scope="external">响应令牌</a>时，才能在无需进行身份验证的情况下可用。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>产品建议名称</p> </td> 
   <td colname="col2"> <p>Target <a href="https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=zh-Hans" format="html" scope="external">产品建议</a>的名称。仅当您在代码或标签管理器中实施调试事件侦听器，并在 Target UI 中打开必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans" format="html" scope="external">响应令牌</a>时，才能在无需进行身份验证的情况下可用。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>产品建议 ID </p> </td> 
   <td colname="col2"> <p>Target 产品建议的 ID。仅当您在代码或标签管理器中实施调试事件侦听器，并在 Target UI 中打开必要的<a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans" format="html" scope="external">响应令牌</a>时，才能在无需进行身份验证的情况下可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>
