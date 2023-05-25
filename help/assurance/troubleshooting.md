---
title: Adobe Experience Platform保证疑难解答指南
description: 本文档概述了使用Adobe Experience Platform保障时常见问题的解决方案。
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---

# Adobe Experience Platform保障故障诊断

如果您在使Assurance正常工作时遇到问题，请参阅以下问题主题下的建议，以解决常见问题。

要启用更平稳的实施并发现任何潜在问题，请确保您已根据以下日期打开SDK日志记录： [启用调试日志记录](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) 在入门指南部分中。

您可以使用更改SDK日志级别 [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API。

## 设备上应用程序问题

### 二维码未打开应用程序

* 直接访问链接。 链接复制自 **会话详细信息**. 将其粘贴到设备的浏览器地址栏以将其打开。 如果它未打开，请参阅部分 [应用程序不会打开链接](#app-does-not-open-link).
* 使用其他二维读者。 对于iOS 11或更高版本，请使用照片应用程序读取二维码。

### 应用程序未打开链接

* 验证是否已在应用程序中正确配置深层链接实施。
   * **Android：** 深层链接（应用程序链接）
      * [创建指向应用程序上下文的深层链接](https://developer.android.com/training/app-links/deep-linking)
   * **iOS：** 自定义URL方案或通用链接
      * [为您的应用程序定义自定义URL方案](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [在应用程序中支持通用链接](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>对于Android，使用 `startSession` 无需显式调用API。 对于iOS，请按照中的说明使用API [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### 出现身份验证叠加，但应用程序无法连接

* 通过设备Web浏览器确保设备的Internet连接。
* 如果应用程序从未成功连接到Assurance服务，请确保已正确设置Assurance服务。 请参阅关于安装 [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md) sdk库。
* 验证会话是否与链接匹配，以及是否正确输入了预期会话。 参见 [日志消息“OrgID信息不可用”](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) （这种情况并不常见，只有在您有权访问多个ORG实例时才相关）。

### Adobe Analytics调试

**后处理状态 — 无调试标记**

在“Analytics事件”视图中，如果事件失败并显示后处理状态“No Debug Flag”，则您当前的Adobe Analytics或Assurance SDK版本可能不支持Analytics调试功能。
请将Adobe Analytics和Assurance SDK扩展升级到最新版本以解决此问题。

| 最低版本要求 | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### React Native MobileCore和AEPAssurance兼容性

| AEP保证版本 | 移动核心版本 | 安装说明 |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

如果您使用 `react-native-acpcore` 使用Assurance时，React Native应用程序可能会因以下错误消息之一而无法构建：

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

或

```
AppDelegate: AEPAssurance.h file not found
```

**解决方案**

如果发生这种情况，请将您的 `react-native-aepassurance` 使用以下npm命令：

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

出现此错误的原因是 `react-native-acpcore` 扩展为 **仅限** 兼容 `react-native-aepassurance` 版本2.x.x及更低版本。
