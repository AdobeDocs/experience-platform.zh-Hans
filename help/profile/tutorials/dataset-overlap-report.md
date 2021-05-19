---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API;报告；数据集重叠报告；用户档案数据
title: 生成数据集重叠报表
type: Tutorial
description: 本教程概述了使用实时客户用户档案API生成数据集重叠报表所需的步骤。
source-git-commit: f30f87527f5e903c851a140e7cbaad1964a48803
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---


# 生成数据集重叠报告

数据集重叠报表可公开对可寻址受众(用户档案)贡献最大的数据集，从而使您能够了解组织[!DNL Profile]存储的构成。

除了提供对数据的洞察外，此报告还可以帮助您采取措施优化许可证使用情况，如设置特定数据使用寿命的限制。

本教程概述了使用[!DNL Real-time Customer Profile] API生成数据集重叠报告并解释组织结果所需的步骤。

## 入门指南

要使用Adobe Experience Platform API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)以收集所需标头所需的值。 要了解有关Experience Platform API的更多信息，请参阅[平台API快速入门文档](../../landing/api-guide.md)。

本教程中所有API调用的所需标头为：

* `Authorization: Bearer {ACCESS_TOKEN}`:标 `Authorization` 题需要以单词为前缀的访问令牌 `Bearer`。必须每24小时生成一个新访问令牌值。
* `x-api-key: {API_KEY}`:它 `API Key` 也称为a， `Client ID` 是只需生成一次的值。
* `x-gw-ims-org-id: {IMS_ORG}`:它 `IMS Org` 也称为，只 `Organization ID` 需生成一次。

完成身份验证教程并收集所需标头的值后，即可开始调用实时客户API。

## 使用命令行生成数据集重叠报告

如果您熟悉使用命令行，可以通过执行`/previewsamplestatus/report/dataset/overlap`GET请求，使用以下cURL请求生成数据集重叠报告。

**请求**

以下请求使用`date`参数返回指定日期的最新报表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报表，则返回该日期的最新报表。 如果指定日期不存在报告，则返回HTTP状态404（未找到）错误。 如果未指定日期，则返回最近的报表。 格式：YYYY-MM-DD。 示例: `date=2024-12-31` |

**响应**

成功的请求返回HTTP状态200(OK)和数据集重叠报告。 报表包括`data`对象，包含以逗号分隔的列表集及其各自的用户档案计数。 有关如何阅读报告的详细信息，请参阅本教程后面关于[解释数据集重叠报告数据](#interpret-the-report)的部分。

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-04-19T19:55:31.147"
}
```

### 使用Postman生成数据集重叠报告

Postman是用于API开发的协作平台，对于可视化API调用非常有用。 它可从[Postman网站](https://www.postman.com)免费下载，并提供用于执行API调用的易用UI。 以下屏幕截图使用Postman界面。

**请求**

要使用Postman请求数据集重叠报表，请完成以下步骤：

* 使用下拉列表，选择GET作为请求类型。
* 在`KEY`列中输入所需的标题：
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* 在`VALUE`列中输入身份验证过程中生成的值，替换大括号(`{{ }}`)和大括号内的任何内容。
* 输入包含或不包含可选`date`参数的请求路径：
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   或
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报表，则返回该日期的最新报表。 如果指定日期不存在报告，则返回HTTP状态404（未找到）错误。 如果未指定日期，则返回最近的报表。 <br/>格式：YYYY-MM-DD。示例: `date=2024-12-31` |

完成请求类型、标头、值和路径后，选择&#x200B;**发送**&#x200B;以发送API请求并生成报告。

![](../images/dataset-overlap-report/postman-request.png)

**响应**

成功的请求返回HTTP状态200(OK)和数据集重叠报告。 报表包括`data`对象，包含以逗号分隔的列表集及其各自的用户档案计数。 有关如何读取报告的详细信息，请参阅[解释数据集重叠报告数据](#interpret-the-report)部分。

![](../images/dataset-overlap-report/postman-response.png)

## 解释数据集重叠报告数据{#interpret-the-report}

生成的数据集重叠报表提供显示报表日期和时间的时间戳，以及包含数据集ID的唯一组合(以逗号分隔的列表)的数据对象。 以下各节提供了有关报告各组成部分的更多信息。

### 报表时间戳

`reportTimestamp`与API请求中提供的日期匹配，或者如果未提供日期，则与最近报告的时间戳匹配。

### 列表数据集ID

`data`对象包含数据集ID的唯一组合，作为逗号分隔的列表，以及数据集组合的相应用户档案计数。

>[!NOTE]
>
>与用户档案集重叠报表的每行关联的所有用户档案计数之和应等于组织中的总数。

要解释报表的结果，请考虑以下示例：

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

此报告提供以下信息：
* 有123个用户档案，包括来自以下数据集的数据：`5d92921872831c163452edc8`、`5da7292579975918a851db57`、`5eb2cdc6fa3f9a18a7592a98`。
* 共有454,412个用户档案，包括来自这两个数据集的数据：`5d92921872831c163452edc8`和`5eb2cdc6fa3f9a18a7592a98`。
* 有107个用户档案只包含来自数据集`5eeda0032af7bb19162172a7`的数据。
* 本组织共有454 642名用户档案。

## 后续步骤

完成本教程后，您现在可以使用实时客户用户档案API生成数据集重叠报表。 要了解有关在API和Experience Platform UI中使用用户档案数据的更多信息，请首先阅读[用户档案概述文档](../home.md)。