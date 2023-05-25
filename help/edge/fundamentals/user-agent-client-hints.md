---
title: 用户代理客户端提示
description: 了解用户代理客户端提示在Web SDK中的工作方式。 客户端提示允许网站所有者访问User-Agent字符串中提供的许多相同信息，但采用更保护隐私的方式。
keywords: 用户代理；客户端提示；字符串；用户代理字符串；低熵；高熵
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 29679e85943f16bcb02064cc60a249a3de61e022
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 7%

---

# 用户代理客户端提示

## 概述 {#overview}

每次Web浏览器向Web服务器发出请求时，请求的标头都包含有关浏览器和运行浏览器的环境的信息。 所有这些数据都会聚合为一个字符串，称为 [!DNL User-Agent] 字符串。

以下是一个示例， [!DNL User-Agent] 字符串看起来像是在上运行的Chrome浏览器发出的请求中 [!DNL Mac OS] 设备。

>[!NOTE]
>
>多年来，中包含的浏览器和设备信息量 [!DNL User-Agent] 字符串已多次增长和修改。 以下示例显示了一组最常见的选项 [!DNL User-Agent] 信息。

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

[!DNL User-Agent] 长期以来，字符串一直被用来为营销和开发团队提供有关浏览器、操作系统和设备如何显示网站内容以及用户如何与网站交互的重要见解。

[!DNL User-Agent] 出于其他各种目的，字符串还用于阻止垃圾邮件并过滤抓取网站的机器人。

## [!DNL User-Agent] Adobe Experience Cloud中的字符串 {#user-agent-in-adobe}

Adobe Experience Cloud解决方案利用 [!DNL User-Agent] 字符串以各种方式显示。

* Adobe Analytics利用 [!DNL User-Agent] 字符串，用于增强和派生与用于访问网站的操作系统、浏览器和设备相关的其他信息。
* Adobe Audience Manager和Adobe Target根据 [!DNL User-Agent] 字符串。

## 用户代理客户端提示简介 {#ua-ch}

近年来，网站所有者和营销供应商使用 [!DNL User-Agent] 字符串以及请求标头中包含的其他信息以创建数字指纹。 这些指纹可以用作在用户不知情的情况下识别用户的手段。

尽管这其中的重要目的 [!DNL User-Agent] 字符串为站点所有者服务，浏览器开发人员已决定更改方法 [!DNL User-Agent] 字符串发挥作用，以限制最终用户的潜在隐私问题。

他们开发的解决方案称为 [用户代理客户端提示](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). 客户端提示仍然允许网站收集必要的浏览器、操作系统和设备信息，同时还可以增强对隐蔽跟踪方法（如指纹）的防范。

客户端提示允许网站所有者访问 [!DNL User-Agent] 字符串，但采用更保护隐私的方式。

当现代浏览器将用户发送到Web服务器时，整个 [!DNL User-Agent] 无论是否需要，都会在每次请求时发送字符串。 另一方面，客户端提示会强制执行一种模型，其中服务器必须向浏览器询问它想要了解的有关客户端的其他信息。 在收到此请求后，浏览器可以应用其自己的策略或用户配置来确定返回的数据。 而不是公开整个 [!DNL User-Agent] 默认情况下，所有请求的访问都以明确且可审核的方式进行管理。

## 浏览器支持 {#browser-support}

[用户代理客户端提示](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) 引入于 [!DNL Google Chrome ]版本89。

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

低熵客户端提示包括不能用于指纹识别用户的基本信息。 信息，例如浏览器品牌、平台以及请求是否来自移动设备。

默认情况下，Web SDK中会启用低熵客户端提示，并在每个请求中传递。

| HTTP 标头 | JavaScript | 默认情况下包含在用户代理中 | 默认情况下包含在客户端提示中 |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | 是 | 是 |
| `Sec-CH-UA-Platform` | `platform` | 是 | 是 |
| `Sec-CH-UA-Mobile` | `mobile` | 是 | 是 |

### 高熵客户端提示 {#high-entropy}

高熵客户端提示是有关客户端设备的更详细信息，例如平台版本、架构、模型、位（64位或32位平台）或完整操作系统版本。 这些信息可能用于指纹。

| HTTP 标头 | JavaScript | 默认情况下包含在用户代理中 | 默认情况下包含在客户端提示中 |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | 是 | 否 |
| `Sec-CH-UA-Arc` | `architecture` | 是 | 否 |
| `Sec-CH-UA-Model` | `model` | 是 | 否 |
| `Sec-CH-UA-Bitness` | `Bitness` | 是 | 否 |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | 是 | 否 |

默认情况下，Web SDK中禁用高熵客户端提示。 要启用它们，您必须手动配置Web SDK以请求高熵客户端提示。

## 高熵客户端提示对Experience Cloud解决方案的影响 {#impact-in-experience-cloud-solutions}

某些Adobe Experience Cloud解决方案在生成报告时依赖高熵客户端提示中包含的信息。

如果您没有在环境中启用高熵客户端提示，则下面描述的Adobe Analytics和Audience Manager报表和特征将无法工作。

### Adobe Analytics报表依赖高熵客户端提示 {#analytics}

此 [操作系统](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html?lang=zh-Hans) 维度包括作为高熵客户端提示存储的操作系统版本。 如果未启用高熵客户端提示，则对于从Chromium浏览器收集的点击，操作系统版本可能不准确。

### 依赖高熵客户端提示的Audience Manager特征 {#aam}

[!DNL Google] 已更新 [!DNL Chrome] 浏览器功能，可最大限度地减少通过 `User-Agent` 标头。 因此，Audience Manager客户使用 [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en) 将不再收到基于以下特征的可靠信息： [平台级别键](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html?lang=zh-Hans).

使用平台级别关键值进行定位的Audience Manager客户必须切换到 [Experience PlatformWeb SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=en) 而不是 [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en)，并启用 [高熵客户端提示](#enabling-high-entropy-client-hints) 以继续接收可靠特征数据。

## 启用高熵客户端提示 {#enabling-high-entropy-client-hints}

要在Web SDK部署中启用高熵客户端提示，您必须包含其他 `highEntropyUserAgentHints` 上下文选项，如 [配置文档](configuring-the-sdk.md#context)，以及您现有的配置。

例如，要从Web属性检索高熵客户端提示，您的配置将如下所示：

`context: ["highEntropyUserAgentHints", "web"]`

## 示例 {#example}

浏览器向Web服务器发出的第一个请求的标头中包含的客户端提示将包含浏览器品牌、浏览器的主要版本以及客户端是否为移动设备的指示器。 每段数据都将有自己的标头值，而不是分组到单个中 [!DNL User-Agent] 字符串，如下所示：

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

等同的 [!DNL User-Agent] 同一浏览器的标题将如下所示：

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

尽管信息类似，但对服务器的第一个请求包含客户端提示。 这些仅包括 [!DNL User-Agent] 字符串。 请求中缺少的是操作系统体系结构、完整操作系统版本、版面引擎名称、版面引擎版本和完整浏览器版本。

然而，在接获要求时， [!DNL Client Hints API] 允许Web服务器询问有关设备的其他详细信息。 当请求这些值时，根据浏览器策略或用户设置，浏览器响应可能包含该信息。

以下是由返回的JSON对象示例 [!DNL Client Hints API] 当请求高熵值时：


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
