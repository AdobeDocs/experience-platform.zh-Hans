---
title: 用户代理客户端提示
description: 了解用户代理客户端提示在Web SDK中的工作方式。 客户端提示允许网站所有者访问用户代理字符串中提供的许多相同信息，但保护隐私的方式更加严格。
keywords: 用户代理；客户端提示；字符串；用户代理字符串；低熵；高熵
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 3%

---

# 用户代理客户端提示

## 概述 {#overview}

每次Web浏览器向Web服务器发出请求时，请求的标题都包含有关浏览器和浏览器运行环境的信息。 所有这些数据都会聚合为一个字符串，称为用户代理字符串。

以下是用户代理字符串在来自在[!DNL Mac OS]设备上运行的Chrome浏览器的请求中的显示示例。

>[!NOTE]
>
>多年来，用户代理字符串中包含的浏览器和设备信息量增长并多次修改。 以下示例显示了一组最常见的用户代理信息。

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| 字段 | 值 |
|---|---|
| 软件名称 | Chrome |
| 软件版本 | 105 |
| 完整软件版本 | 105.0.0.0 |
| 布局引擎名称 | AppleWebKit |
| 布局引擎版本 | 537.36 |
| Operating system | MAC OS X |
| 操作系统版本 | 10.15.7 |
| 设备 | 英特尔Mac OS X 10_15_7 |

## 用例 {#use-cases}

长期以来，用户代理字符串一直被用来为营销和开发团队提供有关浏览器、操作系统和设备如何显示网站内容以及用户如何与网站交互的重要见解。

出于其他各种目的，用户代理字符串还用于阻止垃圾邮件并过滤抓取站点的机器人。

## Adobe Experience Cloud中的用户代理字符串 {#user-agent-in-adobe}

Adobe Experience Cloud解决方案以各种方式利用用户代理字符串。

* Adobe Analytics利用用户代理字符串来补充和获取与用于访问网站的操作系统、浏览器和设备相关的其他信息。
* Adobe Audience Manager和Adobe Target根据用户代理字符串提供的信息，使最终用户有资格参加分段和个性化活动。

## 引入用户代理客户端提示 {#ua-ch}

近年来，网站所有者和营销供应商使用用户代理字符串以及请求标头中包含的其他信息来创建数字指纹。 这些指纹可以用作在用户不知情的情况下识别用户的手段。

尽管用户代理字符串对网站所有者具有重要用途，但浏览器开发人员已决定更改用户代理字符串的操作方式，以限制最终用户的潜在隐私问题。

他们开发的解决方案称为[用户代理客户端提示](https://developer.chrome.com/docs/privacy-sandbox/user-agent/)。 客户端提示仍然允许网站收集必要的浏览器、操作系统和设备信息，同时还可以增强对隐蔽跟踪方法（如指纹）的防范。

客户端提示允许网站所有者访问用户代理字符串中提供的许多相同信息，但保护隐私的方式更加严格。

当现代浏览器将用户发送到Web服务器时，无论是否需要，都会在每次请求时发送整个用户代理字符串。 另一方面，客户端提示会强制实施一种模型，其中服务器必须向浏览器询问它想要了解的有关客户端的其他信息。 在收到此请求后，浏览器可以应用自己的策略或用户配置来确定返回的数据。 与默认情况下对所有请求公开整个用户代理字符串不同，现在可以明确且可审核的方式管理访问。

## 浏览器支持 {#browser-support}

[用户代理客户端提示](https://developer.chrome.com/docs/privacy-sandbox/user-agent/)随[!DNL Google Chrome]版本89引入。

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

低熵客户端提示包括无法用于指纹识别的用户的基本信息。 信息，例如浏览器品牌、平台以及请求是否来自移动设备。

在Web SDK中，默认启用低熵客户端提示，并在每个请求中传递。

| HTTP标头 | JavaScript | 默认情况下包含在用户代理中 | 默认情况下包含在客户端提示中 |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | 是 | 是 |
| `Sec-CH-UA-Platform` | `platform` | 是 | 是 |
| `Sec-CH-UA-Mobile` | `mobile` | 是 | 是 |

### 高熵客户端提示 {#high-entropy}

高熵客户端提示是有关客户端设备的更详细信息，例如平台版本、架构、模型、位（64位或32位平台）或完整操作系统版本。 这些信息可能被用于指纹。

| 属性 | 描述 | HTTP标头 | XDM 路径 | 示例 | 默认包含在用户代理中 | 默认情况下包含在客户端提示中 |
| --- | --- | --- | --- | --- |---|---|
| 操作系统版本 | 操作系统的版本。 | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` | 是 | 否 |
| 架构 | 底层CPU架构。 | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` | 是 | 否 |
| 设备型号 | 使用的设备的名称。 | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` | 是 | 否 |
| 位数 | 基础CPU架构支持的位数。 | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` | 是 | 否 |
| 浏览器供应商 | 创建浏览器的公司。 低熵提示`Sec-CH-UA`也收集此元素。 | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` | 是 | 否 |
| 浏览器名称 | 使用的浏览器。 低熵提示`Sec-CH-UA`也收集此元素。 | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` | 是 | 否 |
| 浏览器版本 | 浏览器的重要版本。 低熵提示`Sec-CH-UA`也收集此元素。 不会自动收集确切的浏览器版本。 | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` | 是 | 否 |


默认情况下，在Web SDK中禁用高熵客户端提示。 要启用这些功能，您必须手动配置Web SDK以请求高熵客户端提示。

## 高熵客户端提示对Experience Cloud解决方案的影响 {#impact-in-experience-cloud-solutions}

某些Adobe Experience Cloud解决方案在生成报告时依赖高熵客户端提示中包含的信息。

如果您没有在环境中启用高熵客户端提示，则下面描述的Adobe Analytics和Audience Manager报表和特征将不起作用。

### Adobe Analytics报告依赖于高熵客户端提示 {#analytics}

[操作系统](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html)维度包括作为高熵客户端提示存储的操作系统版本。 如果未启用高熵客户端提示，则对于从Chromium浏览器收集的点击，操作系统版本可能不准确。

### 依赖高熵客户端提示的Audience Manager特征 {#aam}

[!DNL Google]已更新[!DNL Chrome]浏览器功能以最小化通过`User-Agent`标头收集的信息。 因此，使用[DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=zh-Hans)的Audience Manager客户将不再收到基于[平台级别密钥](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html)的特征的可靠信息。

使用平台级别密钥进行定位的Audience Manager客户必须切换到[Experience Platform Web SDK](/help/web-sdk/home.md)，而不是[DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=zh-Hans)，并启用[高熵客户端提示](#enabling-high-entropy-client-hints)以继续接收可靠的特征数据。

## 启用高熵客户端提示 {#enabling-high-entropy-client-hints}

要在Web SDK部署中启用高熵客户端提示，必须在`highEntropyUserAgentHints`字段中包括其他[`context`](/help/web-sdk/commands/configure/context.md)上下文选项。

例如，要从Web属性检索高熵客户端提示，您的配置将如下所示：

`context: ["highEntropyUserAgentHints", "web"]`

## 示例 {#example}

浏览器向Web服务器发出的第一个请求的标头中包含的客户端提示将包含浏览器品牌、浏览器的主要版本以及客户端是否为移动设备的指示器。 每段数据都有自己的标题值，而不是分组到单个用户代理字符串中，如下所示：

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

相同浏览器的等效[!DNL User-Agent]标头如下所示：

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

尽管信息类似，但对服务器的第一个请求包含客户端提示。 这些仅包括用户代理字符串中可用内容的子集。 请求中缺少的是操作系统体系结构、完整操作系统版本、版面引擎名称、版面引擎版本和完整浏览器版本。

但是，在后续请求中，[!DNL Client Hints API]允许Web服务器询问有关设备的其他详细信息。 在请求这些值时，根据浏览器策略或用户设置，浏览器响应可能包含该信息。

以下是请求高熵值时[!DNL Client Hints API]返回的JSON对象示例：


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
