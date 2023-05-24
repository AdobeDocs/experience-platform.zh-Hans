---
keywords: 文字分類；文字分類
solution: Experience Platform
title: 內容與商務AI API中的文字分類
description: 文字分類服務在指定文字片段時，可以將它分類為一個或多個標籤。 分類可以是單一標籤、多標籤或階層式。
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 4%

---

# 文字分類

>[!NOTE]
>
>Content and Commerce AI為測試版。 檔案內容可能會有變動。

文字分類服務在指定文字片段時，可以將它分類為一個或多個標籤。 分類可以是單一標籤、多標籤或階層式。

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下請求會根據承載中提供的輸入引數來分類片段中的文字。 請參閱裝載範例下表，以瞭解有關所示輸入引數的詳細資訊。

>[!CAUTION]
>
>`analyzer_id` 決定哪些 [!DNL Sensei Content Framework] 已使用。 請檢查您是否擁有適當的 `analyzer_id` 進行要求之前。 聯絡Content and Commerce AI測試版團隊，接收您的 `analyzer_id` 以取得此服務。

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\", 
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"Server and Workstation Processors, Microcode Update is a self-extracting executable file containing the latest beta microcode updates (System Configuration Data) and software license agreement.\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
         "parameters": {}
    }]
}'
```

| 属性 | 描述 | 強制 |
| --- | --- | --- |
| `analyzer_id` | 此 [!DNL Sensei] 您的請求部署在下的服務ID。 此ID會決定 [!DNL Sensei Content Frameworks] 已使用。 若要使用自訂服務，請聯絡Content and Commerce AI團隊以設定自訂ID。 | 是 |
| `application-id` | 已建立之應用程式的ID。 | 是 |
| `data` | 一個陣列，其中包含JSON物件，而陣列中的每個物件都代表一個檔案。 在此陣列中傳遞的任何引數都會覆寫在 `data` 陣列。 此表格中下面列出的任何剩餘屬性，都可以從內覆寫 `data`. | 是 |
| `language` | 輸入文字的語言。 默认值为 `en`。 | 否 |
| `content-type` | 用於指出輸入是請求內文的一部分，還是S3儲存貯體的已簽署URL。 此屬性的預設值為 `inline`. | 否 |
| `encoding` | 輸入文字的編碼格式。 這可以是 `utf-8` 或 `utf-16`. 此屬性的預設值為 `utf-8`. | 否 |
| `threshold` | 分數臨界值（0至1），超過該臨界值即需要傳回結果。 使用值 `0` 以傳回所有結果。 此屬性的預設值為 `0`. | 否 |
| `top-N` | 要傳回的結果數（不能為負整數）。 使用值 `0` 以傳回所有結果。 當與搭配使用時 `threshold`，傳回的結果數是設定的任一限制中的較小值。 此屬性的預設值為 `0`. | 否 |
| `custom` | 任何要傳遞的自訂引數。 此屬性需要有效的JSON物件才能運作。 | 否 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 如果未傳遞此專案，則會指派自動產生的ID。 | 否 |
| `content` | 文字分類服務使用的內容。 內容可以是原始文字（「inline」內容型別）。 <br> 如果內容是S3上的檔案（「s3-bucket」內容型別），請傳遞已簽署的URL。 | 是 |

**响应**

成功的回應會傳回回應陣列中的分類文字。

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_name": "abc123",
            "feature_value": [
              {
                "feature_value": [
                  {
                    "feature_value": 0.6899315714836121,
                    "feature_name": "Embedded & IoT"
                  }
                ],
                "feature_name": "labels"
              },
              {
                "feature_name": "status",
                "feature_value": "success"
              }
            ]
          }
        ]
      }
    }
  ],
  "error": []
}
```
