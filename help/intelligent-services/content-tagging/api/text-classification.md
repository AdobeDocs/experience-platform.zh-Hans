---
keywords: 文本分类；文本分类
solution: Experience Platform
title: Content and Commerce AI API中的文本分类
description: 为文本片段指定文本分类服务时，可以将其分类为一个或多个标签。 分类可以是单标签、多标签或分层。
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: 081e31727b4e78126e60896b3b850c5589526152
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 4%

---

# 文本分类

>[!NOTE]
>
>Content and Commerce AI处于测试阶段。 文档可能会发生更改。

为文本片段指定文本分类服务时，可以将其分类为一个或多个标签。 分类可以是单标签、多标签或分层。

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下请求根据有效负载中提供的输入参数分类片段中的文本。 有关显示的输入参数的更多信息，请参阅示例有效负载下表。

>[!CAUTION]
>
>`analyzer_id` 确定哪些 [!DNL Sensei Content Framework] 已使用。 请检查您是否拥有 `analyzer_id` 然后再提出请求。 联系Content and Commerce AI测试版团队，接收 `analyzer_id` 用于此服务。

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

| 属性 | 描述 | 必需 |
| --- | --- | --- |
| `analyzer_id` | 此 [!DNL Sensei] 您的请求部署在下的服务ID。 此ID确定 [!DNL Sensei Content Frameworks] 已使用。 对于自定义服务，请联系内容和商务AI团队以设置自定义ID。 | 是 |
| `application-id` | 创建的应用程序的ID。 | 是 |
| `data` | 一个数组，其中包含一个JSON对象，该数组中的每个对象都表示一个文档。 作为此数组的一部分传递的任何参数都将覆盖 `data` 数组。 此表下面列出的任何剩余属性都可从中覆盖 `data`. | 是 |
| `language` | 输入文本的语言。 默认值为 `en`。 | 否 |
| `content-type` | 用于指示输入是请求正文的一部分，还是S3存储桶的已签名URL。 此属性的默认值为 `inline`. | 否 |
| `encoding` | 输入文本的编码格式。 这可以是 `utf-8` 或 `utf-16`. 此属性的默认值为 `utf-8`. | 否 |
| `threshold` | 分数阈值（0到1），超过该阈值需要返回结果。 使用值 `0` 以返回所有结果。 此属性的默认值为 `0`. | 否 |
| `top-N` | 要返回的结果数（不能为负整数）。 使用值 `0` 以返回所有结果。 当与结合使用时 `threshold`，则返回的结果数是设置的任一限制中的较小值。 此属性的默认值为 `0`. | 否 |
| `custom` | 要传递的任何自定义参数。 此属性需要有效的JSON对象才能正常工作。 | 否 |
| `content-id` | 响应中返回的数据元素的唯一ID。 如果未传递此ID，则会分配自动生成的ID。 | 否 |
| `content` | 文本分类服务使用的内容。 内容可以是原始文本（“inline”内容类型）。 <br> 如果内容是S3上的文件（“s3-bucket”内容类型），请传递已签名的URL。 | 是 |

**响应**

成功的响应在响应数组中返回分类文本。

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
