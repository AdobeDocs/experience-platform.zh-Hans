---
keywords: 文本分类；文本分类
solution: Experience Platform
title: 内容和Commerce AI API中的文本分类
description: 文本分类服务在给定文本片段时，可以将其分类为一个或多个标签。 分类可以是单标签、多标签或分层。
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 4%

---

# 文本分类

>[!NOTE]
>
>Content和Commerce AI处于测试阶段。 文档可能会发生更改。

文本分类服务在给定文本片段时，可以将其分类为一个或多个标签。 分类可以是单标签、多标签或分层。

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下请求根据有效负载中提供的输入参数对片段中的文本进行分类。 有关显示的输入参数的更多信息，请参阅示例有效负载下方的表。

>[!CAUTION]
>
>`analyzer_id`确定使用哪个[!DNL Sensei Content Framework]。 在提出请求之前，请检查您是否拥有适当的`analyzer_id`。 请联系内容和Commerce AI测试版团队，接收您关于此服务的`analyzer_id`。

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
| `analyzer_id` | 您的请求部署所在的[!DNL Sensei]服务ID。 此ID确定使用了[!DNL Sensei Content Frameworks]中的哪一个。 对于自定义服务，请联系内容和Commerce AI团队以设置自定义ID。 | 是 |
| `application-id` | 已创建应用程序的ID。 | 是 |
| `data` | 一个数组，其中包含一个JSON对象，该数组中的每个对象表示一个文档。 作为此数组的一部分传递的任何参数都将覆盖`data`数组外部指定的全局参数。 此表格中下面列出的任何剩余属性都可以从`data`中覆盖。 | 是 |
| `language` | 输入文本的语言。 默认值为 `en`。 | 否 |
| `content-type` | 用于指示输入是请求正文的一部分还是S3存储桶的已签名URL。 此属性的默认值为`inline`。 | 否 |
| `encoding` | 输入文本的编码格式。 这可以是`utf-8`或`utf-16`。 此属性的默认值为`utf-8`。 | 否 |
| `threshold` | 分数阈值（0到1），超过该阈值需要返回结果。 使用值`0`返回所有结果。 此属性的默认值为`0`。 | 否 |
| `top-N` | 要返回的结果数（不能为负整数）。 使用值`0`返回所有结果。 当与`threshold`一起使用时，返回的结果数是设置的任一限制中的较小值。 此属性的默认值为`0`。 | 否 |
| `custom` | 要传递的任何自定义参数。 此属性需要一个有效的JSON对象才能正常工作。 | 否 |
| `content-id` | 响应中返回的数据元素的唯一ID。 如果未传递此，则会分配自动生成的ID。 | 否 |
| `content` | 文本分类服务使用的内容。 内容可以是原始文本（“inline”内容类型）。 <br>如果内容是S3 （&#39;s3-bucket&#39;内容类型）上的文件，请传递已签名的URL。 | 是 |

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
