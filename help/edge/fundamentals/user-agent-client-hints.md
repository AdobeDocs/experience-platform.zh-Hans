---
title: 用户代理客户端提示
description: 了解Web SDK中用户代理客户端提示的工作方式
keywords: 用户代理；客户端提示；字符串；用户代理字符串；低熵；高熵
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: faeec4288948012fabeb25d0a0ce5a3b45f563ec
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 7%

---

# 用户代理客户端提示

## 概述 {#overview}

每次Web浏览器向Web服务器发出请求时，请求的标头都包含有关浏览器以及浏览器所运行的环境的信息。 所有此数据都会聚合到一个名为 [!DNL User-Agent] 字符串。

以下是 [!DNL User-Agent] 字符串在来自在 [!DNL Mac OS] 设备。

>[!NOTE]
>
>在这些年中， [!DNL User-Agent] 字符串已多次增长和修改。 以下示例显示了 [!DNL User-Agent] 信息。

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| 字段 | 值 |
|---|---|
| 软件名称 | Chrome |
| 软件版本 | 105 |
| 完整软件版本 | 105.0.0.0 |
| 版面引擎名称 | AppleWebKit |
| 版面引擎版本 | 537.36 |
| Operating system | Mac OS X |
| 操作系统版本 | 10.15.7 |
| 设备 | 英特尔Mac OS X 10_15_7 |

## 用例 {#use-cases}

[!DNL User-Agent] 字符串长期以来一直用于向营销和开发团队提供关于浏览器、操作系统和设备如何显示网站内容以及用户如何与网站交互的重要洞察信息。

[!DNL User-Agent] 字符串还用于阻止垃圾邮件和过滤爬网站的机器人，以获取各种其他目的。

## [!DNL User-Agent] Adobe Experience Cloud中的字符串 {#user-agent-in-adobe}

Adobe Experience Cloud解决方案利用 [!DNL User-Agent] 字符串。

* Adobe Analytics利用 [!DNL User-Agent] 字符串，用于扩充和获取与用于访问网站的操作系统、浏览器和设备相关的其他信息。
* Adobe Audience Manager和Adobe Target根据 [!DNL User-Agent] 字符串。

## 用户代理客户端提示简介 {#ua-ch}

近年来，站点所有者和营销供应商已使用 [!DNL User-Agent] 字符串以及请求标头中包含的其他信息一起创建数字指纹。 这些指纹可以用作在用户不知情的情况下识别用户的手段。

尽管有重要的目的 [!DNL User-Agent] 为站点所有者提供的字符串，浏览器开发人员已决定更改 [!DNL User-Agent] 字符串会运行，以限制最终用户的潜在隐私问题。

他们开发的解决方案称为 [用户代理客户端提示](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). 客户端提示仍允许网站收集必要的浏览器、操作系统和设备信息，同时还可以增强对隐藏跟踪方法（如指纹）的保护。

客户端提示允许网站所有者访问 [!DNL User-Agent] 字符串，但更能保护隐私。

当现代浏览器将用户发送到Web服务器时， [!DNL User-Agent] 无论是否需要字符串，都会在每次请求时发送字符串。 另一方面，客户端提示强制实施一个模型，服务器必须在该模型中向浏览器询问其希望了解的有关客户端的其他信息。 当收到此请求时，浏览器可以应用其自己的策略或用户配置来确定返回哪些数据。 而不是公开整个 [!DNL User-Agent] 字符串默认情况下，访问现在以可审核的显式方式进行管理。

## 浏览器支持 {#browser-support}

[用户代理客户端提示](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) 在 [!DNL Google Chrome ]版本89。

其他基于Chromium的浏览器支持客户端提示API，例如：

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## 类别 {#categories}

用户代理客户端提示分为两类：

* [低熵客户端提示](#low-entropy)
* [高熵客户端提示](#high-entropy)

### 低熵客户端提示 {#low-entropy}

低熵客户端提示包括不能用于指纹用户的基本信息。 有关浏览器品牌、平台以及请求是否来自移动设备等信息。

低熵客户端提示默认在Web SDK中启用，并在每个请求中传递。

| HTTP 标头 | JavaScript | 默认情况下包含在用户代理中 | 默认情况下包含在客户端提示中 |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | 是 | 是 |
| `Sec-CH-UA-Platform` | `platform` | 是 | 是 |
| `Sec-CH-UA-Mobile` | `mobile` | 是 | 是 |

### 高熵客户端提示 {#high-entropy}

高熵客户端提示是有关客户端设备的更详细信息，如平台版本、架构、模型、位（64位或32位平台）或完整操作系统版本。 此信息可能用于指纹识别。

| HTTP 标头 | JavaScript | 默认情况下包含在用户代理中 | 默认情况下包含在客户端提示中 |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | 是 | 否 |
| `Sec-CH-UA-Arc` | `architecture` | 是 | 否 |
| `Sec-CH-UA-Model` | `model` | 是 | 否 |
| `Sec-CH-UA-Bitness` | `Bitness` | 是 | 否 |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | 是 | 否 |

默认情况下，Web SDK中会禁用高熵客户端提示。 要启用它们，您必须手动配置Web SDK以请求高熵客户端提示。

## 高熵客户端提示对Experience Cloud解决方案的影响 {#impact-in-experience-cloud-solutions}

某些Adobe Experience Cloud解决方案在生成报表时依赖于高熵客户端提示中包含的信息。

如果您未在环境中启用高熵客户端提示，则以下描述的Adobe Analytics和Audience Manager报表及特征将不起作用。

### Adobe Analytics报告依赖于高熵客户端提示 {#analytics}

的 [操作系统](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html?lang=zh-Hans) 维度包括作为高熵客户端提示存储的操作系统版本。 如果未启用高熵客户端提示，则对于从Chromium浏览器收集的点击，操作系统版本可能不准确。

### Audience Manager依赖于高熵客户端提示的特征 {#aam}

[!DNL Google] 已更新 [!DNL Chrome] 浏览器功能，可最大限度地减少通过 `User-Agent` 标题。 因此，Audience Manager客户使用 [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en) 将不再收到基于的特征的可靠信息 [平台级别关键值](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html?lang=zh-Hans).

使用平台级别关键值进行定位的Audience Manager客户必须切换到 [Experience PlatformWeb SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=en) 而不是 [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en)，并启用 [高熵客户端提示](#enabling-high-entropy-client-hints) 继续接收可靠的特征数据。

## 启用高熵客户端提示 {#enabling-high-entropy-client-hints}

要在Web SDK部署中启用高熵客户端提示，您必须包含 `highEntropyUserAgentHints` 上下文选项，如 [配置文档](configuring-the-sdk.md#context)，以及现有配置。

例如，要从Web属性中检索高熵客户端提示，您的配置将如下所示：

`context: ["highEntropyUserAgentHints", "web"]`

## 示例 {#example}

浏览器向Web服务器发出的第一个请求的标头中包含的客户端提示将包含浏览器品牌、浏览器的主要版本以及客户端是否为移动设备的指示器。 每个数据将具有其自己的标题值，而不是分组到单个数据中 [!DNL User-Agent] 字符串，如下所示：

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

等效项 [!DNL User-Agent] 同一浏览器的标头如下所示：

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

虽然信息类似，但向服务器发出的第一个请求包含客户端提示。 这些仅包含 [!DNL User-Agent] 字符串。 请求中缺少操作系统架构、完整操作系统版本、布局引擎名称、布局引擎版本和完整浏览器版本。

但是，在后续请求中， [!DNL Client Hints API] 允许web服务器询问有关该设备的其他详细信息。 当根据浏览器策略或用户设置请求这些值时，浏览器响应可能包含该信息。

以下是返回的JSON对象示例 [!DNL Client Hints API] 请求高熵值时：


```json
{
   "architecture":"x86",
   "bitness":"64",
   "brands":[
      {
         "brand":" Not A;Brand",
         "version":"99"
      },
      {
         "brand":"Chromium",
         "version":"100"
      },
      {
         "brand":"Google Chrome",
         "version":"100"
      }
   ],
   "fullVersionList":[
      {
         "brand":" Not A;Brand",
         "version":"99.0.0.0"
      },
      {
         "brand":"Chromium",
         "version":"100.0.4896.127"
      },
      {
         "brand":"Google Chrome",
         "version":"100.0.4896.127"
      }
   ],
   "mobile":false,
   "model":"",
   "platformVersion":"12.2.1"
}
```
