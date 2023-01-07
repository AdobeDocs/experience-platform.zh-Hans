---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy Service发行说明
description: Adobe Experience Platform Privacy Service的最新发行说明。
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 5%

---

# [!DNL Privacy Service] 发行说明

本文档包含有关Adobe Experience Platform新增功能的信息 [!DNL Privacy Service]，以及增强功能和重要错误修复。

>[!NOTE]
>
>其他 [!DNL Experience Platform] 可找到服务 [此处](../release-notes/latest/latest.md).

## 2020 年 9 月 9 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 支持LGPD（巴西） | 如今，巴西可以在 [!DNL Lei Geral de Proteção de Dados] (LGPD)法规。 这些作业将根据法规代码进行跟踪 `lgpd_bra`. |

## 2020年4月8日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| PDPA支持 | [!DNL Privacy] 现在，可以根据泰国的个人数据保护法(PDPA)创建和跟踪请求。 在API中发出隐私请求时， `regulation` 数组接受值“pdpa_tha”。 |
| UI中的命名空间类型 | 现在，您可以在 [!DNL Privacy Service] UI。 请参阅 [用户指南](ui/user-guide.md) 以了解更多信息。 |
| 弃用旧端点 | 旧API端点(`data/privacy/gdpr`)已被弃用。 |

## 2020 年 1 月 14 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| [!DNL Privacy Service] 重新品牌化 | 以前称为“GDPR服务”的更名为 [!DNL Privacy Service] 随着该服务的发展，除了GDPR之外，还支持其他法规。 |
| 新的API端点 | 的基本路径 [!DNL Privacy Service] API已从 `/data/privacy/gdpr` to `/data/core/privacy/jobs` |
| 新增必需 `regulation` 属性 | 在 [!DNL Privacy Service] API， a `regulation` 必须在请求有效负载中提供属性，以指示要跟踪作业的法规。 接受的值为 `gdpr` 和 `ccpa`. 请参阅 [隐私作业](api/privacy-jobs.md) 在 [!DNL Privacy Service] API指南以了解更多信息。 |
| 支持Adobe Primetime身份验证 | [!DNL Privacy Service] 现在接受来自Adobe Primetime身份验证的访问/删除请求，使用 `primetimeAuthentication` 作为其产品价值。 请参阅 [Primetime身份验证文档](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) 以了解更多信息。 |

### 增强功能

* [!DNL Privacy Service] UI增强功能：
   * 为GDPR和CCPA法规分别设置作业跟踪页面。
   * 新建 *调节类型* 用于在GDPR和CCPA的跟踪数据之间切换的下拉列表。

## 2019年7月25日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 请求量度功能板 | 中的新量度功能板 [!DNL Privacy Service] UI可以查看已提交、出错和已完成的GDPR请求。 |
| 请求生成器 | 为了为同时具有技术用户和非技术用户提交GDPR请求的组织提供服务，UI中新增了“创建请求”功能。 JSON文件提交功能在 [!DNL Privacy Service] UI，适用于那些希望继续使用UI的组织。 |
| GDPR作业事件通知 | 有关GDPR作业状态的事件通知是许多工作流的一个关键元素。 虽然之前使用单个电子邮件通知来提供通知，但GDPR事件通知是利用Adobe I/O事件的消息，会将这些消息发送到配置的Webhook，以促进作业请求自动化。 [!DNL Privacy Service] UI用户可订阅Adobe I/OGDPR事件，以在产品或GDPR作业完成后接收更新。 |

## 2019年4月18日

### 增强功能

* 状态表在 [!DNL Privacy Service] UI已修改为7天。
* 更好地处理内部异常。
* 通过为具有低数据更改率的常见内部调用引入缓存，提高了性能。

### 错误修复

* 为 `GET /` 的端点 [!DNL Privacy Service] API。

## 2019 年 4 月 11 日

### 增强功能

* 更新了UI，以支持面向测试版客户的新功能
* 新量度API，可在Beta版中支持UI 2.0功能

## 2019 年 4 月 9 日

### 增强功能

* 将所有查找(GET)API调用更新为默认的30天回顾范围
* 使用限制的API的最大回顾范围为45天

## 2019年2月14日

### 增强功能

* 强制执行 `include` 字段。
* 强制执行 `include` 字段。

### 错误修复

* 修复了客户无法加载 [!DNL Privacy Service] UI。
