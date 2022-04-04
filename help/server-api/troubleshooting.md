---
title: 故障排除
description: 了解如何对使用Adobe Experience Platform Edge Network Server API时的错误进行故障诊断
seo-description: Learn how to troubleshoot errors when using the Adobe Experience Platform Edge Network Server API
keywords: 边缘网络；网关；API；故障诊断；错误；Griffon
exl-id: f0223fca-30ec-4229-93a5-3faa6cef5482
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 1%

---

# 故障排除

Adobe Experience Platform边缘网络服务器API允许您在事件通过边缘网络数据收集管道处理时从服务捕获调试信息。

与 [Experience Platform调试器](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) 允许您调试基于API的实施。

使用 [Griffon项目](https://aep-sdks.gitbook.io/docs/beta/project-griffon)，则可以创建一个调试会话ID，以便在边缘网络请求中进一步使用该ID来跟踪事件。
