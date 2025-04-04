---
title: Adobe Experience Cloud Identity Service扩展概述
description: 了解Adobe Experience Platform中的Adobe Experience Cloud Identity Service Tag扩展。
exl-id: 9bfcb666-a3f1-46ad-8678-2c63738da2b2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 75%

---

# Adobe Experience Cloud Identity Service扩展概述

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

使用本参考可了解有关配置Adobe Experience Cloud ID扩展以及使用此扩展构建规则时可用的选项的信息。

使用此扩展可将Experience Cloud Identity Service与您的资产相集成。 通过Experience Cloud Identity Service，您可以为网站访客创建并存储唯一的永久标识符。

## 配置 Experience Cloud ID 扩展

此部分提供有关配置 Experience Cloud ID 扩展时可用的选项的参考。

如果尚未安装Experience Cloud ID扩展，请打开您的资产，然后选择&#x200B;**[!UICONTROL 扩展>目录]**，将鼠标悬停在Experience Cloud ID扩展上，然后选择&#x200B;**[!UICONTROL 安装]**。

要配置该扩展，请打开“扩展”选项卡，将鼠标悬停在该扩展上，然后选择&#x200B;**[!UICONTROL 配置]**。

![](../../../images/optin.jpg)

可以使用以下配置选项：

### Experience Cloud Organization ID

您的 Experience Cloud 组织的 ID。

您的 ID 是由 24 个字符组成的字母数字字符串，其后跟 `@AdobeOrg`。如果您不知道此 ID，请联系客户关怀团队。

### Exclude specific paths

如果 URL 与任何指定的路径相匹配，则不会加载 Experience Cloud ID。

（可选）如果这是正则表达式，则启用 Regex。

选择&#x200B;**[!UICONTROL 添加]**&#x200B;以排除其他路径。

### Opt In

使用 Opt In 选项可确定是否要求访客选择启用您网站上的 Adobe 服务，包括是否创建跟踪访客活动的 Cookie。

选择加入是所有Experience Platform解决方案客户端库的集中式引用点，用于确定在访问您的网站时是否可以在用户的设备或浏览器上创建Cookie。 Opt In 不支持收集或存储用户同意首选项。

**Enable Opt In?**

所选选项可确定您的网站是否需要等待同意才能跟踪访客在您的网站上的活动。

有三个选项：

* **No：**&#x200B;无需等待同意即可跟踪访客。如果您未选择任一选项，则这是默认行为。
* **Yes：**&#x200B;需要等待同意才能跟踪访客。
* **Determined at runtime using function：**&#x200B;以编程方式确定在运行时该值是 true 还是 false。如果选择此选项，则 Select Data Element 字段将会变得可用。此时，需选择一个可确定是否等待同意的数据元素。此数据元素解析为布尔值。例如，您可以选择一个根据访客所在国家/地区是否位于欧盟来确定提供同意与否的数据元素。

**Is Opt In Storage Enabled?**

如果启用，则同意将存储在您的域的第一方 Cookie 中。如果未启用，则同意设置将保留在您的 CMP 或由您管理的 Cookie 中。

**Opt In Cookie Domain?**

如果已启用存储，则使用此可选设置可指定存储“选择启用”Cookie 的域。您可以输入域，也可以选择包含该域的数据元素。

**Opt In Storage Expiry?**

指定已启用存储时“选择启用”Cookie 的过期时间（以秒为单位）。

输入一个数字，然后从下拉列表中选择一个时间单位。例如，输入2并选择&#x200B;**[!UICONTROL 周]**。 默认值为 13 个月。

**Permissions?**

将先前的同意传递到“选择启用”库。选择包含该同意的数据元素。元素类型必须是对象或 JSON 字符串。覆盖 Pre Opt In Approvals。

示例：

`"{"aa":true,"aam":true,"ecid":true}"`

**Pre Opt In Approvals?**

定义访客未设置首选项时批准或拒绝的类别。假定从加载页面时起同意所选的解决方案。元素类型必须是对象或 JSON 字符串（示例：`{aam: true}`）。

### Variables

将名称-值对设置为 Experience Cloud ID 实例属性。使用下拉菜单选择一个变量，然后键入或选择一个值。有关每个变量的信息，请参阅[Experience Cloud Identity Service文档](https://experiencecloud.adobe.com/resources/help/zh_CN/mcvid/mcvid-overview.html)。

## Experience Cloud ID 扩展操作类型

此部分介绍 Experience Cloud ID 扩展中可用的操作类型。

### 操作类型

#### Set Customer IDs

设置一个或多个客户 ID。

1. 输入集成代码。

   集成代码应包含在 Audience Manager 或“客户属性”中设置为数据源的值。

1. 选择一个值。

   该值应为用户 ID。数据元素非常适用于动态值，例如来自特定于客户端的内部系统的 ID。

1. 选择身份验证状态。

   可用选项包括：

   * Unknown
   * Authenticated
   * Logged out

1. （可选）选择&#x200B;**[!UICONTROL 添加]**&#x200B;以设置更多客户ID。
1. 选择&#x200B;**[!UICONTROL 保留更改]**。
