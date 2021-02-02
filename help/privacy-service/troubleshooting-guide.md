---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy Service疑难解答指南
topic: troubleshooting
description: 此文档提供有关Privacy Service的常见问题解答，以及有关API中常见错误的信息。
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---


# [!DNL Privacy Service] 疑难解答指南

Adobe Experience Platform[!DNL Privacy Service]提供RESTful API和用户界面，帮助公司管理客户数据隐私请求。 通过[!DNL Privacy Service]，您可以提交访问和删除私人或个人客户数据的请求，从而促进自动遵守组织和法律隐私法规。

此文档提供有关[!DNL Privacy Service]的常见问题解答，以及有关API中常见错误的信息。

## 在API中发出隐私请求时，用户ID和用户ID之间有何区别？{#user-ids}

要在API中生成新的隐私作业，请求的JSON有效负荷必须包含`users`数组，该数组列表适用于隐私请求的每个用户的特定信息。 `users`数组中的每个项目都是一个对象，它表示由其`key`值标识的特定用户。

反过来，每个用户对象（或`key`）都包含其自己的`userIDs`数组。 此数组列表该特定用户&#x200B;**的特定ID值**。

请考虑以下示例`users`阵列：

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

数组包含两个对象，表示由其`key`值（“DavidSmith”和“user12345”）标识的各个用户。 “DavidSmith”只有一个列出的ID（其电子邮件地址），而“user12345”有两个（其电子邮件地址和ECID）。

有关提供用户身份信息的详细信息，请参见[隐私请求标识数据指南](identity-data.md)。


## 我是否可以使用[!DNL Privacy Service]清除意外发送到[!DNL Platform]的数据？

Adobe不支持使用[!DNL Privacy Service]清除意外提交到产品的数据。 [!DNL Privacy Service] 旨在帮助您履行对数据主体（或消费者）访问或删除请求的义务。这些请求是时间敏感的，并且与适用的隐私法相关。 提交不属于数据主体／消费者访问或删除请求的请求会影响所有[!DNL Privacy Service]客户以及[!DNL Privacy Service]支持适当法律时间表的能力。

请联系您的客户经理(CDM)，协调并提供删除任何PII或数据问题的工作水平。

## 如何获取有关隐私请求或工作状态的信息？

您可以使用[!DNL Privacy Service] API或用户界面检索有关特定作业的详细信息。

### 使用API

要使用[!DNL Privacy Service] API检索特定作业的状态，请使用请求路径中作业的ID向根(`GET /`)端点发出请求。 有关详细信息，请参阅[!DNL Privacy Service]开发人员指南中关于[检查作业状态的部分。](api/privacy-jobs.md#check-the-status-of-a-job)

### 使用UI

所有活动作业请求都列在[!DNL Privacy Service] UI仪表板的&#x200B;**[!UICONTROL 作业请求]**&#x200B;构件中。 每个作业请求的状态显示在&#x200B;**[!UICONTROL 状态]**&#x200B;列下。 有关在UI中查看作业请求的详细信息，请参阅[Privacy Service用户指南](ui/user-guide.md)。

## 如何下载已完成的隐私工作的结果？

[!DNL Privacy Service] API和用户界面均提供以ZIP格式下载已完成作业结果的方法。

### 使用API

使用要在请求路径中下载其结果的作业的ID，向[!DNL Privacy Service] API中的根(`GET /`)端点发出请求。 如果作业状态为完成，则API将在响应主体中包含`downloadURL`属性。 此属性包含一个URL，您可以将其粘贴到浏览器的地址栏中以下载ZIP文件。

有关详细信息，请参阅[!DNL Privacy Service]开发人员指南中关于[按作业的ID](api/privacy-jobs.md#check-the-status-of-a-job)查找作业的部分。

### 使用UI

在[!DNL Privacy Service] UI仪表板中，从&#x200B;**作业请求**&#x200B;构件中找到要下载的作业。 选择作业的ID以打开“作业详细信息”页。 从此处，选择右上角的&#x200B;**下载**&#x200B;以下载ZIP文件。 有关更详细的步骤，请参见[Privacy Service用户指南](ui/user-guide.md)。

## 常见错误消息

下表概述了[!DNL Privacy Service]中的一些常见错误，并提供了帮助解决各自问题的说明。

| 错误消息 | 描述 |
| --- | --- |
| 找不到用户ID。 | 找不到请求中提供的某些用户ID，已跳过。 确保在请求有效负荷中使用正确的命名空间和ID值。 有关提供身份数据](./identity-data.md)的文档，请参见[，以获取更详细的说明。 |
| 无效命名空间 | 为用户ID提供的标识命名空间无效。 请参见[!DNL Privacy Service]开发人员指南附录中关于[标准标识命名空间](./api/appendix.md#standard-namespaces)的部分，了解已接受命名空间的列表。 如果您使用的是自定义命名空间，请确保将ID的`type`属性设置为“custom”。 |
| 部分完成 | 作业已成功完成，但某些数据不适用于给定请求，已被跳过。 |
| 数据不是所需格式。 | 指定应用程序的一个或多个数据值格式不正确。 有关详细信息，请查看作业详细信息。 |
| 尚未配置IMS组织。 | 未为[!DNL Privacy Service]配置IMS组织时，会出现此消息。 有关详细信息，请与管理员联系。 |
| 需要访问权限。 | 使用[!DNL Privacy Service]需要访问权限。 请与管理员联系以获取访问权限。 |
| 上传和存档访问数据时出现问题。 | 发生此错误时，请重新上传访问数据，然后重试。 |
| 已超出当前文档率限制的工作量。 | 出现此错误时，请降低提交率，然后重试。 |