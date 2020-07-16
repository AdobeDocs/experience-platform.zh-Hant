---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 接受的身份名稱空間和限定詞
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 9%

---


# 附錄

## 標準身分名稱空間 {#standard-namespaces}

所有傳送至的身分必須以 [!DNL Privacy Service] 特定的身分命名空間提供。 身分名稱空間是 [Adobe Experience Platform Identity Service的元件](../../identity-service/home.md) ，可指出身分相關的上下文。

下表概述了幾種常用的預先定義識別類型，這些類型由提供， [!DNL Experience Platform]以及它們的關聯 `namespace` 值：

| 身分類型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 電子郵件 | 電子郵件 | 6 |
| 電話 | 電話 | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| Adobe Audience Manager UUID | 核心 | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Target ID | TNTID | 9 |
| [!DNL Apple] 廣告商的ID | IDFA | 20915 |
| [!DNL Google] 廣告 ID | GAID | 20914 |
| [!DNL Windows] AID | WAID | 8 |

>[!NOTE]
>
>每個身分類型也有 `namespaceId` 一個整數值，當將身分屬性設定為&quot;namespaceId&quot;時， `namespace` 可使用此整 `type` 數值來取代字串。 如需詳細資訊，請參 [閱命名空間限](#namespace-qualifiers) 定詞一節。

您可以向API中的端點提出GET請求，以擷取組織所使用之識 `idnamespace/identities` 別名稱空間 [!DNL Identity Service] 清單。 如需詳細 [資訊，請參閱Identity Service開發人員指南](../../identity-service/api/getting-started.md) 。

## 命名空間限定詞

在API中指 `namespace` 定值時，命名空間限 [!DNL Privacy Service] 定符必須包含在對應的參 ****`type` 數中。 下表概述了不同接受的命名空間限定詞。

| 限定詞 | 定義 |
| --------- | ---------- |
| 標準 | 其中一個標準名稱空間是全域定義的，不會系結至個別組織資料集（例如，電子郵件、電話號碼等）。 提供命名空間ID。 |
| 自訂 | 在組織上下文中建立的唯一名稱空間，而不是在中共用 [!DNL Experience Cloud]。 值代表要搜尋的好記名稱（&quot;name&quot;欄位）。 提供命名空間ID。 |
| integrationCode | 整合代碼——類似「自訂」，但明確定義為要搜尋之資料來源的整合代碼。 提供命名空間ID。 |
| namespaceId | 指出值是透過namespace服務建立或映射之namespace的實際ID。 |
| 未註冊 | 未在namespace服務中定義且採用「原樣」的自由格式字串。 任何處理這些類型名稱空間的應用程式都會針對它們進行檢查，並處理（如果適合公司內容和資料集）。 未提供命名空間ID。 |
| analytics | 在內部映射的自訂命名空間， [!DNL Analytics]而非在namespace服務中。 這會直接依原始請求所指定的方式傳入，但沒有命名空間ID |
| Target | 自訂命名空間由內部瞭解， [!DNL Target]而非在namespace服務中。 這會直接依原始請求所指定的方式傳入，但沒有命名空間ID |

## 接受的產品值

下表概述在工作建立請求的屬性中指定Adobe `include` 產品的接受值。

| 產品 | 用於屬性中的 `include` 值 |
--- | ---
| Adobe Advertising Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;行銷活動&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Adobe Primetime驗證 | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| 客戶記錄服務 | &quot;CRS&quot; |
| 即時客戶個人檔案 | &quot;ProfileService&quot; |