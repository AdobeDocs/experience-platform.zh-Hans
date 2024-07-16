---
title: Adobe Experience Platform Assurance 疑难解答指南
description: 本文档概述了使用 Adobe Experience Platform Assurance 时常见问题的解决方案。
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 100%

---

# Adobe Experience Platform Assurance 疑难解答

如果 Assurance 无法正常工作，请参阅以下问题主题下的建议来解决常见问题。

为了更顺利的实施并发现任何潜在问题，请确保根据“开始使用”部分中的[启用调试记录](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/)打开 SDK 记录。

您可以使用 [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel)API 更改 SDK 日志级别。

## 设备上、应用程序问题

### 二维码打不开应用程序

* 直接访问该链接。复制&#x200B;**会话详情**&#x200B;中的链接。将其粘贴到设备的浏览器地址栏中，以将其打开。如果打不开，请参阅[应用程序无法打开链接](#app-does-not-open-link)部分。
* 使用不同的 QR 阅读器。对于 iOS 11 或更高版本，请使用照片应用程序读取 QR 码。

### 应用程序打不开链接

* 验证应用程序中的深层链接实施是否配置正确。
   * **Android：**&#x200B;深层链接（应用程序链接）
      * [创建与应用程序上下文的深层链接](https://developer.android.com/training/app-links/deep-linking)
   * **iOS：**&#x200B;自定义 URL 方案或通用链接
      * [为您的应用程序定义自定义 URL 方案](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [在您的应用程序中支持通用链接](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>对于 Android，`startSession` API 不需要显式调用。对于 iOS，请使用 [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core) 中描述的 API。

### 出现身份验证叠加层，但应用程序无法连接

* 通过设备网络浏览器确保设备的互联网连接。
* 如果应用程序从未成功连接到 Assurance 服务，请确保其正确设置 Assurance。请参阅有关安装 [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md) SDK 库的说明。
* 验证会话是否与链接匹配，并且是否正确输入了预期会话。请参阅[日志消息“OrgID 信息不可用”](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available)（这种情况并不常见，仅当您有权访问多个 ORG 实例时才相关）。

### Adobe Analytics 调试

**后处理状态 - 无调试标志**

在您的 Analytics 事件视图中，如果事件失败并且后处理状态显示为“无调试标志”，则您当前的 Adobe Analytics 或 Assurance SDK 版本可能不支持 Analytics 调试功能。
请将 Adobe Analytics 和 Assurance SDK 扩展程序升级到最新版本以解决此问题。

| 最低版本要求 | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### React Native MobileCore 和 AEPAssurance 兼容性

| AEP Assurance 版本 | 移动核心版本 | 安装说明 |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

如果您正在使用带有 `react-native-acpcore` 的 Assurance，React Native 应用程序可能无法构建并会出现以下错误消息之一：

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

或

```
AppDelegate: AEPAssurance.h file not found
```

**解决方案**

如果发生这种情况，请使用以下 npm 命令降级您的 `react-native-aepassurance`：

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

出现此错误的原因是`react-native-acpcore`该扩展程序&#x200B;**仅与**`react-native-aepassurance`2.xx 及以下版本兼容。
