---
title: 子資源完整性(SRI)支援
description: 瞭解Adobe Experience Platform如何支援子資源完整性(SRI)。
exl-id: bd8bc3f7-9a85-44e2-ae07-f0664179b51c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 72%

---

# 子資源完整性(SRI)支援

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

本文介紹Adobe Experience Platform如何支援子資源完整性(SRI)。

现代网站是通过引用 Web 上不同位置的图像、内容和脚本来构建的。SRI可讓瀏覽器確認要求的檔案內容未意外修改。

虽然 SRI 与内容安全策略 (CSP) 的用例是互补的，但是 SRI 不同于 CSP，CSP 可确保网站上仅允许使用来自可信来源的文件。而 SRI 则更进一步，它可确保这些文件的内容符合您的预期。

>[!NOTE]
>
>有关 SRI 的更多详细信息，请参阅 [MDN Web 文档](https://developer.mozilla.org/zh-CN/docs/Web/Security/Subresource_Integrity)。

SRI 验证过程可概括如下：

1. 您生成要验证的资产的加密哈希。
1. 您将哈希放置在网站上用于加载文件的 HTML 元素的 `integrity` 属性中。
1. 当浏览器发现 `integrity` 属性时，浏览器会请求资源，并独立生成自己的加密哈希版本。
1. 浏览器将 `integrity` 哈希与它生成的哈希进行比较。如果二者匹配，则允许使用资产。如果二者不匹配，则将阻止使用资产。

## 标记管理系统的限制

作為標籤管理系統(TMS)，Adobe Experience Platform中的標籤提供編譯的JavaScript程式庫組建，讓您透過單一載入到頁面上 `<script>` 元素（內嵌程式碼）。 TMS 提供的动态功能是通过动态交换该脚本的内容来实现的，无需更改其他任何内容。

但是，如果脚本内容发生更改，这些内容的加密哈希也会随之更改。因此，要搭配使用 SRI 与 TMS 的唯一方法是，在发布新内部版本的同时更新嵌入代码。对于许多人来说，这首先就违背了使用 TMS 的主要目的。

下一個最佳標籤安全性選項是實作內容安全性原則。 如需詳細資訊，請參閱以下指南： [CSP和標籤](./content-security-policy.md).

## 将 SRI 集成到内部版本部署中

如果您仍然希望将 SRI 用于库内部版本，则必须使用自托管。如果您使用 Adobe 管理的主机，则在没有足够的时间且新内部版本内容与嵌入代码的 `integrity` 属性不匹配的情况下，无法使用 SRI。

自动完成嵌入代码更新流程的复杂程度因网站结构而异，但一般步骤可概括如下：

1. 通过 SFTP 交付或从用户界面下载存档来检索生产库内部版本。
1. 生成主内部版本的加密哈希。
1. 确保将嵌入代码的 `integrity` 属性更新为新哈希，并将引用的内部版本作为同一部署的一部分进行更新。

>[!IMPORTANT]
>
>此方法仅适用于主内部版本。它不包含任何可能存在的较小文件。

## 后续步骤

本檔案說明搭配標籤使用SRI的限制，以及將SRI整合至程式庫組建部署（儘管有這些限制）所需的步驟。 如果您尚未閱讀指南，強烈建議您參閱 [CSP和標籤](./content-security-policy.md) 以取得替代安全性選項。
