---
title: 自訂中繼資料詳細資料報表資料型別
description: 瞭解自訂中繼資料詳細資料報告Experience Data Model (XDM)資料型別。
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 4%

---

# [!UICONTROL 自訂中繼資料詳細資訊] 報表資料型別

[!UICONTROL 自訂中繼資料詳細資訊] 「報表」是一種標準Experience Data Model (XDM)資料型別，可定義儲存自訂中繼資料的結構。 此 [!UICONTROL 自訂中繼資料詳細資訊] 報表資料型別會擷取詳細資訊，例如與內容或互動相關聯的自訂中繼資料的名稱和值。 Adobe服務會使用媒體報表欄位來分析使用者傳送的媒體收集欄位。 系統會計算此資料以及其他特定使用者量度，並據此回報。

![「自訂中繼資料詳細資訊」報表資料型別的圖表。](../images/data-types/the-custom-metadata-reporting.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL 自訂中繼資料欄位名稱] | `name` | 字串 | 自訂欄位的名稱。 |
| [!UICONTROL 自訂中繼資料欄位值] | `value` | 字串 | 自訂欄位的值。 |

{style="table-layout:auto"}
