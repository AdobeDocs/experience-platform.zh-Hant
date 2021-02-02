---
keywords: Experience Platform;home；熱門主題
solution: Experience Platform
title: 隱私權服務API開發人員指南附錄
topic: developer guide
description: 本檔案包含使用隱私權服務API的其他資訊。
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 9%

---


# 附錄

以下各節包含使用Adobe Experience Platform Privacy Service API的其他資訊。

## 標準身份名稱空間{#standard-namespaces}

傳送到[!DNL Privacy Service]的所有身份都必須以特定的身份名稱空間提供。 身分名稱空間是[Adobe Experience Platform Identity Service](../../identity-service/home.md)的元件，用以指出身分相關的內容。

下表概述了[!DNL Experience Platform]提供的幾種常用、預先定義的身份類型，以及其關聯的`namespace`值：

| 身分類型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 電子郵件 | 電子郵件 | 6 |
| 電話 | 電話 | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| Adobe Audience Manager UUID | 核心 | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Target ID | TNTID | 9 |
| [!DNL Apple] 廣告商的ID | IDFA | 二零九一五年 |
| [!DNL Google] 廣告 ID | GAID | 二零九一四年 |
| [!DNL Windows] AID | WAID | 8 |

>[!NOTE]
>
>每個身分類型也有一個`namespaceId`整數值，當將身分的`type`屬性設為&quot;namespaceId&quot;時，該整數值可用來取代`namespace`字串。 如需詳細資訊，請參閱[namespace限定詞](#namespace-qualifiers)一節。

您可以向[!DNL Identity Service] API中的`idnamespace/identities`端點發出GET請求，以檢索組織正在使用的身份名稱空間清單。 如需詳細資訊，請參閱[Identity Service開發人員指南](../../identity-service/api/getting-started.md)。

## 命名空間限定詞

在[!DNL Privacy Service] API中指定`namespace`值時，**命名空間限定詞**&#x200B;必須包含在對應的`type`參數中。 下表概述了不同接受的命名空間限定詞。

| 限定詞 | 定義 |
| --------- | ---------- |
| 標準 | 其中一個標準名稱空間是全域定義的，不會系結至個別組織資料集（例如，電子郵件、電話號碼等）。 提供命名空間ID。 |
| 自訂 | 在組織上下文中建立的唯一名稱空間，不在[!DNL Experience Cloud]中共用。 值代表要搜尋的好記名稱（&quot;name&quot;欄位）。 提供命名空間ID。 |
| integrationCode | 整合代碼——類似「自訂」，但明確定義為要搜尋之資料來源的整合代碼。 提供命名空間ID。 |
| namespaceId | 指出值是透過namespace服務建立或映射之namespace的實際ID。 |
| 未註冊 | 未在namespace服務中定義且採用「原樣」的自由格式字串。 任何處理這些類型名稱空間的應用程式都會針對它們進行檢查，並處理（如果適合公司內容和資料集）。 未提供命名空間ID。 |
| analytics | 在[!DNL Analytics]內部映射的自訂命名空間，而不是在namespace服務中。 這會直接依原始請求所指定的方式傳入，但沒有命名空間ID |
| Target | [!DNL Target]在內部可理解的自訂命名空間，而不是在namespace服務中。 這會直接依原始請求所指定的方式傳入，但沒有命名空間ID |

## 接受的產品值

下表概述在工作建立請求的`include`屬性中指定Adobe產品的接受值。

| 產品 | 用於`include`屬性的值 |
--- | ---
| Adobe Advertising Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Adobe Primetime驗證 | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| 客戶記錄服務 | &quot;CRS&quot; |
| 即時客戶個人檔案 | &quot;ProfileService&quot; |