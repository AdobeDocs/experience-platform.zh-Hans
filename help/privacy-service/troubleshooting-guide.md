---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy Service疑难解答指南
description: 本文档提供了有关Privacy Service的常见问题解答，以及有关API中常见错误的信息。
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 1%

---

# [!DNL Privacy Service] 疑难解答指南

Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和用户界面，帮助公司管理客户数据隐私请求。 使用 [!DNL Privacy Service]，您可以提交访问和删除私人或个人客户数据的请求，以促进自动遵守组织和法律隐私法规。

本文档提供了有关 [!DNL Privacy Service]，以及有关API中常见错误的信息。

## 在API中发出隐私请求时，用户ID与用户ID之间有何区别？ {#user-ids}

要在API中创建新的隐私作业，请求的JSON有效负载必须包含 `users` 列出隐私请求所适用的每个用户的特定信息的数组。 中的每个项目 `users` 数组是表示特定用户的对象，由其标识 `key` 值。

反过来，每个用户对象(或 `key`)包含其自己的 `userIDs` 数组。 此数组列出特定ID值 **对于一个特定用户**.

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

数组包含两个对象，表示由其标识的各个用户 `key` 值(“DavidSmith”和“user12345”)。 “DavidSmith”只有一个列出的ID（其电子邮件地址），而“user12345”有两个（其电子邮件地址和ECID）。

有关提供用户身份信息的更多信息，请参阅 [隐私请求的身份数据](identity-data.md).


## 我能用一下吗 [!DNL Privacy Service] 清理意外发送到 [!DNL Platform]?

Adobe不支持使用 [!DNL Privacy Service] 用于清除意外提交到产品的数据。 [!DNL Privacy Service] 旨在帮助您履行数据主体（或消费者）访问或删除请求的义务。 不支持或允许将Privacy Service用于数据清理或维护的任何其他用途。

隐私请求对时间敏感，且已完成，且与适用的隐私法相关。 提交的请求不属于数据主体/消费者访问或删除请求，这会影响所有 [!DNL Privacy Service] 客户和 [!DNL Privacy Service] 支持适当的法律时间表。 现已设置硬性的每日上载限制，以帮助防止滥用服务。

请联系您的Adobe客户团队，以协调并提供相应的精力，以解决任何PII或数据问题。

## 如何获取有关隐私请求或工作状态的信息？

您可以使用 [!DNL Privacy Service] API或用户界面。

### 使用 API

要使用 [!DNL Privacy Service] API，向根(`GET /`)端点，使用请求路径中作业的ID。 有关更多详细信息，请参阅 [检查作业的状态](api/privacy-jobs.md#check-the-status-of-a-job) 在 [!DNL Privacy Service] API指南。

### 使用UI

所有活动作业请求都列在 **[!UICONTROL 作业请求]** 小组件 [!DNL Privacy Service] UI功能板。 每个作业请求的状态显示在 **[!UICONTROL 状态]** 列。 有关在UI中查看作业请求的更多信息，请参阅 [Privacy Service用户指南](ui/user-guide.md).

## 如何下载已完成的隐私作业的结果？

的 [!DNL Privacy Service] API和用户界面都提供了以ZIP格式下载已完成作业结果的方法。

### 使用 API

向根(`GET /`)端点 [!DNL Privacy Service] API，使用要在请求路径中下载其结果的作业的ID。 如果作业状态完成，则API将包含 `downloadURL` 属性。 此属性包含一个URL，您可以将其粘贴到浏览器的地址栏中以下载ZIP文件。

有关更多详细信息，请参阅 [按身份查找工作](api/privacy-jobs.md#check-the-status-of-a-job) 在 [!DNL Privacy Service] API指南。

### 使用UI

在 [!DNL Privacy Service] UI功能板，从 **作业请求** 小组件。 选择作业的ID以打开“作业详细信息”页面。 从此处选择 **下载** 下载ZIP文件时，您会看到此对话框。 请参阅 [Privacy Service用户指南](ui/user-guide.md) 以了解更详细的步骤。

## 常见错误消息

下表概述了 [!DNL Privacy Service]，其中包含可帮助解决其各自问题的描述。

| 错误消息 | 描述 |
| --- | --- |
| 未找到用户ID。 | 找不到请求中提供的某些用户ID，因此已跳过。 确保在请求有效负载中使用正确的命名空间和ID值。 请参阅 [提供身份数据](./identity-data.md) 以了解更详细的说明。 |
| 命名空间无效 | 为用户ID提供的身份命名空间无效。 请参阅 [标准身份命名空间](./api/appendix.md#standard-namespaces) 在 [!DNL Privacy Service] API指南附录，以获取已接受的命名空间列表。 如果您使用的是自定义命名空间，请确保您正在设置ID的 `type` 属性更改为“自定义”。 |
| 部分完成 | 作业已成功完成，但某些数据不适用于给定请求，因此被跳过。 |
| 数据不是必需的格式。 | 指定应用程序的一个或多个数据值的格式不正确。 有关更多信息，请查看作业详细信息。 |
| 尚未配置IMS组织。 | 如果贵组织未配置 [!DNL Privacy Service]. 有关更多信息，请与管理员联系。 |
| 需要访问权限和权限。 | 要使用，需要拥有访问权限和权限 [!DNL Privacy Service]. 请与管理员联系以获取访问权限。 |
| 上载和存档访问数据时出现问题。 | 发生此错误时，请重新上载访问数据，然后重试。 |
| 超出了当前文档速率限制的工作量。 | 发生此错误时，请降低提交率并重试。 |
