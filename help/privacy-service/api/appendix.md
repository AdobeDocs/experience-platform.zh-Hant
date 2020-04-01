---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 接受的身份名稱空間和限定詞
topic: developer guide
translation-type: tm+mt
source-git-commit: d0fcae6b1b75584a2c26d6eee5b47e0d60a142ba

---


# 附錄

## 標準身分名稱空間

所有傳送至隱私權服務的身分必須以特定的身分命名空間提供。 身分名稱空間是 [Adobe Experience Platform Identity Service的元件](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_services_architectural_overview/identity_services_architectural_overview.md) ，可指出身分相關的上下文。

下表概述Experience Platform提供的幾種常用、預先定義的身分類型，以及其相關 `namespace` 值：

| 身分類型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 電子郵件 | 電子郵件 | 6 |
| 電話 | 電話 | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| Adobe Audience Manager UUID | 核心 | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Target ID | TNTID | 9 |
| 廣告商的Apple ID | IDFA | 20915 |
| Google廣告ID | GAID | 20914 |
| Windows AID | WAID | 8 |

>[!NOTE] 每個身分類型也有 `namespaceId` 一個整數值，當將身分屬性設定為&quot;namespaceId&quot;時， `namespace` 可使用此整 `type` 數值來取代字串。 如需詳細資訊，請參 [閱命名空間限](#namespace-qualifiers) 定詞一節。

您可以向Identity Service API中的端點提出GET請求，以擷取組織所使 `idnamespace/identities` 用的識別名稱空間清單。 如需詳細 [資訊，請參閱Identity Service開發人員指南](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_services_architectural_overview/identity_services_api.md) 。

## 命名空間限定詞

在隱私權服 `namespace` 務API中指定值時，命名空 **間限定詞** ，必須包含在對應的參 `type` 數中。 下表概述了不同接受的命名空間限定詞。

| 限定詞 | 定義 |
| --------- | ---------- |
| 標準 | 其中一個標準名稱空間是全域定義的，不會系結至個別組織資料集（例如，電子郵件、電話號碼等）。 提供命名空間ID。 |
| 自訂 | 在組織內容中建立、未在Experience Cloud間共用的獨特命名空間。 值代表要搜尋的好記名稱（&quot;name&quot;欄位）。 提供命名空間ID。 |
| integrationCode | 整合代碼——類似「自訂」，但明確定義為要搜尋之資料來源的整合代碼。 提供命名空間ID。 |
| namespaceId | 指出值是透過namespace服務建立或映射之namespace的實際ID。 |
| 未註冊 | 未在namespace服務中定義且採用「原樣」的自由格式字串。 任何處理這些類型名稱空間的應用程式都會針對它們進行檢查，並處理（如果適合公司內容和資料集）。 未提供命名空間ID。 |
| analytics | 在Analytics中內部映射的自訂命名空間，而不是在namespace服務中。 這會直接依原始請求所指定的方式傳入，但沒有命名空間ID |
| Target | Target內部瞭解的自訂命名空間，而非namespace服務。 這會直接依原始請求所指定的方式傳入，但沒有命名空間ID |

## 接受的產品值

下表概述在工作建立請求的屬性中指定Adobe `include` 產品的接受值。

| 產品 | 用於屬性中的 `include` 值 |
--- | ---
| Adobe Advertising Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;促銷活動&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Adobe Primetime驗證 | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| 客戶記錄服務 | &quot;CRS&quot; |
| 即時客戶個人檔案 | &quot;ProfileService&quot; |