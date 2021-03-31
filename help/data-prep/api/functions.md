---
keywords: Experience Platform；主页；热门主题；数据准备；api指南；模式;
solution: Experience Platform
title: 模式API端点
topic: 模式
description: '您可以使用Adobe Experience Platform API中的“/functions”端点验证映射表达式和列表可用的映射集函数。 '
translation-type: tm+mt
source-git-commit: 60c80a73deb8c77f19d5963cc3319d46143fb4c3
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 2%

---


# 函数端点

映射集函数允许您在源模式和目标应用程序之间转换数据。 您可以使用`/languages/el`端点验证表达式，并获取所有可用映射集函数的列表。

## 验证表达式

您可以通过向`/languages/el/validate`端点发出POST请求来验证当前表达式是否有效。

**API格式**

```
POST /languages/el/validate
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/languages/el/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "expression": "concat(\"Hi\", \",\", \"there\", \"!\")"
  }'
```

**响应**

成功的响应返回HTTP状态200，验证状态为表达式。

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## 列表映射集函数

通过向`/languages/el/functions`端点发出GET请求，可以检索所有可用映射集函数的列表。

**API格式**

```
GET /languages/el/functions
```

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/functions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，并列表所有可用的映射集函数。

>[!NOTE]
>
>此响应已截断空间。

```json
[
    {
        "category": "Date / Time",
        "function": "date",
        "description": "Function that converts date string into a ZonedDateTime object.",
        "syntax": "ZonedDateTime date(String, String, ZonedDateTime)",
        "returns": "Returns the date object that is formatted in given format or a default date if the expression evaluates to a null date.",
        "returnType": "java.time.ZonedDateTime",
        "example": "",
        "result": "",
        "params": [],
        "since": 1
    },
    {
        "category": "Hierarchies - Arrays",
        "function": "first",
        "description": "Function to retrieve the first element of the given array.",
        "syntax": "T first(T...)",
        "returns": "The first element or null if the array is null or empty.",
        "returnType": "java.lang.Object",
        "example": "first(\"1\", \"2\", \"3\")",
        "result": "\"1\"",
        "params": [
            {
                "name": "values",
                "description": "Zero or more arguments",
                "type": "object",
                "dataType": "[Ljava.lang.Object;",
                "position": 1
            }
        ],
        "since": 1
    }
]
```

## 列表映射集运算符

通过向`/languages/el/operators`端点发出GET请求，可以检索所有可用的映射集运算符的列表。

**API格式**

```
GET /languages/el/operators
```

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/operators \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，并列表所有可用的映射集运算符。

>[!NOTE]
>
>此响应已截断空间。

```json
[
    {
        "operatorSymbol": "+",
        "methodName": "add",
        "numberOfOperands": 2,
        "description": "Simple arithmetic addition",
        "example": "1 + 2"
    },
    {
        "operatorSymbol": "/",
        "methodName": "divide",
        "numberOfOperands": 2,
        "description": "Simple arithmetic division",
        "example": "1 / 2"
    },
    {
        "operatorSymbol": "~",
        "methodName": "complement",
        "numberOfOperands": 1,
        "description": "The usual ~ operator is used, e.g.\n~33\n, ~0010 0001 = 1101 1110 = -34.",
        "example": "~44"
    },
    {
        "operatorSymbol": "-",
        "methodName": "negate",
        "numberOfOperands": 1,
        "description": "The unary - operator is used. For example\n-12",
        "example": "-12"
    },
    {
        "operatorSymbol": "!",
        "methodName": "not",
        "numberOfOperands": 1,
        "description": "The usual ! operator can be used as well as the word not, e.g.\n!cond1\nand\nnot cond1\nare equivalent",
        "example": "!cond1"
    }
]
```
