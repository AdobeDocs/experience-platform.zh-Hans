---
title: Auditor索引標籤
description: 瞭解如何使用Adobe Experience Platform Debugger中的Auditor標籤來測試Adobe Experience Cloud實作。
keywords: debugger;experience platform debugger 扩展程序;chrome;扩展程序;审计员;dtm;target
exl-id: 409094f8-a7d9-45f7-ba12-b5e6250abc0f
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 35%

---

# Auditor索引標籤

在Adobe Experience Platform Debugger中，您可以使用 **[!UICONTROL Auditor]** 索引標籤以在您的頁面上執行一系列稽核測試。

要使用此功能：

1. 選取 **[!UICONTROL Auditor]** 左側導覽列中。
1. 選取 **[!UICONTROL 執行Auditor測試]**. 測試完成後，其結果會顯示於下方。

![Auditor標籤上測試結果的熒幕擷圖](../images/auditor-results.png)

在结果列表上，显示了相应的测试及其结果，并提供了用来解决任意问题的建议。

## 解讀測試結果

每項測試都會加權，而您的測試分數會等於指派的權重。 如果您通過權重為5的測試，則會獲得5分。

| 得分 | 描述 |
| --- | --- |
| 0 | 警示您應留意的問題，但不影響您的分數。 |
| 1 | 建議最佳化。 不影响数据准确性。 |
| 2 | 若未通過此測試，表示您將無法存取Adobe Experience Cloud中的最新功能和修正。 |
| 3 | 測試效率，以及實作是否遵循最佳實務准則。 |
| 4 | 若未通過，表示您可能正在收集不可靠的資料。 |
| 5 | 失敗表示您可能會看到資料遺失。 |

所有測試都會通過或失敗。 检测是否符合测试条件，不存在针对部分合规情况的分量得分。例如，在检测是否含有最新版本的 Adobe 解决方案时，如果您使用的版本与最新版本之间只相差一个版本，那么这种情况下您的得分与相关五个版本的得分是一样的。最新版本包含效能改進和錯誤修正，因此建議使用最新版本。

**强烈建议**&#x200B;修复任何 4 级或 5 级结果。

**建议**&#x200B;修复任何 1 级到 3 级的结果。

## 支援的Adobe技術

Auditor功能可對下列Adobe技術評分：

* Adobe Advertising Cloud DSP
* Adobe Advertising Cloud Search
* Adobe Analytics
* Adobe Experience Cloud Identity Service
* Adobe Target
* 標籤(前身為Adobe Experience Platform Launch)

## 測試規則

如需此功能所提供測試規則的詳細資訊，請參閱下列檔案：

* [标记一致性](./tag-consistency.md)
* [标记状态](./tag-presence.md)
* [配置](./configuration.md)
* [警报](./alerts.md)
