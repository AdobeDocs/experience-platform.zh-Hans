---
keywords: Experience Platform；首頁；熱門主題；資料品質；品質；品質；支援的驗證；驗證；支援的驗證；
solution: Experience Platform
title: 資料品質
description: 以下檔案提供Adobe Experience Platform中批次和串流擷取支援的檢查和驗證行為摘要。
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 6%

---

# Adobe Experience Platform中的資料品質

Adobe Experience Platform針對透過批次或串流擷取上傳的任何資料，提供完整、準確和一致的明確定義保證。 以下檔案提供中批次和串流擷取支援的檢查和驗證行為摘要 [!DNL Experience Platform].

## 支援的檢查

|   | 批次擷取 | 串流擷取 |
| ------ | --------------- | ------------------- |
| 資料型別檢查 | 是 | 是 |
| 列舉檢查 | 是 | 是 |
| 範圍檢查（最小值、最大值） | 是 | 是 |
| 必填欄位檢查 | 是 | 是 |
| 圖樣檢查 | 否 | 是 |
| 格式檢查 | 否 | 是 |

## 支援的驗證行為

批次和串流擷取都會將不良資料移動到中進行擷取和分析，以防止失敗的資料下游 [!DNL Data Lake]. 資料擷取針對批次和串流擷取提供下列驗證。

### 批量摄取

批次擷取會完成下列驗證：

| 驗證區域 | 描述 |
| --------------- | ----------- |
| 架构 | 確保結構描述為 **not** 空白，並包含對聯合結構描述的參考，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 請確定已定義所有有效的身分描述項。 |
| `createdUser` | 確保允許擷取批次的使用者擷取批次。 |

### 流式摄取

下列驗證會針對串流擷取完成：

| 驗證區域 | 描述 |
| --------------- | ----------- |
| 架构 | 確保結構描述為 **not** 空白，並包含對聯合結構描述的參考，如下所示： `"meta:immutableTags": ["union"]` |
| `identityField` | 請確定已定義所有有效的身分描述項。 |
| JSON | 確保JSON有效。 |
| 组织 | 確保列出的組織是有效的組織。 |
| 來源名稱 | 確保指定資料來源的名稱。 |
| 数据集 | 確保資料集已指定、啟用且未移除。 |
| 标头 | 確保標頭已指定且有效。 |

關於如何操作的更多資訊 [!DNL Platform] 監視及驗證資料可在以下網址找到： [監控資料流程檔案](./monitor-data-ingestion.md).

## 身分值驗證

下表概述您必須遵循的現有規則，以確保身分值成功驗證。

| 命名空间 | 驗證規則 | 違反規則時的系統行為 |
| --- | --- | --- |
| ECID | <ul><li>ECID的身分值必須剛好38個字元。</li><li>ECID的身分值只能包含數字。</li></ul> | <ul><li>如果ECID的身分值不完全是38個字元，則會略過記錄。</li><li>如果ECID的身分值包含非數字字元，則會略過記錄。</li></ul> |
| 非ECID | 身分值不可超過1024個字元。 | 如果身分值超過1024個字元，則會略過記錄。 |

如需詳細資訊，請參閱 [!DNL Identity Service] 護欄，請參閱 [[!DNL Identity Service] 護欄概述](../../identity-service/guardrails.md).
