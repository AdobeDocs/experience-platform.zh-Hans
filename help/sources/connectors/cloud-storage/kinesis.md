---
keywords: Experience Platform；首頁；熱門主題；Amazon Kinesis；amazon kinesis；Kinesis；kinesis
solution: Experience Platform
title: Amazon Kinesis來源聯結器總覽
description: 瞭解如何使用API或使用者介面將Amazon Kinesis連結至Adobe Experience Platform。
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] 聯結器

Adobe Experience Platform為AWS等雲端服務供應商提供原生連線， [!DNL Google Cloud Platform]、和 [!DNL Azure]. 您可以將來自這些系統的資料帶入 [!DNL Platform].

雲端儲存空間來源可將您自己的資料帶入 [!DNL Platform] 而不需要下載、格式化或上傳。 內嵌的資料可以格式化為XDM JSON、XDM Parquet或分隔。 流程的每個步驟都會整合至來源工作流程。 [!DNL Platform] 可讓您從匯入資料 [!DNL Amazon Kinesis] 即時。

>[!NOTE]
>
>的縮放因數 [!DNL Kinesis] 如果您需要擷取大量資料，則必須增加。 目前，您可從以下來源取得的最大資料量： [!DNL Kinesis] account to Platform是每秒4000筆記錄。 若要擴充並擷取較大量的資料，請聯絡您的Adobe代表。

## 先决条件

下節提供建立之前所需的先決條件設定的進一步資訊 [!DNL Kinesis] 來源連線。

### 設定存取原則

A [!DNL Kinesis] 串流需要下列許可權才能建立來源連線：

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

這些許可權是透過 [!DNL Kinesis] 主控台和會在您輸入認證並選取資料流後，由Platform檢查。

以下範例顯示建立「 」所需的最低存取許可權 [!DNL Kinesis] 來源連線。

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:GetShardIterator",
                "kinesis:GetRecords",
                "kinesis:DescribeStream",
                "kinesis:ListStreams"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `kinesis:GetShardIterator` | 需要用來周遊記錄的動作。 |
| `kinesis:GetRecords` | 從特定位移或分片ID取得記錄所需的動作。 |
| `kinesis:DescribeStream` | 此動作會傳回有關串流的資訊，包括產生分片ID所需的分片對應。 |
| `kinesis:ListStreams` | 列出您可從UI選取的可用串流所需的動作。 |

如需控制存取許可權的詳細資訊，請參閱： [!DNL Kinesis] 資料串流，請參閱下列內容 [[!DNL Kinesis] 檔案](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### 設定疊代器型別

[!DNL Kinesis] 支援下列疊代器型別，可讓您指定讀取資料的順序：

| 迭代器型別 | 描述 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 從由特定序號識別的位置開始讀取資料。 |
| `AFTER_SEQUENCE_NUMBER` | 從特定序號所識別的位置之後，開始讀取資料。 |
| `AT_TIMESTAMP` | 從由特定時間戳記所識別的位置開始讀取資料。 |
| `TRIM_HORIZON` | 從最舊的資料記錄開始讀取資料。 |
| `LATEST` | 從最近的資料記錄開始讀取資料。 |

A [!DNL Kinesis] UI來源目前僅支援 `TRIM_HORIZON`，而API同時支援兩者 `TRIM_HORIZON` 和 `LATEST` 作為取得資料的模式。 Platform使用的預設疊代器值 [!DNL Kinesis] 來源為 `TRIM_HORIZON`.

如需疊代器型別的詳細資訊，請參閱下列內容 [[!DNL Kinesis] 檔案](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Connect [!DNL Amazon Kinesis] 至 [!DNL Platform]

以下檔案提供有關如何連線的資訊 [!DNL Amazon Kinesis] 至 [!DNL Platform] 使用API或使用者介面：

### 使用API

- [使用流量服務API建立Amazon Kinesis來源連線](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用流量服務API收集串流資料](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在使用者介面中建立Amazon Kinesis來源連線](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中設定雲端儲存體連線的資料流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
