---
keywords: Experience Platform;home;popular topics;consent;Consent
solution: Experience Platform
title: CCPA常见问题解答
topic: troubleshooting
description: 本文档回答了有关加利福尼亚州消费者保护法(CCPA)及其在Adobe Experience Cloud实施的常见问题。
translation-type: tm+mt
source-git-commit: 172710c62b6f60de74e05364edb1191fbba0ff64
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 0%

---


# CCPA常见问题解答

本文档回答了有关该(CCPA)及其在 [!DNL California Consumer Protection Act] Adobe Experience Cloud实施的常见问题。

## 什么是CCPA?

加 [!DNL California Consumer Privacy Act] 州新的隐私法(CCPA)为居民提供个人信息的新权利，并对在加利福尼亚开展业务的特定实体承担数据保护责任。

>[!NOTE]
>
>尽管CCPA在2020年1月正式生效，但法律制定者仍在对CCPA进行微调。 此外，加州监管机构尚未起草的法规也将提供重要的实施和其他指导细节。

尽管CCPA确实共享了根据欧洲合并的一般数据保护规定(GDPR)提供的一些概念，例如个人访问和删除个人信息的权利，但CCPA与GDPR有若干主要不同之处。 例如，CCPA为消费者提供特定数据共享活动的选择退出权，这些数据共享客户有资格向第三方“销售”个人信息，而不是要求事先同意。

## CCPA下的个人信息定义是什么？

个人信息是“能够识别、关联、描述、能够与消费者或家庭相关，或能够与消费者或家庭直接或间接合理关联的信息。”

## Adobe Experience Cloud使用的哪些类型的个人信息或标识符符合这些新要求？

以下标识符常用于应 [!DNL Experience Cloud] 用程序，并可能受CCPA要求的约束：

- 名称
- 邮政地址
- 唯一个人标识符
- 联机标识符
- IP地址
- 电子邮件地址
- 帐户名称

个人信息还可以包括因特网或其他电子网络活动信息。 这包括但不限于：

- 浏览历史记录
- 搜索历史记录
- 关于消费者与网站、应用程序或广告交互的信息

尽管CCPA涵盖大量个人信息，但Adobe的标准合同条款仍规定一般禁止在应用程序中导入和使用敏感个人信息(如SSN、驾驶执照信息、财务帐户信息和生物统计数 [!DNL Experience Cloud] 据)。

## CCPA公司不同的角色和职责是如何适用的 [!DNL Experience Cloud]?

如CCPA所定义，以下角色适用于Adobe及其客户：

- Adobe客户（请求从加利福尼亚州居民处收集和使用个人信息的一方）将被视为 **业务**。
- Adobe在提供服务方面将被视为一个 **服务提供商**。

鉴于这种关系和Adobe的合同语言，向Adobe披露信息可能不会被视为“出售”，企业需要为此提供通知并优惠选择退出。

但是，Adobe服务可用于支持某些数据共享和传输至第三方。 这些第三方转让可被视为“出售”，并依法要求披露和选择退出。  客户应与其法律顾问合作，评估特定使用案例，以评估适用要求。

## 企业为访问或删除个人信息而响应消费者请求的天数？

假定该企业已收集个人信息，并且可以验证或验证特定加利福尼亚消费者的身份，CCPA允许在45天内完成消费者请求（有些例外）。

## Adobe在CCPA之下扮演什么角色？

作为服务提供商,Adobe代表业务收集和处理个人信息，并受合同约束，仅将这些信息用于协议中规定的特定用途。

鉴于这种关系和Adobe的合同语言，对Adobe的披露属于法律对服务提供商的规定，很可能不会被视为“出售”，企业需要为其提供通知，并优惠选择退出。

Adobe服务可用于支持特定数据共享和传输至第三方。 这些第三方转让可被视为“出售”，并依法要求披露和选择退出。  客户应与其法律顾问合作，评估特定使用案例，以评估适用要求。

## 如果我维护的是某些类型的数据符合要求，如何支持CCPA下的消费者隐私要求？

在您采取必要步骤验证CA用户身份后，Adobe Experience Platform [!DNL Privacy Service] 允许您向兼容应用程序提交消费者隐私 [!DNL Experience Cloud] 请求。 有关更多 [信息](../home.md) ，请参阅Privacy Service概述。 有关您的特定应用程序如 [!DNL Experience Cloud] 何满足隐私请求的信息，请参阅有关Privacy Service和Experience Cloud应 [用程序的指南](../experience-cloud-apps.md)。

>[!NOTE]
>
>加州监管机构仍将提供进一步指导，说明哪些类型的数据符合消费者隐私要求。

## Adobe是否会优惠其他有助于满足CCPA要求的工具？

Adobe Experience Cloud应用程序提供数据管理和管理功能，这些功能有助于公司的隐私需求。 这些工具包括数据使用标签、基于角色的访问控制、IP模糊化和散列功能。

Adobe已获得其隐私和安全实践的各种认证，如ISO 27001认证和TrustArc GDPR验证。