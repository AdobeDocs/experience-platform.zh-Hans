---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy Service发行说明
description: Adobe Experience Platform Privacy Service的最新发行说明。
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 5%

---

# [!DNL Privacy Service] 发行说明

本文档包含有关Adobe Experience Platform [!DNL Privacy Service]的新增功能、增强功能和重大错误修复的信息。

>[!NOTE]
>
>其他[!DNL Experience Platform]服务的最新发行说明可在[此处](../release-notes/latest/latest.md)找到。

## 2020 年 9 月 9 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 支持LGPD（巴西） | 现在可以根据巴西的[!DNL Lei Geral de Proteção de Dados] (LGPD)法规创建隐私作业。 根据法规代码`lgpd_bra`跟踪这些作业。 |

## 2020年4月8日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| PDPA支持 | 在泰国，现在可以根据《个人数据保护法》(PDPA)创建和跟踪[!DNL Privacy]请求。 在API中发出隐私请求时，`regulation`数组接受值“pdpa_tha”。 |
| UI中的命名空间类型 | 您现在可以在[!DNL Privacy Service] UI的请求生成器中指定不同的命名空间类型。 有关详细信息，请参阅[用户指南](ui/user-guide.md)。 |
| 弃用旧端点 | 已弃用旧的API终结点(`data/privacy/gdpr`)。 |

## 2020年1月14日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| [!DNL Privacy Service]品牌再造 | 以前称为“GDPR服务”的服务已更名为[!DNL Privacy Service]，因为该服务已扩展以支持除GDPR之外的其他法规。 |
| 新API端点 | [!DNL Privacy Service] API的基本路径已从`/data/privacy/gdpr`更新为`/data/core/privacy/jobs` |
| 新必需的`regulation`属性 | 在[!DNL Privacy Service] API中创建新作业时，必须在请求有效载荷中提供`regulation`属性，以指示要跟踪该作业的法规。 接受的值为`gdpr`和`ccpa`。 有关详细信息，请参阅[!DNL Privacy Service] API指南中有关[隐私作业](api/privacy-jobs.md)的文档。 |
| 支持Adobe Primetime身份验证 | [!DNL Privacy Service]现在接受来自Adobe Primetime身份验证的访问/删除请求，使用`primetimeAuthentication`作为其产品值。 有关详细信息，请参阅[Primetime身份验证文档](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)。 |

### 增强功能

* [!DNL Privacy Service]用户界面增强：
   * 根据GDPR和CCPA法规，单独设置作业跟踪页面。
   * 新增了&#x200B;*法规类型*&#x200B;下拉列表，以便在GDPR和CCPA的跟踪数据之间切换。

## 2019年7月25日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 请求量度仪表板 | [!DNL Privacy Service] UI中的新量度仪表板提供已提交、有错误和已完成的GDPR请求的可见性。 |
| 请求生成器 | 要为具有提交GDPR请求的技术和非技术用户的组织提供服务，UI中已添加了“创建请求”功能。 对于希望继续使用JSON文件的组织，仍可在[!DNL Privacy Service] UI中使用它的JSON文件提交功能。 |
| GDPR作业事件通知 | 关于GDPR作业状态的事件通知是许多工作流程的关键元素。 虽然之前使用单独的电子邮件通知提供通知，但GDPR事件通知是利用Adobe I/O事件的消息，这些通知将发送到配置的webhook以促进作业请求自动化。 [!DNL Privacy Service]个UI用户可以订阅Adobe I/OGDPR事件，以便在完成产品或GDPR作业后接收更新。 |

## 2019年4月18

### 增强功能

* [!DNL Privacy Service] UI中状态表的默认范围已修改为7天跨度。
* 更好的内部异常处理。
* 通过为具有低数据更改率的常见内部调用引入缓存，改进了性能。

### 错误修复

* 为[!DNL Privacy Service] API中的`GET /`终结点添加了已筛选查询的缺失日志记录信息。

## 2019年4月11

### 增强功能

* 更新了UI，以支持测试版客户的新功能
* 新量度API可在Beta版中支持UI 2.0功能

## 2019 年 4 月 9 日

### 增强功能

* 将所有查找(GET) API调用更新为默认的30天回顾范围
* 限制API的使用，使其最大回溯范围为45天

## 2019年2月14日

### 增强功能

* 在每次提交POST时强制`include`字段。
* 上传JSON时强制`include`字段。

### 错误修复

* 修复了客户无法加载[!DNL Privacy Service] UI的问题。
