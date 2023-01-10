---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy ServiceAPI指南附錄
description: 本檔案包含使用Privacy ServiceAPI的其他資訊。
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 7%

---

# Privacy ServiceAPI指南附錄

以下小節包含使用Adobe Experience Platform Privacy Service API的其他資訊。

## 標準身分識別命名空間 {#standard-namespaces}

傳送至的所有身分 [!DNL Privacy Service] 必須以特定身分命名空間提供。 身分識別命名空間是 [Adobe Experience Platform Identity Service](../../identity-service/home.md) 指出身分相關的內容。

下表概述了幾種常用的預先定義身分類型，可供 [!DNL Experience Platform]，及其關聯 `namespace` 值：

| 身分類型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 電子郵件 | `Email` | `6` |
| 電話 | `Phone` | `7` |
| Adobe Advertising Cloud ID | `AdCloud` | `411` |
| Adobe Audience Manager UUID | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| Adobe Target ID | `TNTID` | `9` |
| [!DNL Apple] 廣告商的ID | `IDFA` | `20915` |
| [!DNL Google] 廣告 ID | `GAID` | `20914` |
| [!DNL Windows] AID | `WAID` | `8` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>每個身分類型也有 `namespaceId` 整數值，可用來取代 `namespace` 字串 `type` 屬性轉換為「namespaceId」。 請參閱 [命名空間限定符](#namespace-qualifiers) 以取得更多資訊。

您可以向提出GET要求，以擷取組織正在使用的身分命名空間清單 `idnamespace/identities` 端點 [!DNL Identity Service] API。 請參閱 [Identity Service開發人員指南](../../identity-service/api/getting-started.md) 以取得更多資訊。

## 命名空間限定符

指定 `namespace` 值 [!DNL Privacy Service] API, a **命名空間限定符** 必須包含在對應的 `type` 參數。 下表概述了不同接受的命名空間限定符。

| 限定符 | 定義 |
| --------- | ---------- |
| `standard` | 全域定義的其中一個標準命名空間，不會系結至個別組織資料集（例如電子郵件、電話號碼等）。 已提供命名空間ID。 |
| `custom` | 在組織內容中建立、不在 [!DNL Experience Cloud]. 值代表要搜尋的好記名稱（「name」欄位）。 已提供命名空間ID。 |
| `integrationCode` | 整合代碼 — 類似「自訂」，但明確定義為要搜尋之資料來源的整合代碼。 已提供命名空間ID。 |
| `namespaceId` | 指示值是通過命名空間服務建立或映射的命名空間的實際ID。 |
| `unregistered` | 未在命名空間服務中定義且以「原樣」取用的自由字串。 處理這些類型命名空間的任何應用程式都會針對這些應用程式進行檢查，並視情況處理公司內容和資料集。 未提供命名空間ID。 |
| `analytics` | 內部對應的自訂命名空間 [!DNL Analytics]，而不是在命名空間服務中。 這會以原始請求指定的方式直接傳入，沒有命名空間ID |
| `target` | 內部了解的自訂命名空間 [!DNL Target]，而不是在命名空間服務中。 這會以原始請求指定的方式直接傳入，沒有命名空間ID |

{style=&quot;table-layout:auto&quot;}

## 接受的產品值

下表概述了在中指定Adobe產品的接受值 `include` 作業建立請求的屬性。

| 產品 | 在 `include` 屬性 |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform（資料湖） | `aepDataLake` |
| Adobe Experience Platform（即時客戶個人檔案） | `profileService` |
| Adobe Primetime驗證 | `primetimeAuthentication` |
| Adobe Target | `target` |
| 客戶屬性(CRS) | `CRS` |
| 身份識別服務 | `identity` |
| Marketo Engage | `marketo` |

{style=&quot;table-layout:auto&quot;}
