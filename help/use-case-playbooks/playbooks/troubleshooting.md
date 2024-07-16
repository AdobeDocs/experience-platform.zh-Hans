---
solution: Experience Platform
title: 行动手册的已知限制和疑难解答
description: 详细了解行动手册的已知问题和常见问题以及如何对其进行故障诊断
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 0faf3187c0b32e0be70033e501939412ade37d7e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# 故障排除 {#troubleshooting}

查看有关使用用例行动手册时常见错误的故障排除建议

## 未配置Adobe Journey Optimizer表面 {#surfaces-not-configured}

在创建行动手册的实例时，您可能会看到下面显示的消息。

![疑难解答](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

这是因为Journey Optimizer行动手册为电子邮件、推送和短信渠道创建消息。 阅读[入门](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer)指南以配置不同的表面。

## 创建新实例时状态&#x200B;*失败* {#status-failed}

如果您在尝试创建实例时看到失败消息，这可能是因为管理员未向您授予所需的用户权限。 行动手册包含大量不同的资产，您的用户需要拥有创建这些资产的权限，才能成功创建行动手册的实例。 有关如何设置权限，请参阅本指南的[权限](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions)部分。

## 导入失败 {#import-failure}

客户在不同的测试环境中操作，有时在将实例从其环境导入到Adobe沙盒时，可能会失败。 要查看这些导入的状态，请从左侧导航中选择“沙盒”，然后选择“作业”。 您可以在此处查看导入文件的所有详细信息。 选择状态为失败的文件，然后选择查看作业详细信息。 此时将显示一个模式窗口。 选择查看JSON文件，然后向下滚动并复制“消息”下显示的错误消息。 很可能会显示多条错误消息，因此请确保复制所有错误消息。 在尝试记录错误票证时，将这些错误发送给您的Adobe团队。 这加快了解决过程，并为您的团队提供了更多关于所发生情况的上下文。
