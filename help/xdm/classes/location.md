---
title: 位置類別
description: 瞭解體驗資料模型(XDM)中的Location類別。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 7%

---

# [!UICONTROL 位置]類別

在Experience Data Model (XDM)中，[!UICONTROL Location]類別會擷取即時活動位置資訊，例如旅行館或運動競技場。

![位置類別結構](../images/classes/location.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
| --- | --- | --- | --- |
| [!UICONTROL 識別碼] | `_id` | [!UICONTROL 字串] | 記錄的唯一、系統產生的字串識別碼。 此欄位用於追蹤個別記錄的唯一性、防止資料重複，以及在下游服務中查詢該記錄。<br><br>由於此欄位是由系統產生，因此不需要在資料擷取期間提供明確的值。 不過，您仍然可以視需要選擇提供自己的唯一ID值。 |
| [!UICONTROL 位置識別碼] | `locationID` | [!UICONTROL 字串] | 位置的唯一識別碼。 |
| [!UICONTROL 位置名稱] | `locationName` | [!UICONTROL 字串] | 位置的名稱。 |

類別可以使用[[!UICONTROL 位置]欄位群組](../field-groups/location/healthcare-location.md)擴充，以說明有關位置的進一步詳細資訊。
