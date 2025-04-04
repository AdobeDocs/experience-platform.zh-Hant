---
title: 資料Distiller Authorization API指南
description: 瞭解如何使用Data Distiller Authorization API來強制執行透過SQL的安全連線的網路型IP限制。 使用此API可增強您Adobe Experience Platform資料的資料存取控制。
role: Developer
exl-id: bcc5ea0e-cb6d-4c7b-bf9f-a0336f76c4c8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---

# 資料Distiller Authorization API指南

>[!AVAILABILITY]
>
>已購買Data Distiller附加元件的客戶可使用此功能。 如需詳細資訊，請聯絡您的 Adobe 代表。

使用資料Distiller授權API來強制執行IP型限制。 套用這些措施，可確保只有經過核准的網路和使用者端電腦才能透過Adobe Experience Platform中的SQL存取資料。 這些控制功能可協助您符合嚴格的安全性標準，同時提供即時存取監控和警報。

使用此API，您可以設定、強制執行並監視透過SQL介面存取資料的IP限制。 本檔案提供API核心功能、端點功能和未來功能的概觀。

## 主要功能

下列功能可讓您定義IP型存取限制、監視存取嘗試，以及自訂查詢服務的網路安全性設定：

- **定義網路型資料存取控制**：指定查詢服務存取允許的IP範圍。 此限制特別適用於SQL資料庫連線，包括透過Business Intelligence (BI)工具、資料庫使用者端或程式設計介面（例如JDBC）建立的連線。
- **啟用完整的監視和警示**：所有存取嘗試（包括被拒絕的連線）都會記錄並傳送到[Adobe Experience Platform稽核記錄](../../landing/governance-privacy-security/audit-logs/overview.md)以進行即時追蹤。 使用此功能來監控存取模式，並偵測潛在的安全性違規。
- **設定彈性的IP限制**：以個別IP和CIDR區塊格式指定允許的IP。 這些設定適用於每個沙箱，可讓您根據特定安全需求量身打造網路限制。

## 稽核與監控功能

為了支援安全資料存取實務，查詢服務會記錄所有存取或嘗試存取Experience Platform的使用者端IP。 稽核事件（包括被拒絕的連線）會傳送至Experience Platform稽核記錄。 如此可啟用：

- **即時監視**：追蹤IP型存取模式以確保法規遵循。
- **未授權存取警示**：識別並回應未授權IP的存取嘗試。

如需詳細資訊，請參閱[稽核記錄總覽](../../landing/governance-privacy-security/audit-logs/overview.md)。

## 後續步驟

檢閱[快速入門手冊](./getting-started.md)以開始使用Data Distiller Authorization API，瞭解必要的設定步驟，包括必要的標頭和API呼叫慣例。 然後，探索端點特定的[IP存取](./ip-access.md)和[IP驗證](./validate.md)指南，以設定和管理安全資料存取。

請參閱[Data Distiller Authorization OpenAPI參考檔案](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/)，以檢視標準化、機器可讀的格式，更易於整合、測試和探索。

如需每個傳回資料集的不同回應引數相關資訊，請參閱[資料集API開發人員檔案](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets)。
