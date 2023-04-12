---
keywords: Experience Platform；配置文件；实时客户配置文件；故障诊断；API；报表；数据集重叠报表；配置文件数据
title: 生成数据集重叠报表
type: Tutorial
description: 本教程概述了使用实时客户资料API生成数据集重叠报表所需的步骤。
exl-id: 90894ed3-b09e-435d-a9e3-18fd6dc8e907
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 1%

---

# 生成数据集重叠报表

数据集重叠报表可显示贵组织的构成 [!DNL Profile] 通过公开对可寻址受众（用户档案）贡献最大的数据集进行存储。

除了提供对数据的分析之外，此报表还可以帮助您采取措施来优化许可证使用情况，例如为特定数据的有效期设置限制。

本教程概述了使用 [!DNL Real-Time Customer Profile] API并解释贵组织的结果。

## 快速入门

要使用Adobe Experience Platform API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以收集所需标题所需的值。 要了解有关Experience PlatformAPI的更多信息，请参阅 [Platform API快速入门文档](../../landing/api-guide.md).

本教程中所有API调用所需的标头包括：

* `Authorization: Bearer {ACCESS_TOKEN}`:的 `Authorization` 标头需要前置有单词的访问令牌 `Bearer`. 必须每24小时生成一次新的访问令牌值。
* `x-api-key: {API_KEY}`:的 `API Key` 也称为a `Client ID` 和是一个只需生成一次的值。
* `x-gw-ims-org-id: {ORG_ID}`:组织ID只需生成一次。

完成身份验证教程并收集所需标头的值后，您便可以开始调用实时客户API。

## 使用命令行生成数据集重叠报表

如果您熟悉使用命令行，则可以使用以下cURL请求通过执行以下GET请求来生成数据集重叠报表： `/previewsamplestatus/report/dataset/overlap`.

**请求**

以下请求使用 `date` 参数来返回指定日期的最新报表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报表，则会返回该日期的最新报表。 如果指定日期不存在报表，则会返回HTTP状态404（未找到）错误。 如果未指定日期，则返回最近的报表。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**响应**

成功的请求会返回HTTP状态200（确定）和数据集重叠报表。 该报表包含 `data` 对象，包含以逗号分隔的数据集列表及其各自的配置文件计数。 有关如何阅读报表的详细信息，请参阅 [解释数据集重叠报表数据](#interpret-the-report) 稍后在本教程中介绍。

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

### 使用Postman生成数据集重叠报表

Postman是一个用于API开发的协作平台，可用于显示API调用。 可以从 [Postman网站](https://www.postman.com) 和为执行API调用提供了易于使用的UI。 以下屏幕截图使用Postman界面。

**请求**

要使用Postman请求数据集重叠报表，请完成以下步骤：

* 使用下拉菜单，选择GET作为请求类型。
* 在 `KEY` 列：
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* 在 `VALUE` 列，替换大括号(`{{ }}`)和大括号内的任何内容。
* 输入包含或不包含可选项的请求路径 `date` 参数：
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   或
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| 参数 | 描述 |
|---|---|
| `date` | 指定要返回的报表的日期。 如果在该日期运行了多个报表，则会返回该日期的最新报表。 如果指定日期不存在报表，则会返回HTTP状态404（未找到）错误。 如果未指定日期，则返回最近的报表。 <br/>格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

请求类型、标头、值和路径完成后，选择 **发送** 发送API请求并生成报表。

![](../images/dataset-overlap-report/postman-request.png)

**响应**

成功的请求会返回HTTP状态200（确定）和数据集重叠报表。 该报表包含 `data` 对象，包含以逗号分隔的数据集列表及其各自的配置文件计数。 有关如何阅读报表的详细信息，请参阅 [解释数据集重叠报表数据](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## 解释数据集重叠报表数据 {#interpret-the-report}

生成的数据集重叠报表提供了一个显示报表日期和时间的时间戳，以及一个数据对象，该数据对象包含以逗号分隔的列表形式的数据集ID的唯一组合。 以下各节提供了有关报表各组成部分的其他信息。

### 报表时间戳

的 `reportTimestamp` 与API请求中提供的日期匹配，或者如果未提供日期，则与最新报表的时间戳匹配。

### 数据集ID列表

的 `data` 对象包含以逗号分隔的列表形式表示的数据集ID的唯一组合，以及该数据集组合的相应配置文件计数。

>[!NOTE]
>
>与数据集重叠报表的每一行关联的所有配置文件计数之和应当等于您组织中的配置文件总数。

要解释报表的结果，请考虑以下示例：

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

此报表提供以下信息：

* 共有123个用户档案，其中包含来自以下数据集的数据： `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* 共有454,412个用户档案，包含来自以下两个数据集的数据： `5d92921872831c163452edc8` 和 `5eb2cdc6fa3f9a18a7592a98`.
* 有107个配置文件只包含来自数据集的数据 `5eeda0032af7bb19162172a7`.
* 组织共有454,642个用户档案。

## 后续步骤

完成本教程后，您现在可以使用实时客户资料API生成数据集重叠报表。 要了解有关在API和Experience PlatformUI中使用用户档案数据的更多信息，请首先阅读 [配置文件概述文档](../home.md).
