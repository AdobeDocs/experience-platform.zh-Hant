---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service API指南附錄
description: 本檔案包含使用Privacy Service API的其他資訊。
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 9b3fb0d545408369d96a3fc7c5c6e9c098af9933
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 6%

---

# Privacy Service API指南附錄

以下小節包含使用Adobe Experience Platform Privacy Service API的其他資訊。

## 標準身分名稱空間 {#standard-namespaces}

傳送至[!DNL Privacy Service]的所有身分都必須以特定身分名稱空間提供。 身分識別名稱空間是[Adobe Experience Platform Identity Service](../../identity-service/home.md)的元件，指出與身分識別相關的內容。

下表概述[!DNL Experience Platform]提供的幾種常用預先定義的身分型別，以及其相關的`namespace`值：

| 身分識別類型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 電子郵件 | `Email` | `6` |
| 電話 | `Phone` | `7` |
| Adobe Advertising Cloud ID | `AdCloud` | `411` |
| ADOBE AUDIENCE MANAGER UUID | `CORE` | `0` |
| ADOBE EXPERIENCE CLOUD ID | `ECID` | `4` |
| ADOBE TARGET ID | `TNTID` | `9` |
| 廣告商的[!DNL Apple] ID | `IDFA` | `20915` |
| [!DNL Google]廣告ID | `GAID` | `20914` |
| [!DNL Windows]輔助 | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>每個身分型別也有`namespaceId`整數值，當將身分的`namespace`屬性設定為「namespaceId」時，可用來取代`type`字串。 如需詳細資訊，請參閱[名稱空間限定詞](#namespace-qualifiers)的相關章節。

您可以向`idnamespace/identities` API中的[!DNL Identity Service]端點發出GET要求，以擷取貴組織正在使用的身分識別名稱空間清單。 如需詳細資訊，請參閱[Identity Service開發人員指南](../../identity-service/api/getting-started.md)。

## 名稱空間限定詞 {#namespace-qualifiers}

在`namespace` API中指定[!DNL Privacy Service]值時，對應的&#x200B;**引數中必須包含**&#x200B;名稱空間限定詞`type`。 下表概述不同的名稱空間限定詞。

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

## 接受的產品值 {#accepted-product-values}

本節列出建立Privacy Service工作（API或UI）時，`include`屬性中接受的產品識別碼值。 在工作請求的`include`陣列中使用這些值。

下表列出支援的產品、其UI顯示名稱及其對應的程式碼值。

>[!NOTE]
>
>- 產品值不區分大小寫；建議使用駝峰式大小寫來保持一致性。
>- UI和API僅支援上述產品。 如果沒有為您的組織布建產品，則可能會忽略該產品或導致驗證錯誤 — 請參閱您的Adobe合約或布建檔案以確認權益。

| 品牌產品名稱 | UI顯示名稱 | `include` 值 |
| ------------------------------------------------------ | -------------------------- | ---------------------------------------- |
| Adobe Analytics | [!UICONTROL Analytics] | `analytics` |
| Adobe Audience Manager | [!UICONTROL Audience Manager] | `audienceManager` |
| Adobe Advertising | [!UICONTROL Ad Cloud] | `adCloud` |
| Adobe Experience Platform （設定檔存放區） | [!UICONTROL Profile] | `profileService` |
| Adobe Experience Platform （資料湖） | [!UICONTROL AEP Data Lake] | `aepDataLake` |
| Adobe Campaign | [!UICONTROL Campaign] | `campaign` |
| Adobe Target | [!UICONTROL Target] | `target` |
| 客戶屬性 | [!UICONTROL Customer Attributes (CRS)] | `CRS` |
| Adobe Journey Optimizer | [!UICONTROL Adobe Journey Optimizer] | `cjm` |
| Marketo Engage | [!UICONTROL Marketo Engage / AJO B2B] | `marketo` |
| 身分識別服務 | [!UICONTROL Identity] | `identity` |
| Marketo Measure | [!UICONTROL Marketo Measure] | `marketomeasure` |
| Adobe Commerce | [!UICONTROL Commerce (Personalization)] | `commerceMarketingData` |

{style="table-layout:auto"}
