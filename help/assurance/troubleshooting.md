---
title: Adobe Experience Platform Assurance疑难解答指南
description: 本文档概述了使用Adobe Experience Platform Assurance时的常见问题解决方案。
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---


# Adobe Experience Platform保障故障诊断

如果您在确保工作中遇到问题，请参阅以下问题主题下的建议，以解决常见问题。

要实现更顺畅的实施并发现任何潜在问题，请确保您已按 [启用调试日志记录](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) 中的快速入门部分。

您可以使用 [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API。

## 设备内、应用程序问题

### QR代码未打开应用程序

* 直接访问链接。 从以下位置复制链接 **会话详细信息**. 将其粘贴到设备的浏览器地址栏中以将其打开。 如果未打开，请参阅部分 [应用程序将不会打开链接](#app-does-not-open-link).
* 使用其他二维码阅读器。 对于iOS 11或更高版本，请使用照片应用程序读取二维码。

### 应用程序未打开链接

* 验证是否在应用程序中正确配置了深层链接实施。
   * **Android:** 深层链接（应用程序链接）
      * [创建指向应用程序上下文的深层链接](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** 自定义URL方案或通用链接
      * [为应用程序定义自定义URL方案](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [在您的应用程序中支持通用链接](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>对于Android， `startSession` 无需显式调用API。 对于iOS，请按照 [Adobe Experience Platform保障](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### 出现身份验证叠加，但应用程序无法连接

* 确保设备通过设备Web浏览器连接Internet。
* 如果应用程序从未成功连接到保证服务，请确保已为保证正确设置。 请参阅安装 [Adobe Experience Platform保障](./tutorials/implement-assurance.md) SDK库。
* 验证会话与链接匹配，并为预期会话正确输入。 请参阅 [日志消息“OrgID信息不可用”](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) （仅当您有权访问多个ORG实例时，这种情况才不常见且相关）。

### Adobe Analytics调试

**后处理状态 — 无调试标记**

在Analytics事件视图中，如果事件在处理后状态为“无调试标志”时失败，则您当前的Adobe Analytics或保证SDK版本可能不支持Analytics调试功能。
请将Adobe Analytics和保障SDK扩展升级到最新版本以解决此问题。

| 最低版本要求 | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### React本机MobileCore和AEPA保险兼容性

| AEP保障版本 | 移动核心版本 | 安装说明 |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

如果您使用 `react-native-acpcore` 有保证， React本机应用程序可能无法使用以下错误消息之一进行构建：

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

或

```
AppDelegate: AEPAssurance.h file not found
```

**解决方案**

如果发生这种情况，请降级 `react-native-aepassurance` 使用以下npm命令：

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

出现此错误的原因是 `react-native-acpcore` 扩展 **仅** 兼容 `react-native-aepassurance` 版本2.x.x及更低版本。
