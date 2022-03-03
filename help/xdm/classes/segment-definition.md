---
solution: Experience Platform
title: Segment Definition Class
topic-legacy: overview
description: This document provides an overview of the Segment definition class in Experience Data Model (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---

# 

The class includes required fields such as the ID and name of a segment, along with other optional attributes. This class should be used if you are bringing in segment definitions from external systems into Adobe Experience Platform.

>[!NOTE]
>
>This class should only be used to capture information about segment definitions themselves. [](../field-groups/profile/segmentation.md)

![](../images/classes/segment-definition.png)

| 屬性 | 說明 |
| --- | --- |
| `_repo` |  <ul><li>`createDate`</li><li>`modifyDate`</li></ul> |
| `_id` | A unique, system-generated string identifier for the record. This field is used to track the uniqueness of an individual record, prevent duplication of data, and to look up that record in downstream services.<br><br>However, you can still opt to supply your own unique ID values if you wish.<br><br>****[](../schema/composition.md#identity) |
| `createdByBatchID` | The ID of the ingested batch that caused the record to be created. |
| `description` | A description for the segment definition. |
| `identityMap` | A map field that contains a set of namespaced identities for the individuals the segment applies to. [](../schema/composition.md#identityMap) |
| `modifiedByBatchID` | The ID of the last ingested batch that caused the record to be updated. |
| `repositoryCreatedBy` | The ID of the user who created the record. |
| `repositoryLastModifiedBy` | The ID of the user who last modified the record. |
| `segmentName` | **** |
| `segmentStatus` | The status of the segment from the external system. The following values are accepted: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | The latest version number of the segment definition. |

{style=&quot;table-layout:auto&quot;}
