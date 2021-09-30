---
keywords: Experience Platform；主页；热门主题；Salesforce;Salesforce；字段映射；字段映射；映射；Marketo;B2B;b2b
solution: Experience Platform
title: Salesforce映射字段
topic-legacy: overview
description: 下表包含Salesforce源字段与其对应XDM字段之间的映射。
source-git-commit: 00207ae10979b48d190cbda63aecf55e0f6d0f9c
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 11%

---

# [!DNL Salesforce] 字段映射

下表包含[!DNL Salesforce]源字段与其相应的体验数据模型(XDM)字段之间的映射。

## 联系人 {#contact}

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `AccountId` | `b2b.accountID` |
| `AccountId` | `personComponents.sourceAccountID` |
| `AssistantName` | `extendedWorkDetails.assistantDetails.name.fullName` |
| `AssistantPhone` | `extendedWorkDetails.assistantDetails.phone.number` |
| `Birthdate` | `person.birthDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Department` | `extendedWorkDetails.departments` |
| `Email` | `workEmail.address` | 这是次标识。 |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `HomePhone` | `homePhone.number` |
| `Id` | `personID` | 这是主标识 |
| `Id` | `personComponents.sourcePersonID` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastName` | `person.name.lastName` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `b2b.personSource` |
| `LeadSource` | `personComponents.personSource` |
| `MailingCity` | `workAddress.city` |
| `MailingCountry` | `workAddress.country` |
| `MailingLatitude` | `workAddress._schema.latitude` |
| `MailingLongitude` | `workAddress._schema.longitude` |
| `MailingPostalCode` | `workAddress.postalCode` |
| `MailingState` | `workAddress.state` |
| `MailingStreet` | `workAddress.street1` |
| `MobilePhone` | `mobilePhone.number` |
| `Name` | `person.name.fullName` |
| `OtherCity` | `otherAddress.city` |
| `OtherCountry` | `otherAddress.country` |
| `OtherLatitude` | `otherAddress._schema.latitude` |
| `OtherLongitude` | `otherAddress._schema.longitude` |
| `OtherPhone` | `otherPhone.number` |
| `OtherPostalCode` | `otherAddress.postalCode` |
| `OtherState` | `otherAddress.state` |
| `OtherStreet` | `otherAddress.street1` |
| `Phone` | `workPhone.number` |
| `ReportsToId` | `extendedWorkDetails.reportsToID` |
| `Salutation` | `person.name.courtesyTitle` |
| `Title` | `extendedWorkDetails.jobTitle` |

{style=&quot;table-layout:auto&quot;}

## 商机 {#lead}

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `City` | `workAddress.city` |
| `ConvertedContactId` | `b2b.convertedContactID` |
| `ConvertedContactId` | `personComponents.sourceConvertedContactID` |
| `ConvertedDate` | `b2b.convertedDate` |
| `Country` | `workAddress.country` |
| `Email` | `workEmail.address` | 这是次标识 |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `IsConverted` | `b2b.isConverted` |
| `Id` | `personID` | 这是主标识 |
| `Id` | `personComponents.sourcePersonID` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastName` | `person.name.lastName` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `b2b.personSource` |
| `LeadSource` | `personComponents.personSource` |
| `Latitude` | `workAddress._schema.latitude` |
| `Longitude` | `workAddress._schema.longitude` |
| `MiddleName` | `person.name.middleName` |
| `Name` | `person.name.fullName` |
| `PostalCode` | `workAddress.postalCode` |
| `Salutation` | `person.name.courtesyTitle` |
| `State` | `workAddress.state` |
| `Status` | `b2b.personStatus` |
| `Status` | `personComponents.personStatus` |
| `Street` | `workAddress.street1` |
| `Title` | `extendedWorkDetails.jobTitle` |
| `Suffix` | `person.name.suffix` |

{style=&quot;table-layout:auto&quot;}

## 帐户 {#account}

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `AccountNumber` | `accountNumber` |
| `AccountSource` | `accountSourceType` |
| `AnnualRevenue` | `accountOrganization.annualRevenue.amount` |
| `BillingCity` | 地址 | `accountBillingAddress.city` |
| `BillingCountry` | `accountBillingAddress.country` |
| `BillingLatitude` | `accountBillingAddress._schema.latitude` |
| `BillingLongitude` | `accountBillingAddress._schema.longitude` |
| `BillingPostalCode` | `accountBillingAddress.postalCode` |
| `BillingState` | `accountBillingAddress.state` |
| `BillingStreet` | `accountBillingAddress.street1` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `accountDescription` |
| `DunsNumber` | `accountOrganization.DUNSNumber` | data.com功能 |
| `Fax` | `accountFax.number` |
| `Id` | `accountID` | 这是主标识 |
| `Industry` | `accountOrganization.industry` |
| `Jigsaw` | `accountOrganization.jigsaw` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `NaicsCode` | `accountOrganization.NAICSCode` | data.com功能 |
| `NaicsDesc` | `accountOrganization.NAICSDescription` | data.com功能 |
| `Name` | `accountName` |
| `NumberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `Ownership` | `accountOwnership` |
| `ParentId` | `accountParentID` |
| `Phone` | `accountPhone.number` |
| `Rating` | `accountOrganization.rating` |
| `ShippingCity` | `accountShippingAddress.city` |
| `ShippingCountry` | `accountShippingAddress.country` |
| `ShippingLatitude` | `accountShippingAddress._schema.latitude` |
| `ShippingLongitude` | `accountShippingAddress._schema.longitude` |
| `ShippingPostalCode` | `accountShippingAddress.postalCode` |
| `ShippingState` | `accountShippingAddress.state` |
| `ShippingStreet` | `accountShippingAddress.street1` |
| `Sic` | `accountOrganization.SICCode` |
| `SicDesc` | `accountOrganization.SICDescription` |
| `Site` | `accountSite` |
| `TickerSymbol` | `accountOrganization.tickerSymbol` |
| `Tradestyle` | `accountTradeStyle` | data.com功能 |
| `Type` | `accountType` |

{style=&quot;table-layout:auto&quot;}

## 机会 {#opportunity}

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `AccountId` | `accountID` | 关系 |
| `Amount` | `opportunityAmount.amount` |
| `CampaignId` | `campaignID` |
| `CloseDate` | `actualCloseDate` / `expectedCloseDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `opportunityDescription` |
| `ExpectedRevenue` | `expectedRevenue.amount` |
| `FiscalQuarter` | `fiscalQuarter` |
| `FiscalYear` | `fiscalYear` |
| `ForecastCategory` | `forecastCategory` |
| `ForecastCategoryName` | `forecastCategoryName` |
| `Id` | `opportunityID` | 这是主标识 |
| `IsClosed` | `isClosed` |
| `IsWon` | `isWon` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `leadSource` |
| `Name` | `opportunityName` |
| `NextStep` | `nextStep` |
| `Probability` | `probabilityPercentage` |
| `StageName` | `opportunityStage` |
| `TotalOpportunityQuantity` | `opportunityQuantity` |
| `Type` | `opportunityType` |

{style=&quot;table-layout:auto&quot;}

## 机会联系角色 {#opportunity-contact-role}

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `ContactId` | `personID` | 关系 |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Id` | `opportunityPersonID` | 这是主标识 |
| `IsPrimary` | `isPrimary` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `OpportunityId` | `opportunityID` | 关系 |
| `Role` | `personRole` |

{style=&quot;table-layout:auto&quot;}

## Campaign {#campaign}

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `Id` | `xdm: campaignID` | 这是主标识 |
| `Name` | `xdm: campaignName` |
| `ParentId` | `xdm: parentCampaignID` |
| `Type` | `xdm: campaignType` |
| `Status` | `xdm: campaignStatus` |
| `StartDate` | `xdm: campaignStartDate` |
| `EndDate` | `xdm: campaignEndDate` |
| `ExpectedRevenue` | `xdm: expectedRevenue.amount` |
| `BudgetedCost` | `xdm: budgetedCost.amount` |
| `ActualCost` | `xdm: actualCost.amount` |
| `ExpectedResponse` | `xdm: expectedResponse` |
| `IsActive` | `xdm: isActive` |
| `Description` | `xdm: campaignDescription` |
| `CreatedDate` | `xdm: extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `xdm: extSourceSystemAudit.lastUpdatedDate` |
| `LastActivityDate` | `xdm: extSourceSystemAudit.lastActivityDate` |
| `LastViewedDate` | `xdm: extSourceSystemAudit.lastViewedDate` |
| `LastReferencedDate` | `xdm: extSourceSystemAudit.lastReferencedDate` |

## 营销活动成员 {#campaign-member}

| 源字段 | 目标XDM字段路径 | 注释 |
| --- | --- | --- |
| `Id` | `campaignMemberID` | 这是主标识 |
| `CampaignId` | `campaignID` | 关系 |
| `LeadOrContactId` | `personID` | 关系 |
| `Status` | `memberStatus` |
| `HasResponded` | `hasResponded` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `FirstRespondedDate` | `firstRespondedDate` |

## 后续步骤

通过阅读本文档，您对[!DNL Salesforce]源字段与其对应XDM字段之间的映射关系有了深入的了解。 请参阅有关创建 [!DNL Salesforce] 源连接](../../../tutorials/ui/create/crm/salesforce.md)以启动[!DNL Salesforce]数据流的教程。[
