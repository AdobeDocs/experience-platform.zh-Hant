---
title: 藥物類別
description: 瞭解Experience Data Model (XDM)中的Media類別。
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# [!UICONTROL 藥物]類別

在Experience Data Model (XDM)中，[!UICONTROL Media]類別會擷取定義用於醫療的物質（尤其是藥物或藥物）的最小屬性集。

![類別結構](../images/classes/medication.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字串] | 記錄的唯一、系統產生的字串識別碼。 此欄位用於追蹤個別記錄的唯一性、防止資料重複，以及在下游服務中查詢該記錄。<br><br>由於此欄位是由系統產生，因此在資料擷取期間不會提供明確的值。 不過，您仍然可以視需要選擇提供自己的唯一ID值。 |
| `medicationId` | [!UICONTROL 字串] | 適用於藥物的唯一識別碼。 |
| `medicationName` | [!UICONTROL 字串] | 藥物的名稱。 |

{style="table-layout:auto"}

這個類別可以與[[!UICONTROL 醫療保健藥物]欄位群組](../field-groups/medication/healthcare-medication.md)一起擴充，以說明藥物或藥物的進一步詳細資訊。
