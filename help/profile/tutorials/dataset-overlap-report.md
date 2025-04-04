---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API；报表；数据集重叠报表；配置文件数据
title: 生成数据集重叠报表
type: Tutorial
description: 本教程概述了使用实时客户档案API生成数据集重叠报表所需的步骤。
exl-id: 90894ed3-b09e-435d-a9e3-18fd6dc8e907
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 1%

---

# 生成数据集重叠报告

数据集重叠报表通过公开对可寻址受众（用户档案）贡献最大的数据集，提供了对组织[!DNL Profile]存储构成的可见性。

除了提供数据见解外，此报表还可以帮助您采取措施优化许可证使用，例如设置特定数据生命周期的限制。

本教程概述了使用[!DNL Real-Time Customer Profile] API生成数据集重叠报告并解释组织结果所需的步骤。

## 快速入门

要使用Adobe Experience Platform API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，以收集所需标头所需的值。 要了解有关Experience Platform API的更多信息，请参阅[Experience Platform API快速入门文档](../../landing/api-guide.md)。

本教程中的所有API调用所需的标头包括：

* `Authorization: Bearer {ACCESS_TOKEN}`： `Authorization`标头需要前缀为`Bearer`字的访问令牌。 必须每24小时生成一个新的访问令牌值。
* `x-api-key: {API_KEY}`： `API Key`也称为`Client ID`，是一个只需生成一次的值。
* `x-gw-ims-org-id: {ORG_ID}`：组织ID只需生成一次。

完成身份验证教程并收集所需标头的值后，便可以开始调用Real-time Customer API。

## 使用命令行生成数据集重叠报告

如果您熟悉使用命令行，则可以使用以下cURL请求，通过向`/previewsamplestatus/report/dataset/overlap`执行GET请求来生成数据集重叠报表。

**请求**

以下请求使用`date`参数返回指定日期的最新报告。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报告，则返回该日期的最新报告。 如果指定日期不存在报表，则会返回HTTP状态404（未找到）错误。 如果未指定日期，则返回最近的报告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**响应**

成功的请求会返回HTTP状态200 （正常）和数据集重叠报表。 该报告包含一个`data`对象，其中包含以逗号分隔的数据集列表及其各自的配置文件计数。 有关如何读取该报表的详细信息，请参阅本教程后面关于[解释数据集重叠报表数据](#interpret-the-report)的部分。

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

Postman是API开发的协作平台，用于可视化API调用。 可以从[Postman网站](https://www.postman.com)免费下载它，并提供用于执行API调用的易于使用的UI。 以下屏幕截图使用Postman界面。

**请求**

要使用Postman请求数据集重叠报表，请完成以下步骤：

* 使用下拉列表，选择GET作为请求类型。
* 在`KEY`列中输入所需的标题：
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* 将验证期间生成的值输入到`VALUE`列中，并替换大括号(`{{ }}`)和大括号内的任何内容。
* 输入带有或不带有可选`date`参数的请求路径：
  `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
  或
  `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报告，则返回该日期的最新报告。 如果指定日期不存在报表，则会返回HTTP状态404（未找到）错误。 如果未指定日期，则返回最近的报告。 <br/>格式： YYYY-MM-DD。 示例：`date=2024-12-31` |

完成请求类型、标头、值和路径后，选择&#x200B;**发送**&#x200B;以发送API请求并生成报告。

![](../images/dataset-overlap-report/postman-request.png)

**响应**

成功的请求会返回HTTP状态200 （正常）和数据集重叠报表。 该报告包含一个`data`对象，其中包含以逗号分隔的数据集列表及其各自的配置文件计数。 有关如何读取报告的详细信息，请参阅[中关于解释数据集重叠报告数据](#interpret-the-report)的部分。

![](../images/dataset-overlap-report/postman-response.png)

## 解释数据集重叠报表数据 {#interpret-the-report}

生成的数据集重叠报表提供了一个显示报表日期和时间的时间戳，以及一个数据对象，其中包含以逗号分隔的列表形式唯一的数据集ID组合。 以下部分提供了有关报告组件的其他信息。

### 报告时间戳

`reportTimestamp`与API请求中提供的日期匹配，如果未提供日期，则与最新报告的时间戳匹配。

### 数据集ID

`data`对象包括唯一的数据集ID组合，这些数据集ID以逗号分隔列表，分别与该数据集组合的配置文件计数相对应。

>[!NOTE]
>
>与数据集重叠报表的每一行关联的所有配置文件计数的总和应等于贵组织中的配置文件总数。

要解释报表的结果，请考虑以下示例：

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

此报表提供以下信息：

* 有123个配置文件包含来自以下数据集的数据： `5d92921872831c163452edc8`、`5da7292579975918a851db57`、`5eb2cdc6fa3f9a18a7592a98`。
* 有454,412个配置文件包含来自这两个数据集的数据：`5d92921872831c163452edc8`和`5eb2cdc6fa3f9a18a7592a98`。
* 有107个配置文件仅包含来自数据集`5eeda0032af7bb19162172a7`的数据。
* 该组织共有454,642个用户档案。

## 后续步骤

完成本教程后，您现在可以使用实时客户档案API生成数据集重叠报表。 要了解有关在API和Experience Platform UI中使用配置文件数据的更多信息，请从阅读[配置文件概述文档](../home.md)开始。
