---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 隐私服务常见问题解答
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 64cb2de507921fcb4aaade67132024a3fc0d3dee

---


# 隐私服务常见问题解答

本文档提供有关Adobe Experience Platform Privacy Service的常见问题解答。

隐私服务提供RESTful API和用户界面，帮助公司管理客户数据隐私请求。 通过隐私服务，您可以提交访问和删除私人或个人客户数据的请求，以便自动遵守组织和法律隐私法规。

## 在API中发出隐私请求时，用户ID与用户ID之间有何区别？ {#user-ids}

要在API中生成新的隐私作业，请求的JSON有效负荷必须包含一个数组，该数组列表适用于隐私请求的每个用户的特定信息。 `users` 数组中的每个项 `users` 都是一个表示特定用户的对象，该对象由其值标 `key` 识。

反过来，每个用户对象(或 `key`)都包含其自己的数 `userIDs` 组。 此数组列表该特定 **用户的特定ID值**。

Consider the following example `users` array:

```json
"users": [
  {
    "key": "DavidSmith",
    "action": ["access"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "dsmith@acme.com",
        "type": "standard"
      }
    ]
  },
  {
    "key": "user12345",
    "action": ["access", "delete"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "ajones@acme.com",
        "type": "standard"
      },
      {
        "namespace": "ECID",
        "type": "standard",
        "value":  "443636576799758681021090721276",
        "isDeletedClientSide": false
      }
    ]
  }
]
```

该数组包含两个对象，表示由其值(“DavidSmith” `key` 和“user12345”)标识的各个用户。 “DavidSmith”只有一个列出的ID（其电子邮件地址），而“user12345”有两个（其电子邮件地址和ECID）。

有关提供用户身份信息的详细信息，请参阅有关隐私 [请求的身份数据的指南](identity-data.md)。


## 我是否可以使用隐私服务来清理意外发送到平台的数据？

Adobe不支持使用隐私服务清除意外提交到产品的数据。 隐私服务旨在帮助您履行对数据主体（或消费者）访问或删除请求的义务。 这些请求是时间敏感的，并且完成时与适用隐私法相关。 提交不属于数据主体／消费者访问或删除请求的请求会影响所有隐私服务客户以及隐私服务支持相应法律时间线的能力。

请联系您的客户经理(CDM)，以协调并提供删除任何PII或数据问题所需的工作量。

## 如何获取有关我的隐私请求或工作状态的信息？

您可以使用Privacy Service API或用户界面检索有关特定作业的详细信息。

### 使用API

要使用隐私服务API检索特定作业的状态，请使用请求路径中作业的ID向根(`GET /`)端点发出请求。 有关详细信息，请参阅隐私服 [务开发人员指南中有关检查作业](api/privacy-jobs.md#check-the-status-of-a-job) 状态的部分。

### 使用UI

所有活动的作业请求都列在隐 **私服务UI仪表板的** “作业请求”构件中。 每个作业请求的状态显示在“状态” **列下** 。 有关在UI中查看作业请求的详细信息，请参阅隐私 [服务用户指南](ui/user-guide.md)。

## 如何下载已完成的隐私权作业的结果？

隐私服务API和用户界面都提供了以ZIP格式下载完成作业结果的方法。

### 使用API

使用要在请求路径中下载其结果的作业的ID，向Privacy Service API中的根(`GET /`)端点发出请求。 如果作业状态已完成，则API将在响应主体 `downloadURL` 中包含一个属性。 此属性包含一个URL，您可以将其粘贴到浏览器的地址栏中以下载ZIP文件。

有关详细信息，请参阅隐私服 [务开发人员指南中关于通过作业ID](api/privacy-jobs.md#check-the-status-of-a-job) 查找作业的部分。

### 使用UI

在隐私服务UI仪表板中，从作业请求构件中查找要下载 **的作业** 。 单击作业的ID以打开“作业详细 _信息_ ”页。 从此处，单 **击右上角** 的“下载”以下载ZIP文件。 有关更详细 [的步骤，请参阅](ui/user-guide.md) “隐私服务”用户指南。