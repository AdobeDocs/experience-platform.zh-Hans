---
keywords: Experience Platform；主页；热门主题；GDPR；GDPR；CCPA；CCPA；PDPA；PDPA；LGPD；lgpd；概述；概述；法规；法规；法规；法规；隐私；隐私；
solution: Experience Platform
title: 隐私法规概述
description: 本文档概述了Adobe Experience Cloud支持的各种隐私法规。
exl-id: 2ca946cf-94f8-4fd8-bb1a-7f06a5ab1256
source-git-commit: b960e67789acaeb27a0a39db933a2bbb7d84f4d5
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 0%

---

# 隐私法规概述

>[!IMPORTANT]
>
>为了支持数量不断增长的美国州隐私法，Privacy Service正在更改其`regulation_type`值。 使用包含从`ucpa_ut_usa`2025年6月12日开始的状态缩写（例如&#x200B;**）的新值**。 旧值（例如`ucpa_usa`）在&#x200B;**2025年7月28日**&#x200B;之后停止工作。
>
>在此截止日期之前更新您的集成，以避免请求失败。

本文档概述了Adobe Experience Cloud支持的各种隐私法规。

通过使用[Adobe Experience Platform Privacy Service](../home.md)，Experience Cloud根据以下法规支持访问和删除请求：

| 法规 | `regulation_type` | 描述 |
|-----------|-------------------|-------------|
| APA （澳大利亚） | `apa_aus` | [[!DNL Australia Privacy Act (Privacy Act)]](https://www.oaic.gov.au/privacy/the-privacy-act)提升和保护个人隐私，并管理澳大利亚政府机构和组织处理个人信息的方式。 《隐私法》包含适用于私营部门组织的原则。 例如，个人有权了解为什么收集个人信息以及如何使用信息，有权访问、擦除其数据和更正个人信息。 |
| CCPA （加利福利亚州） | `ccpa` | [[!DNL California Consumer Privacy Act (CCPA)]](https://oag.ca.gov/privacy/ccpa)增强了美国加利福尼亚州居民的隐私权和消费者保护。 CCPA为加利福尼亚州居民提供了新的数据隐私权。 其中包括访问和删除个人数据的权利，知晓其个人数据是否被出售或披露（以及披露给谁）的权利，以及选择不将其数据出售给第三方的权利。 |
| CPA （科罗拉多州） | `cpa_co_usa` | [[!DNL Colorado Privacy Act]](https://coag.gov/resources/colorado-privacy-act/) (CPA)为科罗拉多州消费者提供了额外的insight，以便了解个人数据控制者收集、共享和销售哪些数据以及如何使用该数据。 当科罗拉多州居民在个人或家庭环境中采取行动时，CPA会保护他们的个人数据。 这些规则详细说明了一个或多个通用选择退出机制的技术规范。 这些机制清楚地传达了消费者出于定向广告或销售个人数据目的选择退出个人数据处理的肯定、自由给予且明确的选择。 |
| CPRA （加利福利亚州） | `cpra_ca_usa` | [[!DNL California Consumer Privacy Rights Act (CPRA)]](https://cppa.ca.gov/regulations/consumer_privacy_act.html)扩展并修正了《加州消费者隐私法案》(CCPA)的部分内容。 CPRA通过增加消费者权利并扩展敏感个人信息更广泛的定义所涵盖的数据类型，为加州消费者数据隐私建立了新的基准。 此外，CPRA还成立了加州隐私保护局，这是一个致力于实施和实施数据隐私规则的新机构。 |
| CTDPA （康涅狄格州） | `ctdpa_ct_usa` | [[!DNL Connecticut Data Privacy Act]](https://portal.ct.gov/AG/Sections/Privacy/The-Connecticut-Data-Privacy-Act)是适用于康涅狄格州居民的综合性消费者隐私法，授予他们对其个人数据的某些权利。 它还规定了数据控制者处理其个人数据的责任和隐私保护标准。 CTDPA保护康涅狄格州居民的个人或家庭。 CTDPA授予他们以下权利：访问、更正、删除、获取副本或选择退出销售；处理他们的个人数据；或分析他们的个人数据。 |
| DPDPA （特拉华州） | `dpdpa_de_usa` | [[!DNL Delaware Personal Data Privacy Act]](https://legis.delaware.gov/json/BillDetail/GenerateHtmlDocument?legislationId=140388&legislationTypeId=1&docTypeId=2&legislationName=HB154) (DPDPA)授予特拉华州居民访问、更正、删除的权利，以及选择退出个人数据销售和定向广告的权利。 它适用于为至少3.5万名消费者处理数据，或者从影响1万多名消费者的数据销售中获得20%以上收入的企业。 该法规定消费者数据保护做法，对消费者请求做出及时回应，规定侵权行为需有60天的治疗期，并由司法部强制执行。 |
| FDBR （佛罗里达州） | `fdbr_fl_usa` | [[!DNL Florida Digital Bill of Rights]](https://flsenate.gov/Session/Bill/2023/262/BillText/er/HTML) (FDBR)为佛罗里达州居民提供全面的数据隐私权。 这项法律确保个人有权访问、更正、删除和获取其个人数据的副本。 该法规还禁止网络平台进行某些行为，例如未经消费者同意的监控，并要求数据行为透明，包括明确的隐私声明和选择退出针对性广告的个人数据出售或处理功能。 联邦难民局授权佛罗里达州法律事务部执行这些权利，并对违反这些权利的行为实施民事惩罚。 根据该法，数据控制者有义务在收到数据主体请求后45天内作出回应。 |
| GDPR（欧盟） | `gdpr` | [[!DNL General Data Protection Regulation (GDPR)]](https://gdpr-info.eu)为欧洲经济区(EEA)成员引入了几项新的数据隐私权，包括访问权和被遗忘权。 这些权限意味着在EEA中居住且企业已收集其个人数据的任何人均可随时请求访问或删除其数据。<br><br>英国（英国退欧后）有自己的监管版本，即UK-GDPR，该版本为其公民提供了与EEA版本相同的权利。 |
| HIPAA（美利坚合众国） | `hipaa_usa` | [[!DNL Health Insurance Portability and Accountability Act (HIPAA)]](https://www.hhs.gov/hipaa/index.html)是美国联邦法律，旨在提高医疗保健效率、改善健康保险的可移植性，并保护患者和健康计划成员的隐私。 根据HIPAA，个人有权访问和修改其信息，并获得其医疗记录或健康信息的副本。 覆盖的实体和覆盖的实体的业务联系人必须遵守HIPAA规定。 |
| ICDPA （艾奥瓦州） | `icdpa_ia_usa` | [[!DNL Iowa Consumer Data Protection Act]](https://www.legis.iowa.gov/legislation/BillBook?ga=90&ba=SF%20262)为Iowa居民提供访问、删除和选择退出出售其个人数据的权利。 适用于处理10万艾奥瓦州居民以上数据或出售个人数据创造超过50%收入的企业。 ICDPA强调消费者对个人信息的控制，但排除某些组织，包括非营利组织和教育机构。 该法还规定，企业在90天之内纠正侵权行为，然后才予以处罚。 |
| LGPD （巴西） | `lgpd_bra` | [[!DNL Lei Geral de Proteção de Dados (LGPD)]](https://gdpr.eu/gdpr-vs-lgpd/)旨在规范巴西境内所有个人或自然人的个人数据处理方式。 LGPD赋予巴西公民访问和删除其个人数据的权利，知晓其个人数据是否被出售或披露（包括披露给谁）的权利，以及选择不将其数据出售给第三方的权利。 |
| 麦克德巴（明尼苏达州） | `mcdpa_mn_usa` | [[!DNL Minnesota Consumer Data Privacy Act (MCDPA)]](https://www.house.mn.gov/comm/docs/C6hTV3TEt0W2vuhEMtczrQ.pdf)为明尼苏达州居民提供访问、更正、删除和获取其个人数据副本的权利。 它还赋予了选择退出个人数据销售、定向广告和以个人特征描述来推进产生法律或类似重大影响的决策的权利。 该法要求数据控制者有义务提供明确的隐私声明、开展数据保护评估并维护合理的数据安全做法。 执法权授予明尼苏达州总检察长。 |
| 麦克德帕（蒙大拿州） | `mcdpa_mt_usa` | [[!DNL Montana Consumer Data Privacy Act]](https://legiscan.com/MT/text/SB384/id/2791095)使居民有权了解企业收集、共享和出售哪些个人数据及其用途。 它还赋予消费者更正、删除或获取所收集数据副本的能力。 该法适用于处理50,000多个蒙大拿州消费者数据的企业。 该法强调保护敏感的个人数据，包括生物统计和遗传信息。 |
| 姆姆达（华盛顿州） | `mhmda_wa_usa` | [[!DNL Washington My Health My Data Act]](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&full=true)增强了消费者对其健康数据的隐私权。 它规定健康数据的披露、消费者同意和删除权利，并禁止未经授权销售健康数据。 此外，该法还规定，在保健设施周围使用地理围栏是非法的。 |
| 莫德帕（马里兰州） | `modpa_md_usa` | [[!DNL Maryland Online Data Privacy Act]](https://mgaleg.maryland.gov/2024RS/bills/sb/sb0541e.pdf)授予马里兰州居民权限，包括访问、更正、删除和数据可移植性。 居民可以选择退出定向广告、个人数据销售和资料分析。 控制器必须提供隐私声明并为高风险处理执行数据保护评估。 MODPA禁止在精神或生殖健康设施周围设置地理围栏，因而引人注目。 该法适用于那些处理来自3.5万多名消费者数据的实体，或那些处理来自1万多名消费者数据且其中超过20%的收入来自销售这些数据的实体。 这项法律由马里兰州司法部长执行。 |
| NDPA （内布拉斯加州） | `ndpa_ne_usa` | [[!DNL Nebraska Data Protection Act]](https://nebraskalegislature.gov/FloorDocs/108/PDF/Slip/LB1074.pdf)为内布拉斯加州人提供对其个人数据的权限，例如访问、更正、删除和选择退出其销售。 该法适用于满足数据处理特定门槛和个人信息销售收入的企业。 它还要求企业实施合理的数据安全做法，并规定30天的强制治疗期，以便在受到处罚之前解决法规遵从性问题。 |
| 新西兰[!DNL Privacy Act] | `nzpa_nzl` | [新西兰 [!DNL Privacy Act]](https://www.privacy.org.nz/privacy-act-2020/privacy-principles/)控制各机构如何收集、使用、披露、存储和访问新西兰公民和组织的个人信息。 2020年，最新版本的法案对这些隐私法进行了重大更新。 最新情况包括新犯罪、增加罚款、强制通知数据泄露，以及增加隐私专员的权力。 |
| NHDPA （新罕布什尔州） | `nhpa_nh_usa` | [[!DNL New Hampshire Privacy Act]](https://www.doj.nh.gov/sites/g/files/ehbemt721/files/inline-documents/sonh/data-privacy-faqs-revised_0.pdf)通过建立与数据访问、删除和可移植性相关的消费者权利来保护新罕布什尔州居民的个人信息。 它要求组织披露其数据收集和共享做法，并允许消费者选择退出数据销售。 该法适用于达到某些数据处理阈值的企业。 |
| NJDPA （新泽西州） | `njdpa_nj_usa` | [[!DNL New Jersey Data Protection Act]](https://pub.njleg.state.nj.us/Bills/2022/S0500/332_R6.PDF)通过提供访问、更正和删除其信息的权限，授予新泽西居民对其个人数据的控制权。 它包括用于数据销售和定向广告的选择退出机制。 该法涵盖处理大量消费者数据的企业，并要求数据使用透明。 |
| OCPA （俄勒冈州） | `ocpa_or_usa` | [[!DNL Oregon Consumer Privacy Act]](https://olis.oregonlegislature.gov/liz/2023R1/Downloads/PublicTestimonyDocument/59856#:~:text=The%20Act%20requires%20controllers%20to,data%3B%20and%20%E2%80%A2%20Contact%20information.) (OCPA)为俄勒冈州居民提供了对其个人数据的基本权利，并要求处理此类数据的企业承担相关义务。 消费者有权了解、更正、删除和获取其数据的副本，以及选择退出针对性广告或销售的数据处理。 该法要求加强对敏感数据的保护，准许超出特定目的进行数据处理，并规定数据控制者发出全面的隐私声明。 |
| PDPA （泰国） | `pdpa_tha` | 引入[[!DNL Personal Data Protection Act (PDPA)]](https://www.pdpc.gov.sg/Overview-of-PDPA/The-Legislation/Personal-Data-Protection-Act)是为了保护泰国数据所有者免遭非法收集、使用或泄露其个人数据的行为。 受欧盟GDPR的启发，该法规授予泰国公民请求访问或删除其存储的个人数据的权利。 |
| PIPA （韩国） | `pipa_kor` | [[!DNL Personal Information Protection Act (PIPA)]](https://elaw.klri.re.kr/eng_service/lawView.do?hseq=53044&lang=ENG)管理韩国居民个人数据的处理和保护。 PIPA授予居民知情权、访问权、获取副本权，以及请求更正、删除或暂停处理的权利。 个人信息控制者必须明确收集目的，在必要的最低限度内合法处理数据，并确保数据准确性。 PIPA还设立了个人信息保护委员会，以调查和执行个人数据保护条例。 |
| ql25 （魁北克） | `ql25_qc_can` | [[!DNL Quebec Law 25]](https://www.canlii.org/en/qc/laws/astat/sq-2021-c-25/latest/sq-2021-c-25.html) (QL25)增强了魁北克居民的隐私权，以符合全球标准。 该法明确规定居民必须明确同意、数据最小化和有权访问、更正、删除和传输其个人数据。 组织还必须指定一名隐私官员，进行隐私影响评估并通知泄露。 法律强制规定的遵守期限以及对违规行为的大量处罚。 |
| TDPSA （得克萨斯州） | `tdpsa_tx_usa` | [[!DNL Texas Data Privacy and Security Act]](https://capitol.texas.gov/BillLookup/Text.aspx?LegSess=88R&Bill=HB4) (TDPSA)管理得克萨斯州消费者个人数据的收集、使用、处理和处理。 自2024年7月1日起，它授予居民访问、更正、删除和获取其数据副本的权利，以及选择退出定向广告和数据销售的权利。 该法适用于在得克萨斯州开展业务或生产得克萨斯居民消费的产品/服务的实体，不包括小型企业和某些其他组织。 违反规定者可能受到民事处罚。 |
| TIPA （田纳西州） | `tipa_tn_usa` | [[!DNL Tennessee Information Protection Act (TIPA)]](https://www.capitol.tn.gov/Bills/113/Bill/HB1181.pdf)授予田纳西州居民访问、更正、删除和获取其个人数据副本的权利。 该法还规定了选择退出出售个人信息、定向广告和某些类型个人资料的权利。 该法律适用于满足数据处理和收入特定阈值的企业，它要求明确的隐私声明、数据最小化以及合理的安全实践。 执法权授予田纳西州司法部长。 |
| UCPA （犹他州） | `ucpa_ut_usa` | [[!DNL Utah Consumer Privacy Act]](https://le.utah.gov/~2022/bills/static/SB0227.html)为消费者创建了解企业收集哪些个人数据、企业如何使用其个人数据以及企业是否出售其个人数据的权利。 消费者可以要求企业删除或停止出售其个人数据。 |
| VCDPA （弗吉尼亚州） | `vcdpa_va_usa` | [[!DNL Virginia Consumer Data Protection Act (VCDPA)]](https://lis.virginia.gov/cgi-bin/legp604.exe?212+sum+HB2307)为弗吉尼亚州居民（“消费者”）提供了新的数据隐私权，包括访问、删除和更正个人数据的权利。 消费者还有权选择退出个人数据销售、选择退出基于个人数据的分析和处理个人广告。 |

{style="table-layout:auto"}

请参阅[隐私作业端点指南](../api/privacy-jobs.md)，了解如何使用Privacy Service API提交、跟踪和管理访问和删除请求。 该指南包含帮助您入门的示例和格式详细信息。

## 后续步骤

有关支持的法规的更多信息，请参阅以下文档：

* [隐私法规常见问题解答](./faq.md)
* [隐私法规术语](./terminology.md)

要了解如何支持客户访问和删除存储在Experience Cloud应用程序上的数据的请求，请参阅[Privacy Service和Experience Cloud应用程序指南](../experience-cloud-apps.md)。
