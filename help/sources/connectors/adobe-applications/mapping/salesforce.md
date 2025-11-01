---
title: Salesforce映射字段
description: 下表包含Salesforce源字段及其对应的XDM字段之间的映射。
exl-id: 33ee76f2-0495-4acd-a862-c942c0fa3177
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 7%

---

# [!DNL Salesforce]字段映射

下表包含[!DNL Salesforce]源字段及其相应的体验数据模型(XDM)字段之间的映射。

## 联系人 {#contact}

有关XDM类的更多信息，请阅读[XDM个人配置文件概述](../../../../xdm/classes/individual-profile.md)。 有关XDM字段组的详细信息，请阅读[XDM业务人员详细信息架构字段组](../../../../xdm/field-groups/profile/business-person-details.md)指南和[XDM业务人员组件架构字段组](../../../../xdm/field-groups/profile/business-person-components.md)指南。

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `AccountId` | `b2b.accountKey.sourceID` |  |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `b2b.accountKey` |  |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", AccountId, "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personComponents.sourceAccountKey` |  |
| `"Salesforce"` | `b2b.personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | 将自动替换`"${CRM_ORG_ID}"`的值。 |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `b2b.personKey.sourceKey` | 主要身份。 将自动替换`"${CRM_ORG_ID}"`的值。 |
| `AssistantName` | `extendedWorkDetails.assistantDetails.name.fullName` |  |
| `AssistantPhone` | `extendedWorkDetails.assistantDetails.phone.number` |  |
| `Birthdate` | `person.birthDate` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `Department` | `extendedWorkDetails.departments` |  |
| `Email` | `workEmail.address` | 辅助标识。 |
| `Email` | `personComponents.workEmail.address` |  |
| `Fax` | `faxPhone.number` |  |
| `FirstName` | `person.name.firstName` |  |
| `HomePhone` | `homePhone.number` |  |
| `isDeleted` | `isDeleted` |  |
| `Id` | `b2b.personKey.sourceID` |  |
| `"Salesforce"` | `personComponents.sourcePersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `personComponents.sourcePersonKey.sourceInstanceID` |  |
| `Id` | `personComponents.sourcePersonKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `personComponents.sourcePersonKey.sourceKey` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastName` | `person.name.lastName` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `LeadSource` | `b2b.personSource` |  |
| `LeadSource` | `personComponents.personSource` |  |
| `MailingCity` | `workAddress.city` |  |
| `MailingCountry` | `workAddress.country` |  |
| `MailingLatitude` | `workAddress._schema.latitude` |  |
| `MailingLongitude` | `workAddress._schema.longitude` |  |
| `MailingPostalCode` | `workAddress.postalCode` |  |
| `MailingState` | `workAddress.state` |  |
| `MailingStreet` | `workAddress.street1` |  |
| `MobilePhone` | `mobilePhone.number` |  |
| `Name` | `person.name.fullName` |  |
| `OtherCity` | `otherAddress.city` |  |
| `OtherCountry` | `otherAddress.country` |  |
| `OtherLatitude` | `otherAddress._schema.latitude` |  |
| `OtherLongitude` | `otherAddress._schema.longitude` |  |
| `OtherPhone` | `otherPhone.number` |  |
| `OtherPostalCode` | `otherAddress.postalCode` |  |
| `OtherState` | `otherAddress.state` |  |
| `OtherStreet` | `otherAddress.street1` |  |
| `Phone` | `workPhone.number` |  |
| `ReportsToId` | `extendedWorkDetails.reportsToID` |  |
| `Salutation` | `person.name.courtesyTitle` |  |
| `Title` | `extendedWorkDetails.jobTitle` |  |
| `"Contact"` | `b2b.personType` |  |

{style="table-layout:auto"}

## 潜在客户 {#lead}

有关XDM类的更多信息，请阅读[XDM个人配置文件概述](../../../../xdm/classes/individual-profile.md)。 有关XDM字段组的详细信息，请阅读[XDM业务人员详细信息架构字段组](../../../../xdm/field-groups/profile/business-person-details.md)指南和[XDM业务人员组件架构字段组](../../../../xdm/field-groups/profile/business-person-components.md)指南。

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `City` | `workAddress.city` |  |
| `ConvertedDate` | `b2b.convertedDate` |  |
| `Country` | `workAddress.country` |  |
| `Email` | `workEmail.address` | 辅助标识。 |
| `Email` | `personComponents.workEmail.address` |  |
| `Fax` | `faxPhone.number` |  |
| `FirstName` | `person.name.firstName` |  |
| `IsConverted` | `b2b.isConverted` |  |
| `isDeleted` | `isDeleted` |  |
| `"Salesforce"` | `b2b.personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` |  |
| `Id` | `b2b.personKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `b2b.personKey.sourceKey` | 主要身份。 将自动替换`"${CRM_ORG_ID}"`的值。 |
| `"Salesforce"` | `personComponents.sourcePersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `personComponents.sourcePersonKey.sourceInstanceID` |  |
| `Id` | `personComponents.sourcePersonKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `personComponents.sourcePersonKey.sourceKey` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastName` | `person.name.lastName` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `LeadSource` | `b2b.personSource` |  |
| `LeadSource` | `personComponents.personSource` |  |
| `Latitude` | `workAddress._schema.latitude` |  |
| `Longitude` | `workAddress._schema.longitude` |  |
| `Name` | `person.name.fullName` |  |
| `PostalCode` | `workAddress.postalCode` |  |
| `Salutation` | `person.name.courtesyTitle` |  |
| `State` | `workAddress.state` |  |
| `Status` | `b2b.personStatus` |  |
| `Status` | `personComponents.personStatus` |  |
| `Street` | `workAddress.street1` |  |
| `Title` | `extendedWorkDetails.jobTitle` |  |
| `Suffix` | `person.name.suffix` |  |
| `Company` | `b2b.companyName` |  |
| `Website` | `b2b.companyWebsite` |  |
| `ConvertedContactId` | `b2b.convertedContactKey.sourceID` |  |
| `iif(ConvertedContactId != null && ConvertedContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ConvertedContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `b2b.convertedContactKey` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `"Lead"` | `b2b.personType` |  |
| `iif(ConvertedContactId != null && ConvertedContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", ConvertedContactId, "sourceKey", concat(ConvertedContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personComponents.sourceConvertedContactKey` |  |

{style="table-layout:auto"}

## 帐户 {#account}

有关XDM类的详细信息，请阅读[XDM业务帐户详细信息概述](../../../../xdm/classes/b2b/business-account.md)。

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `"Salesforce"` | `accountKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | 将自动替换`"${CRM_ORG_ID}"`的值。 |
| `AccountNumber` | `accountNumber` |  |
| `AccountSource` | `accountSourceType` |  |
| `AnnualRevenue` | `accountOrganization.annualRevenue.amount` |  |
| `BillingCity` | `accountBillingAddress.city` |  |
| `BillingCountry` | `accountBillingAddress.country` |  |
| `BillingLatitude` | `accountBillingAddress._schema.latitude` |  |
| `BillingLongitude` | `accountBillingAddress._schema.longitude` |  |
| `BillingPostalCode` | `accountBillingAddress.postalCode` |  |
| `BillingState` | `accountBillingAddress.state` |  |
| `BillingStreet` | `accountBillingAddress.street1` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `Description` | `accountDescription` |  |
| `DunsNumber` | `accountOrganization.DUNSNumber` | data.com功能 |
| `Fax` | `accountFax.number` |  |
| `isDeleted` | `isDeleted` |  |
| `Id` | `accountKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `accountKey.sourceKey` | 主要身份。 将自动替换`"${CRM_ORG_ID}"`的值。 |
| `Industry` | `accountOrganization.industry` |  |
| `Jigsaw` | `accountOrganization.jigsaw` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `NaicsCode` | `accountOrganization.NAICSCode` | data.com功能 |
| `NaicsDesc` | `accountOrganization.NAICSDescription` | data.com功能 |
| `Name` | `accountName` |  |
| `NumberOfEmployees` | `accountOrganization.numberOfEmployees` |  |
| `Ownership` | `accountOwnership` |  |
| `ParentId` | `accountParentKey.sourceID` |  |
| `iif(ParentId != null && ParentId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ParentId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountParentKey` |  |
| `Phone` | `accountPhone.number` |  |
| `ShippingCity` | `accountShippingAddress.city` |  |
| `ShippingCountry` | `accountShippingAddress.country` |  |
| `ShippingLatitude` | `accountShippingAddress._schema.latitude` |  |
| `ShippingLongitude` | `accountShippingAddress._schema.longitude` |  |
| `ShippingPostalCode` | `accountShippingAddress.postalCode` |  |
| `ShippingState` | `accountShippingAddress.state` |  |
| `ShippingStreet` | `accountShippingAddress.street1` |  |
| `Sic` | `accountOrganization.SICCode` |  |
| `SicDesc` | `accountOrganization.SICDescription` |  |
| `Site` | `accountSite` |  |
| `TickerSymbol` | `accountOrganization.tickerSymbol` |  |
| `Tradestyle` | `accountTradeStyle` | data.com功能 |
| `Type` | `accountType` |  |
| `Website` | `accountOrganization.website` |  |

{style="table-layout:auto"}

## 机会 {#opportunity}

有关XDM类的详细信息，请阅读[XDM业务机会概述](../../../../xdm/classes/b2b/business-opportunity.md)。

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `"Salesforce"` | `opportunityKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | 将自动替换`"${CRM_ORG_ID}"`的值。 |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` | 主要身份。 将自动替换`"${CRM_ORG_ID}"`的值。 |
| `AccountId` | `accountKey.sourceID` |  |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountKey` | 关系。 |
| `Amount` | `opportunityAmount.amount` |  |
| `CampaignId` | `campaignKey.sourceID` |  |
| `iif(CampaignId != null && CampaignId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(CampaignId,"@${CRM_ORG_ID}.Salesforce")), null)` | `campaignKey` |  |
| `CloseDate` | `expectedCloseDate` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `Description` | `opportunityDescription` |  |
| `ExpectedRevenue` | `expectedRevenue.amount` |  |
| `FiscalQuarter` | `fiscalQuarter` |  |
| `FiscalYear` | `fiscalYear` |  |
| `ForecastCategory` | `forecastCategory` |  |
| `ForecastCategoryName` | `forecastCategoryName` |  |
| `Id` | `opportunityKey.sourceID` |  |
| `IsClosed` | `isClosed` |  |
| `isDeleted` | `isDeleted` |  |
| `IsWon` | `isWon` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `LeadSource` | `leadSource` |  |
| `Name` | `opportunityName` |  |
| `NextStep` | `nextStep` |  |
| `Probability` | `probabilityPercentage` |  |
| `StageName` | `opportunityStage` |  |
| `TotalOpportunityQuantity` | `opportunityQuantity` |  |
| `Type` | `opportunityType` |  |
| `CurrencyIsoCode` | `opportunityAmount.currencyCode` |  |

{style="table-layout:auto"}

## 机会联系人角色 {#opportunity-contact-role}

有关XDM类的详细信息，请阅读[XDM业务机会人员关系类概述](../../../../xdm/classes/b2b/business-opportunity-person-relation.md)。

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `"Salesforce"` | `opportunityPersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | 将自动替换`"${CRM_ORG_ID}"`的值。 |
| `"Salesforce"` | `personKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `personKey.sourceInstanceID` |  |
| `ContactId` | `personKey.sourceID` |  |
| `concat(ContactId,"@${CRM_ORG_ID}.Salesforce")` | `personKey.sourceKey` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `Id` | `opportunityPersonKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `opportunityPersonKey.sourceKey` | 主要身份。 将自动替换`"${CRM_ORG_ID}"`的值。 |
| `isDeleted` | `isDeleted` |  |
| `IsPrimary` | `isPrimary` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `"Salesforce"` | `opportunityKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` |  |
| `OpportunityId` | `opportunityKey.sourceID` |  |
| `concat(OpportunityId,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` |  |
| `Role` | `personRole` |  |

{style="table-layout:auto"}

## Campaign {#campaign}

有关XDM类的详细信息，请阅读[XDM商业营销活动类概述](../../../../xdm/classes/b2b/business-campaign.md)。 有关XDM字段组的详细信息，请阅读[XDM商业营销活动详细信息架构字段组](../../../../xdm/field-groups/b2b-campaign/details.md)指南。

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `"Salesforce"` | `campaignKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | 将自动替换`"${CRM_ORG_ID}"`的值。 |
| `isDeleted` | `isDeleted` |  |
| `Id` | `campaignKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `campaignKey.sourceKey` | 主要身份。 将自动替换`"${CRM_ORG_ID}"`的值。 |
| `Name` | `campaignName` |  |
| `ParentId` | `parentCampaignKey.sourceID` |  |
| `iif(ParentId != null && ParentId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ParentId,"@${CRM_ORG_ID}.Salesforce")), null)` | `parentCampaignKey` |  |
| `Type` | `campaignType` |  |
| `Status` | `campaignStatus` |  |
| `StartDate` | `campaignStartDate` |  |
| `EndDate` | `campaignEndDate` |  |
| `ExpectedRevenue` | `expectedRevenue.amount` |  |
| `BudgetedCost` | `budgetedCost.amount` |  |
| `ActualCost` | `actualCost.amount` |  |
| `ExpectedResponse` | `expectedResponse` |  |
| `IsActive` | `isActive` |  |
| `Description` | `campaignDescription` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |  |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |  |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |  |
| `CurrencyIsoCode` | `actualCost.currencyCode` |  |

## 营销活动成员 {#campaign-member}

有关XDM类的详细信息，请阅读[XDM商业营销活动成员概述](../../../../xdm/classes/b2b/business-campaign-members.md)。 有关XDM字段组的详细信息，请阅读[XDM商业营销活动成员详细信息架构字段组](../../../../xdm/field-groups/b2b-campaign/details.md)文档。

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `"Salesforce"` | `campaignMemberKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `campaignMemberKey.sourceInstanceID` | 将自动替换`"${CRM_ORG_ID}"`的值。 |
| `isDeleted` | `isDeleted` |  |
| `Id` | `campaignMemberKey.sourceID` |  |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `campaignMemberKey.sourceKey` | 主要身份。 将自动替换`"${CRM_ORG_ID}"`的值。 |
| `"Salesforce"` | `campaignKey.sourceType` |  |
| `${CRM_ORG_ID}` | `campaignKey.sourceInstanceID` |  |
| `CampaignId` | `campaignKey.sourceID` |  |
| `concat(CampaignId,"@${CRM_ORG_ID}.Salesforce")` | `campaignKey.sourceKey` |  |
| `"Salesforce"` | `personKey.sourceType` |  |
| `${CRM_ORG_ID}` | `personKey.sourceInstanceID` |  |
| `LeadOrContactId` | `personKey.sourceID` |  |
| `concat(LeadOrContactId,"@${CRM_ORG_ID}.Salesforce")` | `personKey.sourceKey` |  |
| `Status` | `memberStatus` |  |
| `HasResponded` | `hasResponded` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `FirstRespondedDate` | `firstRespondedDate` |  |
| `Type` | `b2b.personType` |  |

## 帐户联系人关系 {#account-contact-relation}

有关XDM类的详细信息，请阅读[XDM业务帐户人员关系类](../../../../xdm/classes/b2b/business-account-person-relation.md)。

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `AccountId` | `accountKey.sourceID` |  |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountKey` |  |
| `ContactId` | `personKey.sourceID` |  |
| `iif(ContactId != null && ContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personKey` |  |
| `CreatedById` | `extSourceSystemAudit.createdBy` |  |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |  |
| `EndDate` | `relationEndDate` |  |
| `IsDeleted` | `isDeleted` |  |
| `Id` | `accountPersonKey.sourceID` |  |
| `"Salesforce"` | `accountPersonKey.sourceType` |  |
| `"${CRM_ORG_ID}"` | `accountPersonKey.sourceInstanceID` |  |
| `concat(Id, "@${CRM_ORG_ID}.Salesforce")` | `accountPersonKey.sourceKey` | 主要身份。 |
| `IsActive` | `IsActive` |  |
| `IsDirect` | `IsDirect` |  |
| `LastModifiedById` | `extSourceSystemAudit.lastUpdatedBy` |  |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `explode(Roles,";")` | `personRoles[]` |  |
| `StartDate` | `relationStartDate` |  |

## 后续步骤

通过阅读本文档，您已获得[!DNL Salesforce]源字段及其相应XDM字段之间的映射关系的insight。 有关详细信息，请参阅有关[创建 [!DNL Salesforce] 源连接](../../../connectors/crm/salesforce.md)的文档。
