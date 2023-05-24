---
title: 製作最佳實務
description: 瞭解編寫目的地檔案頁面時應遵循的規則和秘訣，以確保頁面符合Adobe Experience Platform檔案品質標準。
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# 製作最佳實務

## 概述 {#overview}

本頁面說明您應在下列情況下遵循的規則： [編寫您的目的地檔案](./documentation-instructions.md) 頁面，確保其符合Adobe Experience Platform檔案品質標準。

## 一般指引 {#general-guidance}

* 填寫時 [範本](./self-service-template.md) 如需目的地檔案，請參閱Adobe投稿人指南，以瞭解有關 [連結](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en)， [表格](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables)，則 [支援的Markdown語法](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en)， [撰寫指引](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en)、等等。
* 請勿在產品檔案中包含觀察和估計。
* 在Experience Platform檔案中，Adobe作者會使用 **粗體格式設定** 參照使用者介面控制項，如下所示：
   * 前往 **[!UICONTROL 連線]** > **[!UICONTROL 目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。 檢視如何在中記錄使用者介面控制項的範例 [目的地教學課程](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## 寫入樣式

>[!IMPORTANT]
>
>讀取 [Adobe檔案撰寫指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) 開始編寫目的地檔案頁面之前。

* 讓您的句子保持短小並快速切入正題。 如果您的句子超過20個單詞，或是使用多個逗號，請考慮將其分成個別的句子。 長度超過20個字的句子對讀者來說特別具有挑戰性。
* 不要過於客氣。 避免在技術檔案中使用「請」或「請……」。

## 链接 {#linking}

依照提供的檔案範本操作，請勿編輯範本中現有的連結。 加入新連結時，請閱讀 [在檔案中使用連結](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) 投稿人指南中的。

## 品牌指南 {#branding}

* AEP不是經核准的公開術語。 請先使用Adobe Experience Platform，然後使用Experience Platform，再使用平台。
   * **不要使用**：將資料從AEP匯出至YourDestination之前，請務必閱讀並完成這些必要條件。
   * **使用**：將資料從Adobe Experience Platform匯出至YourDestination之前，請務必閱讀並完成這些必要條件。

## 影像和熒幕擷取畫面 {#images-and-screenshots}

* 有關以下專案的資訊： [如何連結至影像](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images)，請參閱投稿人指南。
* 使用熒幕擷取畫面時，請確保您的熒幕擷取畫面能擷取整個Platform UI畫面。
* 標示影像以反白顯示頁面上的特定控制項或標籤時，請嘗試遵循Experience Platform檔案團隊使用的標示樣式。 請注意中如何反白以設定檔為基礎的 [此熒幕擷圖](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* 請使用 `png` 格式化影像。
* 請勿使用編號熒幕擷取畫面作為檔案名稱。 影像檔案名稱應為描述性。
   * **不要使用**： `1.png`， `2.png`， `3.png`
   * **使用**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* 請針對您新增至檔案的所有影像使用替代文字，並在替代文字中使用適當的文法。
   * **不要使用**：目的地連線詳細資料
   * **使用**：平台UI的影像，顯示已填入的目的地連線詳細資訊。

## 过程 {#process}

* 此 [檔案範本](./self-service-template.md) 不常根據合作夥伴的意見更新。 開始編寫目的地的檔案之前，請確定您已下載 [範本的最新版本](../assets/docs-framework/yourdestination-template.zip).
* 撰寫檔案，並從復本的分支建立檔案提取請求(PR) *主分支以外的分支*. 在中製作時，請參閱提交目的地以供檢閱區段 [GitHub介面](./use-github-interface-to-create-documentation.md#submit-review) 或 [您的本機環境](./work-in-local-environment.md#submit-review).
