---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
title: 自助來源中的設定選項（批次SDK）
description: 本檔案提供使用Self-Serve Sources (Batch SDK)所需準備的設定概觀。
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 自助來源中的設定選項（批次SDK）

本檔案提供使用Self-Serve Sources (Batch SDK)所需準備的設定概觀。

## 連線規格

連線規格會傳回來源的聯結器屬性。 它們包括與建立基礎和來源連線相關的驗證規格，以及指派給特定來源的固定連線規格ID。 連線規格與租使用者和組織無關。 典型的連線規格包含指定來源的基本資訊，以及三個不同的區段： `authSpec`， `sourceSpec`、和 `exploreSpec`.

| 規格 | 描述 |
| --- | --- |
| `authSpec` | 此 `authSpec` 陣列包含將來源連線至Platform所需的驗證引數資訊。 任何特定來源都可以支援多種不同型別的驗證。 |
| `sourceSpec` | 此 `sourceSpec` 陣列包含與來源相關的一般資訊，包括在UI中顯示來源所需的屬性資訊、檔案連結，以及有關分頁、標題、內文和排程的引數。 此外， `sourceSpec` 說明從基本連線建立來源連線所需的引數結構，以及建立來源連線所需的引數結構。 |
| `exploreSpec` | 此 `exploreSpec` array定義探索和檢查來源中所包含物件所需的引數。 此 `exploreSpec` 也會定義探索及檢查物件時傳回的回應格式。 |

{style="table-layout:auto"}

## 填入連線規格值

連線規格可分成三個不同的部分：驗證規格、來源規格和探索規格。

如需如何填入連線規格每個部分的值的說明，請參閱下列檔案：

* [設定您的驗證規格](./authspec.md)
* [設定您的來源規格](./sourcespec.md)
* [設定您的瀏覽規格](./explorespec.md)
