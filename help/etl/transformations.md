---
keywords: Experience Platform；主页；热门主题；ETL；ETL转换；ETL转换
solution: Experience Platform
title: 示例ETL转换
description: 本文演示了提取、转换、加载(ETL)开发人员可以遇到的以下示例转换。
exl-id: 8084f5fd-b621-4515-a329-5a06c137d11c
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---

# 示例ETL转换

本文演示了提取、转换、加载(ETL)开发人员可以遇到的以下示例转换。

## 平面CSV到层次结构

### 示例文件

可从由Adobe维护的公共ETL引用[!DNL GitHub]存储库中获得示例CSV和JSON文件：

- [CRM_profiles.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_profiles.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)

### 示例CSV

以下CRM数据已导出为`CRM_profiles.csv`：

```shell
TITLE   F_NAME  L_NAME  GENDER  DOB EMAIL   CRMID   ECID    LOYALTYID   ECID2   PHONE   STREET  CITY    STATE   COUNTRY ZIP LAT LONG
Mr  Ewart   Bennedsen   M   2004-09-25  ebennedsenex@jiathis.com    71a16013-d805-7ece-9ac4-8f2cd66e8eaa    87098882279810196101440938110216748923  2e33192000007456-0365c00000000000   55019962992006103186215643814973128178  256-284-7231    72 Buhler Crossing  Anniston    Alabama US  36205   33.708276   -85.7922905
Dr  Novelia Ansteys F   1987-10-31  nansteysdk@spotify.com  2eeb6532-82e1-0d58-8955-bf97de66a6f5    50829196174854544323574004005273946998  2e3319208000765b-3811c00000000001   65233136134594262632703695260919939885  704-181-6371    79 Northfield Hill  Charlotte   North Carolina  US  28299   35.2188655  -80.8108885
Mr  Ulises  Mochan  M   1996-03-20  umochanco@gnu.org   6f393075-addb-bdd6-73f8-31c393b700f5    70086119428645095847094710218289660855  2e33192080003023-26b2000000000002   82011353387947708954389153068944017636  720-837-4159    00671 Mifflin Trail Lacolle Qu√&copy;bec CA  E5A 45.08338    -73.36585
Mrs Friederike  Durrell F   1979-01-3   fdurrellbj@utexas.edu   33d018ec-5fed-f1a3-56aa-079370a9511b    50164729868919217963697788808932473456  2e33192080006dfc-0cdf400000000003   64452712468609735658703639722261004071  798-528-3458    47 Fremont Hill Independencia   Veracruz Llave  MX  91891   19.3803931  -99.1476905
Rev Evita   Bingall F   1974-02-28  ebingallod@mac.com  8c93db88-f328-8efb-dc73-d5654d371cbe    74973364195185450328832136951985519627  2e331920800038db-0559e00000000004   58945501950285346322834356669253860483  397-178-5897    56 Crescent Oaks Court  Buenavista  Oaxaca  MX  71730   19.4458447  -99.1497665
Mr  Eugenie Bechley F   1969-05-19  ebechley9r@telegraph.co.uk  b0c76a3f-6526-0ad0-e050-48143b687d18    67119779213799783658184754966135750376  2e331920800001a4-24b2800000000005   59715249079109455676103900762283358508  718-374-7456    5760 Southridge Junction    Staten Island   New York    US  10310   40.6307451  -74.1181235
Dr  Cammi   Haslen  F   1973-12-17  chaslenqv@ehow.com  56059cd5-5006-ce5f-2f5f-15b4d856a204    61747117963243728095047674165570746095  2e33192080007c25-2ec0600000000006   86268258269066295956223980330791223320  865-538-8291    83 Veith Street Knoxville   Tennessee   US  37995   35.95   -84.05
```

### 映射

下表概述了CRM数据的映射要求，并包括以下转换：

- `identityMap`属性的标识列
- 出生日期(DOB)到年和月 — 日
- 双精度或短整数的字符串。

| CSV列 | XDM路径 | 数据格式 |
| ---------- | -------- | --------------- |
| 标题 | person.name.courtesyTitle | 复制为字符串 |
| F名称 | person.name.firstName | 复制为字符串 |
| L_NAME | person.name.lastName | 复制为字符串 |
| 性别 | person.gender | 将性别转换为对应的person.gender枚举值 |
| DOB | person.birthDayAndMonth： &quot;MM-DD&quot;<br/>person.birthDate： &quot;YYYY-MM-DD&quot;<br/>person.birthYear： YYYY | 将birthDayAndMonth转换为string<br/>将birthDate转换为string<br/>将birthYear转换为short int |
| EMAIL | personalEmail.address | 复制为字符串 |
| CRMID | identityMap.CRMID[{&quot;id&quot;:x，primary:false}] | 将字符串形式复制到identityMap中的CRMID数组，并将“主要”设置为false |
| ECID | identityMap.ECID[{&quot;id&quot;:x，主要： false}] | 将字符串形式复制到identityMap的ECID数组中的第一个条目，并将“主要”设置为false |
| LOYALTYID | identityMap.LOYALTYID[{&quot;id&quot;:x，primary:true}] | 将字符串形式复制到identityMap中的LOYALTYID数组，并将Primary设置为true |
| ECID2 | identityMap.ECID[{&quot;id&quot;:x，primary:false}] | 将字符串形式复制到identityMap的ECID数组中的第二个条目，并将Primary设置为false |
| 电话 | homePhone.number | 复制为字符串 |
| 街道 | homeAddress.street1 | 复制为字符串 |
| 城市 | homeAddress.city | 复制为字符串 |
| 状态 | homeAddress.stateProvince | 复制为字符串 |
| 国家/地区 | homeAddress.country | 复制为字符串 |
| ZIP | homeAddress.postalCode | 复制为字符串 |
| LAT | homeAddress.latitude | 转换为双精度 |
| 长型 | homeAddress.longitude | 转换为双精度 |


### 输出XDM

以下示例显示转换为XDM的CSV的前两行，如`CRM_profiles.json`中所示：

```json
{
   "person": {
      "name": {
         "courtesyTitle": "Mr",
         "firstName": "Ewart",
         "lastName": "Bennedsen"
      },
      "gender": "male",
      "birthDayAndMonth": "09-25",
      "birthDate": "2004-09-25",
      "birthYear": 2004
   },
   "identityMap": {
      "CRMID": [{
         "id": "71a16013-d805-7ece-9ac4-8f2cd66e8eaa",
         "primary": false
      }],
      "ECID": [{
         "id": "87098882279810196101440938110216748923",
         "primary": false
      },
      {
         "id": "55019962992006103186215643814973128178",
         "primary": false
      }],
      "LOYALTYID": [{
         "id": "2e33192000007456-0365c00000000000",
         "primary": true
      }]
   },
   "homePhone": {
      "number": "256-284-7231"
   },
   "personalEmail": {
      "address": "ebennedsenex@jiathis.com"
   },
   "homeAddress": {
      "street1": "72 Buhler Crossing",
      "city": "Anniston",
      "stateProvince": "Alabama",
      "country": "US",
      "postalCode": "36205",
      "_schema": {
         "latitude": 33.708276,
         "longitude": -85.7922905
      }
   }
},{
   "person": {
      "name": {
         "courtesyTitle": "Dr",
         "firstName": "Novelia",
         "lastName": "Ansteys"
      },
      "gender": "female",
      "birthDayAndMonth": "10-31",
      "birthDate": "1987-10-31",
      "birthYear": 1987
   },
   "identityMap": {
      "CRMID": [{
         "id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5",
         "primary": false
      }],
      "ECID": [{
         "id": "50829196174854544323574004005273946998",
         "primary": false
      },
      {
         "id": "65233136134594262632703695260919939885",
         "primary": false
      }],
      "LOYALTYID": [{
         "id": "2e3319208000765b-3811c00000000001",
         "primary": true
      }]
   },
   "homePhone": {
      "number": "704-181-6371"
   },
   "personalEmail": {
      "address": "nansteysdk@spotify.com"
   },
   "homeAddress": {
      "street1": "79 Northfield Hill",
      "city": "Charlotte",
      "stateProvince": "North Carolina",
      "country": "US",
      "postalCode": "28299",
      "_schema": {
         "latitude": 35.2188655,
         "longitude": -80.8108888
      }
   }
}
```

## 从Dataframe到XDM架构

数据帧（如Parquet文件）的层级必须与要上传到的XDM架构的层级匹配。

### 示例数据流

以下示例数据流的结构已映射到实现[!DNL XDM Individual Profile]类的架构，并包含与该类型架构关联的最常见字段。

```python
[
    StructField("person", StructType(
        [
            StructField("name", StructType(
                [
                    StructField("courtesyTitle", StringType()),
                    StructField("firstName", StringType()),
                    StructField("lastName", StringType())
                ]
            )),
            StructField("gender", StringType()),
            StructField("birthDayAndMonth", StringType()),
            StructField("birthDate", StringType()),
            StructField("birthYear", LongType())
        ]
    )),
    StructField("identityMap", MapType(
        StructField("CRMID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        )),
        StructField("ECID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        )),
        StructField("LOYALTYID", ArrayType(
            StructType(
                [
                    StructField("id", StringType()),
                    StructField("primary", BooleanType())
                ]
            )
        ))
    )),
    StructField("homePhone", StructType(
        [
            StructField("number", StringType())
        ]
    )),
    StructField("personalEmail", StructType(
        [
            StructField("address", StringType())
        ]
    )),
    StructField("homeAddress", StructType(
        [
            StructField("street1", StringType()),
            StructField("city", StringType()),
            StructField("stateProvince", StringType()),
            StructField("country", StringType()),
            StructField("postalCode", StringType()),
            StructField("_schema", StructType(
                [
                    StructField("latitude", DoubleType()),
                    StructField("latitude", DoubleType()),
                ]
            ))
        ]
    ))    
]
```

在构建用于Adobe Experience Platform的数据流时，要确保其层次结构与现有XDM架构完全匹配，以便字段正确映射，这一点很重要。

## 标识到标识映射

### 标识数组

```json
[
  {
    "xdm:id": "someone1@example.com",
    "xdm:namespace": {
      "xdm:code": "Email"
    }
  },
  {
    "xdm:id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5",
    "xdm:namespace": {
      "xdm:code": "CRMID"
    }
  },
  {
    "xdm:id": "2e3319208000765b-3811c00000000001",
    "xdm:namespace": {
      "xdm:code": "LOYALTYID"
    }
  }
]
```

### 映射

下表概述了标识数组的映射要求：

| 标识字段 | identityMap字段 | 数据类型 |
| -------------- | ----------------- | --------- |
| `identities[0].id` | `identityMap[Email][{"id"}]` | 复制为字符串 |
| `identities[1].id` | `identityMap[CRMID][{"id"}]` | 复制为字符串 |
| `identities[2].id` | `identityMap[LOYALTYID][{"id"}]` | 复制为字符串 |

### 输出XDM

下面是转换为XDM的身份数组：

```JSON
"identityMap": {
      "Email": [{
         "id": "someone1@example.com"
      }],
      "CRMID": [{
         "id": "2eeb6532-82e1-0d58-8955-bf97de66a6f5"
      }],
      "LOYALTYID": [{
         "id": "2e3319208000765b-3811c00000000001"
      }]
   }
```
