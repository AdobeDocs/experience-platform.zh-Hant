---
title: 自訂中繼資料詳細資料報表資料型別
description: 瞭解自訂中繼資料詳細資料報告Experience Data Model (XDM)資料型別。
exl-id: d82d42fb-c725-4a81-9b2a-f6434020ab49
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 5%

---

# [!UICONTROL 自訂中繼資料詳細資料]報告資料型別

[!UICONTROL 自訂中繼資料詳細資料]報表是標準的體驗資料模型(XDM)資料型別，定義儲存自訂中繼資料的結構。 [!UICONTROL 自訂中繼資料詳細資料]報表資料型別會擷取詳細資料，例如與內容或互動相關聯的自訂中繼資料的名稱和值。 Adobe服務會使用媒體報表欄位來分析使用者傳送的媒體收集欄位。 系統會計算此資料以及其他特定使用者量度，並據此回報。

![自訂中繼資料詳細資料報表資料型別的圖表。](../images/data-types/the-custom-metadata-reporting.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL 自訂中繼資料欄位名稱] | `name` | 字串 | 自訂欄位的名稱。 |
| [!UICONTROL 自訂中繼資料欄位值] | `value` | 字串 | 自訂欄位的值。 |

{style="table-layout:auto"}
