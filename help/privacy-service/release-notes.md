---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy Service发行说明
topic-legacy: release notes
description: Adobe Experience Platform Privacy Service的最新发行说明。
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---

# [!DNL Privacy Service] 发行说明

本文档包含有关Adobe Experience Platform [!DNL Privacy Service]的新增功能以及增强和重要错误修复的信息。

>[!NOTE]
>
>其他[!DNL Experience Platform]服务的最新发行说明位于[此处](../release-notes/latest/latest.md)。

## 2020 年 9 月 9 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 支持LGPD（巴西） | 现在，可以根据巴西的[!DNL Lei Geral de Proteção de Dados](LGPD)规定创建隐私工作。 这些作业在规章代码`lgpd_bra`下进行跟踪。 |

## 2020 年 4 月 8 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| PDPA支持 | [!DNL Privacy] 现在，可以根据泰国的《个人数据保护法》(PDPA)创建和跟踪请求。在API中发出隐私请求时，`regulation`数组接受值“pdpa_tha”。 |
| 命名空间类型 | 您现在可以在[!DNL Privacy Service] UI的Request Builder中指定不同的命名空间类型。 有关详细信息，请参阅[用户指南](ui/user-guide.md)。 |
| 旧端点弃用 | 旧API端点(`data/privacy/gdpr`)已弃用。 |

## 2020 年 1 月 14 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| [!DNL Privacy Service] 重品牌 | 之前名为“GDPR服务”的服务已更名为[!DNL Privacy Service]，因为该服务已发展为支持除GDPR外的其他法规。 |
| 新的API端点 | [!DNL Privacy Service] API的基本路径已从`/data/privacy/gdpr`更新为`/data/core/privacy/jobs` |
| 新的必需`regulation`属性 | 在[!DNL Privacy Service] API中创建新作业时，必须在请求有效负荷中提供`regulation`属性，以指示跟踪该作业所依据的规则。 接受的值为`gdpr`和`ccpa`。 有关详细信息，请参阅[!DNL Privacy Service]开发人员指南中关于[隐私作业](api/privacy-jobs.md)的文档。 |
| 支持Adobe Primetime身份验证 | [!DNL Privacy Service] 现在接受来自Adobe Primetime身份验证的访问/删除请求，并 `primetimeAuthentication` 将其用作产品值。有关详细信息，请参阅[Primetime身份验证文档](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)。 |

### 增强功能

* [!DNL Privacy Service] UI增强：
   * 为GDPR和CCPA规定分别设置工作跟踪页面。
   * 新的&#x200B;*规章类型*&#x200B;下拉列表用于在GDPR和CCPA的跟踪数据之间切换。

## 2019 年 7 月 25 日

### 新增功能

| 功能 | 描述 |
| --- | --- |
| 请求量度仪表板 | [!DNL Privacy Service] UI中的新量度仪表板可以查看已提交、已出错和已完成的GDPR请求。 |
| 请求生成器 | 为了为技术用户和非技术用户提交GDPR请求的组织提供服务，UI中已添加了“创建请求”功能。 对于希望继续使用JSON文件的组织，[!DNL Privacy Service] UI中仍提供JSON文件提交功能。 |
| GDPR工作事件通知 | 有关GDPR作业状态的事件通知对许多工作流来说都是关键元素。 虽然之前通知是使用单个电子邮件通知发送的，但GDPR事件通知是利用Adobe I/O事件的消息，这些通知会发送到已配置的Webhook，以便于作业请求自动化。 [!DNL Privacy Service] UI用户可订阅Adobe I/O GDPR事件，以在产品或GDPR作业完成后接收更新。 |

## 2019 年 18 月 4 日

### 增强功能

* [!DNL Privacy Service] UI中状态表的默认范围已修改为7天。
* 更好的内部异常处理。
* 通过为低数据更改率的常见内部调用引入缓存，提高了性能。

### 错误修复

* 为[!DNL Privacy Service] API中的`GET /`端点的筛选查询添加了缺少日志记录信息。

## 2019 年 4 月 11 日

### 增强功能

* 更新的UI可支持面向测试版客户的新功能
* 支持测试版UI 2.0功能的新指标API

## 2019 年 4 月 9 日

### 增强功能

* 将所有查找(GET)API调用更新为默认的30天回顾范围
* 限制API使用，最大回顾范围为45天

## 2019 年 2 月 14 日

### 增强功能

* 在每个POST提交中强制执行`include`字段。
* 上传JSON时强制执行`include`字段。

### 错误修复

* 修复了客户无法加载[!DNL Privacy Service] UI的问题。
