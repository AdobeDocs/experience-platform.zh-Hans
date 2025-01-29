---
keywords: Experience Platform；快速入门；归因人工智能；热门主题；归因人工智能输入；归因人工智能输出；归因人工智能故障诊断；归因人工智能错误
solution: Experience Platform, Real-Time Customer Data Platform
feature: Attribution AI
title: Attribution AI错误疑难解答
description: 查找Attribution AI中常见错误的答案。
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Attribution AI错误疑难解答

本文档提供有关Attribution AI的常见问题解答。

## 无法无痕访问Chrome中的Attribution AI

由于Google Chrome无痕模式安全设置发生更新，导致Google Chrome无痕模式中存在加载错误。 Chrome正在积极处理此问题，以使experience.adobe.com成为受信任的域。

![错误图像](./images/faq/error.PNG){width=500}

### 建议的修复

要解决此问题，您需要将experience.adobe.com添加为始终可以使用Cookie的站点。 首先导航到&#x200B;**chrome://settings/cookies**。 接下来，向下滚动到&#x200B;**自定义行为**&#x200B;部分，然后选择“始终可以使用Cookie的站点”旁边的&#x200B;**添加**&#x200B;按钮。 在显示的弹出窗口中，复制并粘贴`[*.]experience.adobe.com`，然后选中&#x200B;**在此网站中包含第三方Cookie**&#x200B;复选框。 完成后，选择&#x200B;**添加**&#x200B;并以无痕方式重新加载Attribution AI。

![建议的修复](./images/faq/cookies2.gif)
