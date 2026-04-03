---
title: 解决数据收集中的身份问题
description: 诊断Web SDK实施中的常见身份问题，包括访客虚增、ECID不一致、Cookie冲突和FPID问题。
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# 解决数据收集中的身份问题

身份问题通常表现为下游报表中的症状（访客计数夸大、配置文件碎片或个性化受损），而不是实施本身中的错误。 此页可帮助您诊断和解决Web SDK实施中最常见的身份问题。 有关标识在数据收集中如何工作的背景，请参阅[标识概述](./overview.md)。

## 检查标识值 {#inspect-identity}

在对特定问题进行故障诊断之前，请检索Web SDK当前使用的身份值。 使用[`getIdentity`](/help/collection/js/commands/getidentity.md)命令查看ECID和其他标识信号：

```js
alloy("getIdentity", { namespaces: ["ECID", "CORE"] }).then(function(result) {
  console.log("ECID:", result.identity.ECID);
  console.log("CORE ID:", result.identity.CORE);
  console.log("Edge region:", result.edge.regionID);
});
```

您还可以在浏览器的开发人员工具中检查标识值：

1. 打开&#x200B;**应用程序**&#x200B;选项卡(Chrome/Edge)或&#x200B;**存储**&#x200B;选项卡(Firefox/Safari)。
2. 在您的域中查找前缀为`kndctr_`的Cookie。 `kndctr_<ORG_ID>_AdobeOrg_identity` Cookie包含ECID。
3. 打开&#x200B;**网络**&#x200B;选项卡并找到`interact`或`collect`请求，以访问Edge Network。 检查`identityMap`的请求有效负载和标识句柄的响应有效负载。

## 常见问题 {#common-issues}

+++**访客计数虚增**

**症状**： Analytics报表显示的独特访客比预期要多，或者同一人员跨会话显示为多个访客。

**可能的原因**：

| 原因 | 如何识别 | 解决方法 |
| --- | --- | --- |
| Cookie生命周期短 | 检查浏览器中`kndctr_`个Cookie的过期时间。 如果它们在7天或更短时间内过期，则浏览器策略可能会限制Cookie持续时间。 | 使用DNS A/AAAA记录实施从服务器设置的[第一方设备ID (FPID)](./fpid.md)以获得较长的Cookie持久性。 |
| 第一个请求缺少FPID | 在页面加载时检查第一个Edge Network请求。 如果不存在任何FPID Cookie，则Edge Network会生成一个新的ECID。 如果FPID是在第一个请求之后设置的，则第一个请求中生成的ECID将被孤立。 | 在Web SDK发送其第一个请求之前设置FPID Cookie。 请参阅[何时设置Cookie](./fpid.md#when-to-set-cookie)。 |
| 跨域的`orgId`不匹配 | 跨域比较`orgId`配置值。 不匹配的值会导致单独的标识范围。 | 在您组织内的所有域上使用相同的[`orgId`](/help/collection/js/commands/configure/orgid.md)。 |
| 同意横幅删除Cookie | 如果您的同意实施在授予同意之前清除所有Cookie，然后Web SDK初始化，则生成一个新的ECID。 | 配置您的同意横幅以保留`kndctr_` Cookie，或延迟Web SDK初始化，直到获得同意为止。 另请参阅[同意和标识](./consent.md)。 |
| JavaScript设置的FPID Cookie | 使用`document.cookie`设置的Cookie受浏览器限制(ITP、ETP)的约束，其生命周期有时限制为24小时。 | 使用DNS A/AAAA记录从服务器设置FPID Cookie，而不是从JavaScript设置。 |

+++

+++**ECID在页面之间意外更改**

**症状**： ECID在同一域的不同页面上不同，或在每次加载页面时发生变化。

**诊断步骤**：

1. 确认两个页面上都存在`kndctr_`身份Cookie。 如果某个页面上缺少该变量，请检查是否在该页面上配置了Web SDK。
2. 验证Cookie域的设置是否足够广泛。 在`shop.example.com`上设置的Cookie在`www.example.com`上不可用。 确保第一方收集和Cookie设置基础结构使用相同的域范围。
3. 检查可在导航时清除Cookie的JavaScript（例如，积极的Cookie同意脚本或隐私工具）。
4. 如果使用单页应用程序，请验证是否在应用程序初始化时配置了Web SDK一次，而不是在每次路由更改时都重新初始化。 重新初始化可以生成新的ECID。

+++

+++**FPID没有为ECID**&#x200B;设定种子

**症状**：您已设置FPID Cookie，但`getIdentity`返回的ECID在每次访问中不一致，或者FPID未出现在Edge Network请求有效负载中。

**诊断步骤**：

1. **验证FPID Cookie格式**： FPID必须是有效的[UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122)。 打开浏览器的开发人员工具，找到FPID Cookie，并确认值与模式`xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx`匹配。
2. **检查数据流中的Cookie名称**：如果您使用的是[数据流Cookie方法](./fpid.md#setting-cookie-datastreams)，则数据流中配置的Cookie名称必须与服务器设置的Cookie名称完全匹配。
3. **确认在请求中发送了Cookie**：在“网络”选项卡中，检查Edge Network请求中的`Cookie`标头。 必须包含FPID Cookie。
4. **检查身份优先级**：如果现有ECID已存储在`kndctr_` Cookie中，则它优先于FPID。 只有在不存在现有ECID时，FPID才会种子生成新的ECID。 查看[FPID的工作方式](./fpid.md#how-fpids-work)以了解完整优先级顺序。
5. **验证CNAME**：如果使用数据流Cookie方法，请确认您的第一方收集CNAME已正确配置，请求将通过它路由。

+++

+++**跨域标识不起作用**

**症状**：访客从您的某个域单击到另一个域，即被视为目标域上的新访客。

**诊断步骤**：

1. **检查URL**：当访客单击链接时，检查目标URL。 它必须包含`adobe_mc`查询字符串参数。 如果缺少参数，则源域不会附加该参数。 请参阅[实施跨域共享](./cross-domain-sharing.md#implement-cross-domain-sharing)。
2. **检查时间**： `adobe_mc`参数将在五分钟后过期。 如果加载目标页面耗时过长（例如，由于重定向或网络速度慢），则参数可能会在Web SDK读取之前过期。
3. **验证`orgId`是否匹配**：两个域必须使用相同的[`orgId`](/help/collection/js/commands/configure/orgid.md)。 组织ID不匹配会导致目标域拒绝已切换的身份。
4. **确认Web SDK位于目标**：目标页面必须已安装并配置Web SDK。 如果没有该参数，`adobe_mc`参数将被忽略。
5. **检查URL剥离**：某些重定向服务、CDN或服务器端逻辑剥离未知的查询字符串参数。 验证`adobe_mc`在源页面和目标页面之间的任何中间重定向中是否仍然有效。

+++

+++**移动到Web标识切换失败**

**症状**：在移动应用程序中启动并打开WebView或移动浏览器的访客在Web端被视为新访客。

**诊断步骤**：

1. **验证URL**：记录传递给WebView的URL。 它必须包含由`adobe_mc`[`getUrlVariables`生成的](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables)参数。
2. **检查SDK版本**： Edge Network扩展的移动身份版本必须为1.1.0或更高版本，并且Web SDK版本必须为2.11.0或更高版本。
3. **检查时间**：与跨域共享一样，`adobe_mc`参数将在五分钟后过期。 确保在构建URL后立即加载WebView。
4. **确认`orgId`匹配**： Experience Cloud组织ID在移动设备SDK和Web SDK配置中必须相同。

+++
