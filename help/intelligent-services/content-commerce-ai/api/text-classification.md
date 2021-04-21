---
keywords: 文本分类；文本分类
solution: Experience Platform, Intelligent Services
title: 内容和商务AI API中的文本分类
topic-legacy: Developer guide
description: 给定文本片段时，文本分类服务可将其分类为一个或多个标签。 分类可以是单标签、多标签或分层。
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 4%

---

# 文本分类

>[!NOTE]
>
>Content and Commerce AI是Beta版。 文档可能会更改。

给定文本片段时，文本分类服务可将其分类为一个或多个标签。 分类可以是单标签、多标签或分层。

**API格式**

```http
POST /services/v1/predict
```

**请求**

以下请求基于在有效负荷中提供的输入参数对来自片段的文本进行分类。 有关所示输入参数的详细信息，请参阅示例有效负荷下表。

>[!CAUTION]
>
>`analyzer_id` 确定 [!DNL Sensei Content Framework] 使用的。在发出请求之前，请检查您是否有正确的`analyzer_id`。 请与内容和商务AI测试版团队联系，以接收此服务的`analyzer_id`。

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

| 属性 | 描述 | 必填 |
| --- | --- | --- |
| `analyzer_id` | 您的请求部署到的[!DNL Sensei]服务ID。 此ID决定使用哪个[!DNL Sensei Content Frameworks]。 有关自定义服务，请联系内容和商务AI团队以设置自定义ID。 | 是 |
| `application-id` | 创建的应用程序的ID。 | 是 |
| `data` | 一个数组，其中包含一个JSON对象，数组中的每个对象都表示一个文档。 作为此数组的一部分传递的任何参数都将覆盖在`data`数组外部指定的全局参数。 下表中列出的所有其余属性都可从`data`中覆盖。 | 是 |
| `language` | 输入文本的语言。 默认值为 `en`。 | 否 |
| `content-type` | 用于指示输入是请求主体的一部分还是S3存储段的已签名URL。 此属性的默认值为`inline`。 | 否 |
| `encoding` | 输入文本的编码格式。 这可以是`utf-8`或`utf-16`。 此属性的默认值为`utf-8`。 | 否 |
| `threshold` | 需要返回结果的分数阈值（0到1）。 使用值`0`返回所有结果。 此属性的默认值为`0`。 | 否 |
| `top-N` | 要返回的结果数（不能为负整数）。 使用值`0`返回所有结果。 与`threshold`一起使用时，返回的结果数是任一限制集中的较小者。 此属性的默认值为`0`。 | 否 |
| `custom` | 要传递的任何自定义参数。 此属性需要有效的JSON对象才能正常工作。 | 否 |
| `content-id` | 在响应中返回的数据元素的唯一ID。 如果未传递，则分配一个自动生成的ID。 | 否 |
| `content` | 文本分类服务使用的内容。 内容可以是原始文本（“内联”内容类型）。 <br> 如果内容是S3(&#39;s3-bucket&#39; content-type)上的文件，请传递已签名的url。 | 是 |

**响应**

成功的响应会返回响应数组中的分类文本。

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
