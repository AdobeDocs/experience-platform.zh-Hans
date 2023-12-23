---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy Service疑难解答指南
description: 本文档提供有关Privacy Service的常见问题解答以及API中常见错误的信息。
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 1%

---

# [!DNL Privacy Service] 疑难解答指南

Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和用户界面，帮助公司管理客户数据隐私请求。 替换为 [!DNL Privacy Service]，您可以提交访问和删除私人或个人客户数据的请求，从而促进自动遵守组织和法律隐私法规。

本文档提供有关以下内容的常见问题解答： [!DNL Privacy Service]，以及有关API中经常遇到的错误的信息。

## 在API中提出隐私请求时，用户和用户ID有何区别？ {#user-ids}

要在API中新建隐私作业，请求的JSON有效负载必须包含 `users` 数组，其中列出了隐私请求应用于的每个用户的特定信息。 中的每项 `users` 数组是表示特定用户的对象，由其 `key` 值。

反过来，每个用户对象(或 `key`)包含它自己的 `userIDs` 数组。 此数组列出了特定的ID值 **针对该特定用户**.

请考虑以下示例 `users` 数组：

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

该数组包含两个对象，分别表示由他们标识的单个用户 `key` 值(“DavidSmith”和“user12345”)。 “DavidSmith”只有一个列出的ID（电子邮件地址），而“user12345”有两个列出的ID（电子邮件地址和ECID）。

有关提供用户标识信息的更多信息，请参阅以下指南中的 [隐私请求的身份数据](identity-data.md).


## 我可以使用 [!DNL Privacy Service] 以清理意外发送到的数据 [!DNL Platform]？

Adobe不支持使用 [!DNL Privacy Service] 用于清除意外提交到产品的数据。 [!DNL Privacy Service] 旨在帮助您履行对数据主体（或消费者）访问或删除请求的义务。 不支持或允许将Privacy Service用于数据清理或维护。

隐私请求对时间敏感，并且是根据适用的隐私法完成的。 提交不是数据主体/消费者访问或删除请求的请求会影响所有 [!DNL Privacy Service] 客户和 [!DNL Privacy Service] 支持适当的法律时限。 现已设定每日硬性上传限制，以防止滥用服务。

请联系您的Adobe客户团队以协调任何PII或数据问题并提供相应的解决措施。

## 如何获取有关隐私请求或作业状态的信息？

您可以使用检索有关特定作业的详细信息 [!DNL Privacy Service] API或用户界面。

### 使用 API

要使用检索特定作业的状态，请执行以下操作 [!DNL Privacy Service] API，向根发出请求(`GET /`)端点，使用请求路径中作业的ID。 有关更多详细信息，请参阅 [检查作业的状态](api/privacy-jobs.md#check-the-status-of-a-job) 在 [!DNL Privacy Service] API指南。

### 使用UI

所有活动作业请求都列在 **[!UICONTROL 作业请求]** 上的构件 [!DNL Privacy Service] UI仪表板。 每个作业请求的状态显示在 **[!UICONTROL 状态]** 列。 有关在UI中查看作业请求的更多信息，请参阅 [Privacy Service用户指南](ui/user-guide.md).

## 如何下载已完成的隐私作业的结果？

此 [!DNL Privacy Service] API和用户界面都提供了以ZIP格式下载已完成作业结果的方法。

### 使用 API

向根用户发出请求(`GET /`)中的端点 [!DNL Privacy Service] API，使用要在请求路径中下载其结果的作业的ID。 如果作业的状态为“完成”，则API将包含 `downloadURL` 属性。 此属性包含一个URL，您可以将其粘贴到浏览器的地址栏来下载ZIP文件。

有关更多详细信息，请参阅 [按作业ID查找作业](api/privacy-jobs.md#check-the-status-of-a-job) 在 [!DNL Privacy Service] API指南。

### 使用UI

在 [!DNL Privacy Service] 在UI仪表板中，找到要下载的作业 **作业请求** 构件。 选择作业的ID以打开“作业详细信息”页。 从此处选择 **下载** 下载ZIP文件。 请参阅 [Privacy Service用户指南](ui/user-guide.md) 以了解更多详细步骤。

## 常见错误消息 {#common-error-messages}

下表概述了中出现的一些常见错误 [!DNL Privacy Service]，其中包含帮助解决其各自问题的描述。

| 错误消息 | 描述 |
| --- | --- |
| 未找到用户ID。 | 无法找到请求中提供的某些用户ID，已跳过这些ID。 确保在请求有效负载中使用正确的命名空间和ID值。 查看文档 [提供身份数据](./identity-data.md) 以取得更详细的解释。 |
| 命名空间无效 | 为用户ID提供的身份命名空间无效。 请参阅以下部分 [标准身份命名空间](./api/appendix.md#standard-namespaces) 在 [!DNL Privacy Service] API指南附录，以获取接受的命名空间列表。 如果您使用的是自定义命名空间，请确保设置ID的 `type` 属性转换为“自定义”。 |
| 部分完成 | 作业已成功完成，但某些数据不适用于给定的请求，已跳过。 |
| 数据的格式不符合要求。 | 指定应用程序的一个或多个数据值的格式不正确。 有关更多信息，请查看作业详细信息。 |
| 尚未配置IMS组织。 | 当您的组织尚未配置以下项时，会发生此消息： [!DNL Privacy Service]. 有关详细信息，请与管理员联系。 |
| 需要访问和权限。 | 必须具有访问权限才能使用 [!DNL Privacy Service]. 请与管理员联系以获取访问权限。 |
| 上载和归档访问数据时出现问题。 | 发生此错误时，请重新上传访问数据并重试。 |
| 工作负载超出了当前的文档速率限制。 | 发生此错误时，请降低提交率并重试。 |
| 请求过多<br>（HTTP 429错误） | 如果您的提交模式超过了受监控的允许数据主体作业限制，您将收到HTTP 429错误，以响应来自组织的持续流量。 Privacy Service用于处理数据主体隐私请求。 不用于数据清理。 如果您收到HTTP 429错误，将实施限制和请求限制以保护Adobe免受可能使合法合规工作面临风险的滥用。<br>以下提供了最小化数据的替代方法 [设置数据集到期计划](../hygiene/ui/dataset-expiration.md) 并使用 [记录删除功能](../hygiene/ui/record-delete.md). 有关如何应用这些功能的更多信息，请参阅各自的文档。 |
