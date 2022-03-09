---
keywords: Experience Platform;profile;real-time customer profile;user interface;UI;customization;profile dashboard;dashboard
title: Profiles Dashboard
description: Adobe Experience Platform provides a dashboard through which you can view important information about your organization's Real-time Customer Profile data.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 7dd7cccfe17d360b072783823517e847a50166e6
workflow-type: tm+mt
source-wordcount: '2324'
ht-degree: 1%

---

# 

[!DNL Real-time Customer Profile]

[](../../profile/ui/user-guide.md)

## Profile dashboard data

The snapshot does not include any event (time series) data.

The attribute data in the snapshot shows the data exactly as it appears at the specific point in time when the snapshot was taken. In other words, the snapshot is not an approximation or sample of the data, and the Profile dashboard is not updating in real time.

>[!NOTE]
>
>Any changes or updates made to the data since the snapshot was taken will not be reflected in the dashboard until the next snapshot is taken.

## 

********

>[!NOTE]
>
>

![](../images/profiles/dashboard-overview.png)

### 

********

[](../customize/modify.md)[](../customize/widget-library.md)

## (Beta) Profile efficacy insights {#profile-efficacy-insights}

>[!IMPORTANT]
>
>The profile efficacy insight functionality is currently in beta and are not available to all users. 文档和功能可能会发生变化。

These widgets illustrate at a glance the composition of your profiles, trends in completeness over time, and assessments on the quality of your profile data.

![](../images/profiles/attributes-quality-assessment.png)

[](#profile-efficacy-widgets)

[****](../customize/modify.md)

## Browse profiles {#browse-profiles}

From here you can see important information belonging to the profile regarding their preferences, past events, interactions, and segments

[](../../rtcdp/profile/profile-browse.md)

## Merge policies {#merge-policies}

When data is brought together from multiple sources to create the customer profile, it is possible for the data to contain conflicting values (for example, one dataset may list a customer as &quot;single&quot; while another dataset may list the customer as &quot;married&quot;). It is the job of the merge policy to determine which data to prioritize and display as part of the profile.

[](../../profile/merge-policies/overview.md)

The dashboard will automatically select a merge policy to display, but you can change the merge policy that is selected using the drop down menu. To choose a different merge policy, select the drop down next to the merge policy name and then select the merge policy that you wish to view.

>[!NOTE]
>
>The dropdown menu shows only merge policies related to the XDM Individual Profile Class, however if your organization has created multiple merge policies, it may mean that you will need to scroll in order to view the complete list of available merge policies.

![](../images/profiles/select-merge-policy.png)

## Union schemas

[!UICONTROL ****]

Union schemas are composed of multiple schemas that share the same class and have been enabled for Profile. They enable you to see in a single view, an amalgamation of every field contained within each schema that shares the same class.

[](../../profile/ui/union-schema.md#view-union-schemas)

## Widgets and metrics

The dashboard is composed of widgets, which are read-only metrics providing important information regarding your Profile data.

The &quot;last updated&quot; date and time on a widget shows when the last snapshot of the data was taken. The date and time of the snapshot is provided in UTC; it is not in the timezone of the individual user or IMS Organization.

## Standard widgets

Adobe provides multiple standard widgets that you can use to visualize different metrics related to your Profile data. [](../customize/widget-library.md)

To learn more about each of the available standard widgets, select the name of a widget from the following list:

* [](#profile-count)
* [](#profiles-added)
* [](#profiles-count-trend)
* [](#profiles-by-identity)
* [](#identity-overlap)

###  {#profile-count}

**** This number is the result of the selected merge policy being applied to your Profile data in order to merge profile fragments together to form a single profile for each individual.

[](#merge-policies)

>[!NOTE]
>
>
>
>[](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count)

![](../images/profiles/profile-count.png)

###  {#profiles-added}

**** This number is the result of the selected merge policy being applied to your Profile data in order to merge profile fragments together to form a single profile for each individual. You can use the dropdown selector to view the profiles added over the last 30 days, 90 days, or 12 months.

>[!NOTE]
>
>This is done to avoid a spike associated with the initial ingestion of profiles into the system. Over the next 30 days, your organization ingests an additional 1,000,000 profiles into the Profile Store. 

![](../images/profiles/profiles-added.png)

###  {#profiles-count-trend}

**** This number is updated each day when the snapshot is taken, therefore if you were to ingest profiles into Platform, the number of profiles would not be reflected until the next snapshot is taken. The count of profiles added is the result of the selected merge policy being applied to your Profile data in order to merge profile fragments together to form a single profile for each individual.

[](#merge-policies)

********

![](../images/profiles/profile-count-trend-captions.png)

A machine learning model automatically generates captions for describing the key trends and important events by analyzing the chart and the data.

![](../images/profiles/profiles-count-trends-automatic-captions-dialog.png)

###  {#profiles-by-identity}

**** The total number of profiles by identity (in other words, adding together the values shown for each namespace) may be higher than the total number of merged profiles because one profile could have multiple namespaces associated with it. For example, if a customer interacts with your brand on more than one channel, multiple namespaces will be associated with that individual customer.

[](#merge-policies)

[](../../identity-service/home.md)

![](../images/profiles/profiles-by-identity.png)

###  {#identity-overlap}

****

After using the dropdown menus on the widget to select the identities that you wish to compare, circles appear displaying the relative size of each identity, with the number of profiles containing both namespaces being represented by the size of the overlap between the circles. If a customer interacts with your brand on more than one channel, multiple identities will be associated with that individual customer, therefore it is likely that your organization will have multiple profiles containing fragments from more than one identity.

[](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles)

[](../../identity-service/home.md)

![](../images/profiles/identity-overlap.png)

## (Beta) Profile efficacy widgets {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>The profile efficacy widgets are currently in Beta and are not available to all users. 文档和功能可能会发生变化。

Adobe provides multiple widgets to asses the completeness of the ingested profiles available for your data analysis. Each of the profile efficacy widgets can be filtered by merge policy. 

To learn more about each of the profile efficacy widgets, select the name of a widget from the following list:

* [](#attribute-quality-assessment)
* [](#profile-completeness)
* [](#profile-completeness-trend)

###  {#attribute-quality-assessment}

This widget shows the completeness and cardinality of each profile attribute since the last processing date. This information is presented as a table with four columns where each row in the table represents a single attribute.

| 栏目 | 描述 |
|---|---|
| 属性 | The name of the attribute. |
| 用户档案 | The number of profiles that have this attribute and are filled with non-null values. |
| Completeness | This percentage is determined by the total number of profiles that have this attribute and are filled with non-null values. The number is calculated by dividing the the total number of profiles by the total number of non-empty values in the profiles for that attribute. |
| Cardinality | **** It is measured across all profiles. |

![](../images/profiles/attributes-quality-assessment.png)

###  {#profile-completeness}

This widget creates a circle chart of profile completeness since the last processing date. The completeness of a profile is measured by the percentage of attributes that are filled with non-null values among all observed attributes.

This widget shows the proportion of profiles that are of high, medium, or low completeness. By default, there are three levels of completeness configured:

* High completeness: Profiles have more than 70% attributes filled.
* Medium completeness: Profiles have less than 70% and more than 30% attributes filled.
* Low completeness: Profiles have less than 30% attributes filled.

![](../images/profiles/profiles-by-completeness.png)

###  {#profile-completeness-trend}

This widget creates a stacked column chart to depict the trend of profile completeness over time. Completeness is measured by the percentage of attributes are filled with non-null values among all observed attributes. It categorizes the profile completeness as high, medium, or low completeness since the last processing date.

The x-axis represents time, the y-axis represents the number of profiles, and the colors represent the three levels of profile completeness.

The three levels of completeness are:

* High completeness: Profiles have more than 70% attributes filled.
* Medium completeness: Profiles have less than 70% and more than 30% attributes filled.
* Low completeness: Profiles have less than 30% attributes filled.

![](../images/profiles/profiles-completeness-trend.png)

## 后续步骤

By following this document you should now be able to locate the Profiles dashboard and understand the metrics displayed in the available widgets. [!DNL Profile][](../../profile/ui/user-guide.md)
