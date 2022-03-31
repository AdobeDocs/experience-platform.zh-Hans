---
keywords: Experience Platform；快速入门；归因ai；热门主题；归因ai输入；归因ai输出；归因ai故障诊断；归因ai错误
solution: Experience Platform, Real-time Customer Data Platform
feature: Attribution AI
title: Attribution AI错误疑难解答
description: 查找Attribution AI中常见错误的答案。
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Attribution AI错误疑难解答

本文档提供了有关Attribution AI的常见问题解答。

## 无法在Chrome（隐身）中访问Attribution AI

由于Google Chrome的隐身模式安全设置中的更新，在Google Chrome的隐身模式中出现加载错误。 该问题正在与Chrome一起积极处理，以使experience.adobe.com成为可信域。

<img src="./images/faq/error.PNG" width="500" /><br />

### 建议的修复

要解决此问题，您需要将experience.adobe.com添加为始终可以使用Cookie的网站。 首先，导航到 **chrome://settings/cookies**. 接下来，向下滚动到 **自定义行为** 部分，然后选择 **添加** 按钮。 在显示的弹出窗口中，复制并粘贴 `[*.]experience.adobe.com` 然后选择 **包括第三方Cookie** 复选框。 完成后，选择 **添加** 然后隐匿地重新加载Attribution AI。

![推荐修复](./images/faq/cookies2.gif)
