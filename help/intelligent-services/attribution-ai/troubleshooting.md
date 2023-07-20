---
keywords: Experience Platform；快速入门；归因人工智能；热门主题；归因人工智能输入；归因人工智能输出；归因人工智能故障排除；归因人工智能错误
solution: Experience Platform, Real-Time Customer Data Platform
feature: Attribution AI
title: Attribution AI错误疑难解答
description: 查找Attribution AI中常见错误的答案。
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Attribution AI错误疑难解答

本文档提供了有关Attribution AI的常见问题解答。

## 无法在Chrome中无痕访问Attribution AI

由于Google Chrome无痕模式安全设置更新，在Google Chrome无痕模式中加载出错。 正在积极使用Chrome解决此问题，以使experience.adobe.com成为受信任的域。

<img src="./images/faq/error.PNG" width="500" /><br />

### 建议的修复

要解决此问题，您需要添加experience.adobe.com作为始终可以使用Cookie的站点。 首先导航到 **chrome://settings/cookies**. 接下来，向下滚动到 **自定义行为** 部分，然后选择 **添加** “始终可以使用Cookie的站点”旁边的按钮。 在显示的弹出窗口中，复制并粘贴 `[*.]experience.adobe.com` 然后选择 **包括第三方Cookie** “在此网站上”复选框。 完成后，选择 **添加** 并隐匿地重新装载Attribution AI。

![建议的修复](./images/faq/cookies2.gif)
