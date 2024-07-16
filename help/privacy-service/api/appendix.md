---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service API指南附錄
description: 本檔案包含使用Privacy Service API的其他資訊。
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 644e85fe5c9b1a37f69c75755713e929736c2e89
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 5%

---

# Privacy Service API指南附錄

以下小節包含使用Adobe Experience Platform Privacy Service API的其他資訊。

## 標準身分名稱空間 {#standard-namespaces}

傳送至[!DNL Privacy Service]的所有身分都必須以特定身分名稱空間提供。 身分識別名稱空間是[Adobe Experience Platform Identity Service](../../identity-service/home.md)的元件，指出與身分識別相關的內容。

下表概述[!DNL Experience Platform]提供的幾種常用預先定義的身分型別，以及其相關的`namespace`值：

| 身分類型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 電子郵件 | `Email` | `6` |
| 電話 | `Phone` | `7` |
| ADOBE ADVERTISING CLOUD ID | `AdCloud` | `411` |
| ADOBE AUDIENCE MANAGER UUID | `CORE` | `0` |
| ADOBE EXPERIENCE CLOUD ID | `ECID` | `4` |
| ADOBE TARGET ID | `TNTID` | `9` |
| 廣告商的[!DNL Apple] ID | `IDFA` | `20915` |
| [!DNL Google]廣告ID | `GAID` | `20914` |
| [!DNL Windows]輔助 | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>每個身分型別也有`namespaceId`整數值，當將身分的`type`屬性設定為「namespaceId」時，可用來取代`namespace`字串。 如需詳細資訊，請參閱[名稱空間限定詞](#namespace-qualifiers)的相關章節。

您可以向[!DNL Identity Service] API中的`idnamespace/identities`端點發出GET要求，以擷取貴組織正在使用的身分識別名稱空間清單。 如需詳細資訊，請參閱[Identity Service開發人員指南](../../identity-service/api/getting-started.md)。

## 名稱空間限定詞

在[!DNL Privacy Service] API中指定`namespace`值時，對應的`type`引數中必須包含&#x200B;**名稱空間限定詞**。 下表概述不同的名稱空間限定詞。

| 限定詞 | 定義 |
| --------- | ---------- |
| `standard` | 全域定義的標準名稱空間之一，不會繫結至個別組織資料集（例如電子郵件、電話號碼等）。 已提供名稱空間ID。 |
| `custom` | 在組織內容中建立的唯一名稱空間，未在[!DNL Experience Cloud]之間共用。 值代表要搜尋的易記名稱（「名稱」欄位）。 已提供名稱空間ID。 |
| `integrationCode` | 整合程式碼 — 類似「自訂」，但特別定義為要搜尋之資料來源的整合程式碼。 已提供名稱空間ID。 |
| `namespaceId` | 表示該值是通過名稱空間服務建立或對應的名稱空間的實際ID。 |
| `unregistered` | 名稱空間服務中未定義的自由格式字串，採用「原樣」處理。 任何可處理這些型別名稱空間的應用程式會根據此類名稱空間進行檢查，並在適合公司內容與資料集時進行處理。 未提供名稱空間ID。 |
| `analytics` | 在[!DNL Analytics]內部對應，而不是在名稱空間服務中的自訂名稱空間。 這會依照原始請求的指定直接傳入，不含名稱空間ID |
| `target` | [!DNL Target]內部可理解的自訂名稱空間，而非名稱空間服務中的自訂名稱空間。 這會依照原始請求的指定直接傳入，不含名稱空間ID |

{style="table-layout:auto"}

## 接受的產品值

下表概述在工作建立請求的`include`屬性中指定Adobe產品時可接受的值。

>[!NOTE]
>
>產品清單的值不區分大小寫。 建議使用駝峰式大小寫，但並未強制執行。

| 產品 | 用於`include`屬性的值 |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `audienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform （資料湖） | `aepDataLake` |
| Adobe Experience Platform （即時客戶個人檔案） | `profileService` |
| Adobe Pass 驗證 | `primetimeAuthentication` |
| Adobe Target | `target` |
| 客戶屬性(CRS) | `CRS` |
| 客戶歷程管理 | `cjm` |
| 身分識別服務 | `identity` |
| Marketo Engage | `marketo` |
| Marketo Measure | `marketomeasure` |

{style="table-layout:auto"}
