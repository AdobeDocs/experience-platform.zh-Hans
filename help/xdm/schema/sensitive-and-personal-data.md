---
title: XDM中的敏感和個人資訊
description: 瞭解關於Experience Data Model (XDM)中敏感個人資訊(SPI)和個人識別資訊(PII)的關鍵考量事項。
exl-id: 92a8b6ad-3c45-4772-8178-60f857ab13e2
source-git-commit: 9785b252b7c9cb3513858476753b6b4f71277ed7
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# XDM中的敏感和個人資訊

Experience Data Model (XDM)提供用於Adobe Experience Platform的標準資料結構，可讓您收集客戶體驗的資料。 此資料可包含敏感的個人資訊(SPI)和個人識別資訊(PII)，例如客戶的電子郵件地址、姓名、帳戶ID和其他資料欄位。

一般資料保護規範(GDPR)等組織規則和法律隱私權法規對SPI和PII的收集、儲存、使用和共用方式實施限制。 因此，請務必考慮哪些欄位代表資料模型中的敏感或個人資訊，並確保您的作業符合組織和法律准則。

本文介紹XDM中敏感資料和個人資料的重要考量事項。

## 決定哪些欄位包含敏感或個人資料

構成SPI和PII的要素內容非常特定，因此您可自行瞭解您的資料模型、業務營運和適用法規，以決定哪些結構描述欄位代表敏感或個人資料。

例如，客戶的法律管轄區會直接影響哪些資訊被視為敏感。 GDPR為SPI和PII提供完善的定義，但歐洲經濟區(EEA)以外的客戶可能會受到不同的定義和限制。

## 處理敏感和個人資料

與敏感資料和個人資料本身的定義類似，處理此資料的限制也是內容專屬的。

在可以收集和處理哪些資料以及出於什麼目的方面，客戶同意通常是關鍵因素。 根據客戶的法律管轄區，收集其敏感和個人資料可能需要明確同意。 即使在不要求明確同意的情況下，資料處理限制仍然適用，具體取決於隱私權通知對客戶的陳述。

請洽詢您的法律團隊，以決定針對您的業務使用案例處理敏感和個人資料的方式。

## 限制使用敏感和個人資料

XDM提供各種標準欄位群組和資料型別，以說明可加強客戶體驗的相關常用資料結構。 但是，如果建議的標準資源包含您不想包含在結構描述中的受限制欄位，則不必使用該資源。

Platform可讓您定義自己的自訂欄位群組和資料型別，讓您在任何可用標準資源不符合需求時，可完全控制資料的結構。 有關如何定義這些自訂資源的詳細資訊，請參閱以下檔案：

* [建立自訂欄位群組](../ui/resources/field-groups.md#create)
* [建立自訂資料型別](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

## 后续步骤

本檔案說明有關XDM中敏感和個人資料的關鍵考量事項。 如需如何建立方案模型以最符合業務使用案例的詳細資訊，請參閱以下指南中的內容： [資料模型化的最佳實務](./best-practices.md).

如需Experience Platform中資料控管和隱私權功能的詳細資訊，請參閱以下文章的概觀： [治理、隱私和安全性](../../landing/governance-privacy-security/overview.md).
