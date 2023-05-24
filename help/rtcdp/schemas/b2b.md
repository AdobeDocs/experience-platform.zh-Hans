---
title: Real-time Customer Data Platform B2B版本中的結構描述
description: 概述Experience Data Model (XDM)結構描述在Adobe Real-time Customer Data Platform B2B版本中的角色。
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Real-time Customer Data Platform B2B版本中的結構描述

Adobe Real-time Customer Data Platform B2B版本提供數種標準 [Experience Data Model (XDM)類別](../../xdm/schema/composition.md#class) 擷取基本B2B資料實體的詳細資訊，例如帳戶、商機、促銷活動等。 此外，Real-Time CDP B2B Edition可讓您定義這些結構描述之間的多對一關係，好讓他們能參與進階細分使用案例。

>[!IMPORTANT]
>
>您必須擁有Real-Time CDP B2B Edition的存取權，B2B結構描述才能參與 [即時客戶個人檔案](../../profile/home.md).

Real-Time CDP B2B Edition提供下列標準類別：

* [XDM商業帳戶](../../xdm/classes/b2b/business-account.md)
* [XDM商業帳戶個人關係](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM商業活動](../../xdm/classes/b2b/business-campaign.md)
* [XDM商業活動會員](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM商業機會](../../xdm/classes/b2b/business-opportunity.md)
* [XDM商業機會個人關係](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM業務行銷清單](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM業務行銷清單成員](../../xdm/classes/b2b/business-marketing-list-members.md)

若要瞭解結構描述如何適合您的B2B工作流程，請參閱 [端到端教學課程](../b2b-tutorial.md).

如需如何在兩個結構描述之間建立多對一關係的步驟，請參閱的教學課程： [定義B2B結構描述關係](../../xdm/tutorials/relationship-b2b.md).

如果您使用B2B來源連線，則可以使用工具來自動產生所需的結構描述以及它們之間的關係。 請參閱指南： [B2B名稱空間](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) 如需詳細資訊，請參閱來原始檔。
