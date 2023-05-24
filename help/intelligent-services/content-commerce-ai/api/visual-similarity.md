---
keywords: 視覺相似度；視覺相似度；ccai api
solution: Experience Platform
title: Content and Commerce AI API中的視覺相似度
description: 視覺相似度服務在指定影像時，會自動從目錄中尋找視覺上相似的影像。
exl-id: fe31d9be-ee42-44fa-b83f-3b8a718cb4e3
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---

# 視覺相似度

>[!NOTE]
>
>[!DNL Content and Commerce AI] 為測試版。 檔案內容可能會有變動。

視覺相似度服務在指定影像時，會自動從目錄中尋找視覺上相似的影像。

本檔案所示的範例請求中使用了下列影像：

![測試影像](../images/Query_Image.jpeg)

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下請求會根據裝載中提供的輸入引數，從目錄中擷取視覺上類似的影像。 請參閱裝載範例下表，以瞭解有關所示輸入引數的詳細資訊。

>[!CAUTION]
>
>`analyzer_id` 決定哪些 [!DNL Sensei Content Framework] 已使用。 請檢查您是否擁有適當的 `analyzer_id` 進行要求之前。 聯絡Content and Commerce AI測試版團隊，接收您的 `analyzer_id` 以取得此服務。

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer $API_TOKEN' \
  -H 'Content-Type: multipart/form-data' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-api-key: $API_KEY' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
         "parameters": {
          "application-id": "1234", 
          "content-type": "inline", 
          "encoding": "jpeg", 
          "threshold": "0", 
          "top-N": "0", 
          "custom": {}, 
          "data": [{
            "content-id": "0987", 
            "content": "inline-image", 
            "content-type": "inline", 
            "encoding": "jpeg", 
            "threshold": "0", 
            "top-N": "0", 
            "historic-metadata": [], 
            "custom": {}
            }]
          }
      }
    ]
}'
```

| 属性 | 描述 | 強制 |
| --- | --- | --- |
| `analyzer_id` | 此 [!DNL Sensei] 您的請求部署在下的服務ID。 此ID會決定 [!DNL Sensei Content Frameworks] 已使用。 若要使用自訂服務，請聯絡Content and Commerce AI團隊以設定自訂ID。 | 是 |
| `application-id` | 您建立之應用程式的ID。 | 是 |
| `data` | 一個陣列，其中包含JSON物件，且陣列中的每個物件都代表一個影像。 在此陣列中傳遞的任何引數都會覆寫在 `data` 陣列。 此表格中下面列出的任何剩餘屬性，都可以從內覆寫 `data`. | 是 |
| `content-id` | 回應中傳回之資料元素的唯一ID。 如果未傳遞，則會指派自動產生的ID。 | 否 |
| `content` | 視覺相似度服務要分析的內容。 如果影像是請求內文的一部分，請使用 `-F file=@<filename>` 在curl命令中傳遞影像，將此引數保留為空字串。 <br> 如果影像是S3上的檔案，請傳遞已簽署的URL。 當內容是請求內文的一部分時，資料元素清單應該只有一個物件。 如果傳遞了多個物件，則只會處理第一個物件。 | 是 |
| `content-type` | 用於指出輸入是請求內文的一部分，還是S3儲存貯體的已簽署URL。 此屬性的預設值為 `inline`. | 否 |
| `encoding` | 輸入影像的檔案格式。 目前只能處理JPEG和PNG影像。 此屬性的預設值為 `jpeg`. | 否 |
| `threshold` | 分數臨界值（0至1），超過該臨界值即需要傳回結果。 使用值 `0` 以傳回所有結果。 此屬性的預設值為 `0`. | 否 |
| `top-N` | 要傳回的結果數（不能為負整數）。 使用值 `0` 以傳回所有結果。 當與搭配使用時 `threshold`，傳回的結果數是設定的任一限制中的較小值。 此屬性的預設值為 `0`. | 否 |
| `custom` | 任何要傳遞的自訂引數。 | 否 |
| `historic-metadata` | 可傳遞中繼資料的陣列。 | 否 |

**响应**

成功的回應會傳回 `response` 包含 `feature_value` 和 `feature_name` 目錄中找到每個視覺上相似的影像。

下列視覺上相似的影像會傳回至下列範例回應中：

![類似影像](../images/results.jpg)

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "678",
                "feature_name": "G34WS945.F1"
              },
              {
                "feature_value": "678",
                "feature_name": "1431RDM JANELLE RAW JACKE"
              },
              {
                "feature_value": "657",
                "feature_name": "GF4045877841 CARLA FLR"
              },
              {
                "feature_name": "1707-686-SGU PATCH XYZ",
                "feature_value": "657"
              },
              {
                "feature_name": "5495MJT AJA BLK",
                "feature_value": "646"
              },
              {
                "feature_name": "IDEAL",
                "feature_value": "645"
              },
              {
                "feature_value": "644",
                "feature_name": "HCAJRA439 CALI JEAN"
              },
              {
                "feature_name": "KT279RK-ONL",
                "feature_value": "644"
              },
              {
                "feature_name": "SP190404-ELLIS",
                "feature_value": "642"
              },
              {
                "feature_name": "GF4174848718 KENDALL DIS",
                "feature_value": "640"
              }
            ],
            "feature_name": "visual_similarity"
          }
        ]
      }
    }
  ],
  "error": []
}
```
