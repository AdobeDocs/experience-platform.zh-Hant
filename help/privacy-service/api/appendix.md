---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy ServiceAPI指南附錄
topic-legacy: developer guide
description: 本檔案包含使用Privacy ServiceAPI的其他資訊。
exl-id: 7099e002-b802-486e-8863-0630d66e330f
translation-type: tm+mt
source-git-commit: e226990fc84926587308077b32b128bfe334e812
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Privacy ServiceAPI指南附錄

以下各節包含使用Adobe Experience Platform Privacy ServiceAPI的其他資訊。

## 標準身份名稱空間{#standard-namespaces}

傳送到[!DNL Privacy Service]的所有身份都必須以特定的身份名稱空間提供。 身分名稱空間是[Adobe Experience Platform身份服務](../../identity-service/home.md)的一個元件，用於指示與身份相關的上下文。

下表概述了[!DNL Experience Platform]提供的幾種常用、預先定義的身份類型，以及其關聯的`namespace`值：

| 身分類型 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 電子郵件 | `Email` | `6` |
| 電話 | `Phone` | `7` |
| Adobe Advertising CloudID | `AdCloud` | `411` |
| Adobe Audience ManagerUUID | `CORE` | `0` |
| Adobe Experience CloudID | `ECID` | `4` |
| Adobe TargetID | `TNTID` | `9` |
| [!DNL Apple] 廣告商的ID | `IDFA` | `20915` |
| [!DNL Google] 廣告 ID | `GAID` | `20914` |
| [!DNL Windows] AID | `WAID` | `8` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>每個身分類型也有一個`namespaceId`整數值，當將身分的`type`屬性設為&quot;namespaceId&quot;時，該整數值可用來取代`namespace`字串。 如需詳細資訊，請參閱[namespace限定詞](#namespace-qualifiers)一節。

您可以通過向[!DNL Identity Service] API中的`idnamespace/identities`端點發出GET請求，檢索組織正在使用的標識名稱空間清單。 如需詳細資訊，請參閱[Identity Service開發人員指南](../../identity-service/api/getting-started.md)。

## 命名空間限定詞

在[!DNL Privacy Service] API中指定`namespace`值時，**命名空間限定詞**&#x200B;必須包含在對應的`type`參數中。 下表概述了不同接受的命名空間限定詞。

| 限定詞 | 定義 |
| --------- | ---------- |
| `standard` | 其中一個標準名稱空間是全域定義的，不會系結至個別組織資料集（例如，電子郵件、電話號碼等）。 提供命名空間ID。 |
| `custom` | 在組織上下文中建立的唯一名稱空間，不在[!DNL Experience Cloud]中共用。 值代表要搜尋的好記名稱（&quot;name&quot;欄位）。 提供命名空間ID。 |
| `integrationCode` | 整合代碼——類似「自訂」，但明確定義為要搜尋之資料來源的整合代碼。 提供命名空間ID。 |
| `namespaceId` | 指出值是透過namespace服務建立或映射之namespace的實際ID。 |
| `unregistered` | 未在namespace服務中定義且採用「原樣」的自由格式字串。 任何處理這些類型名稱空間的應用程式都會針對它們進行檢查，並處理（如果適合公司內容和資料集）。 未提供命名空間ID。 |
| `analytics` | 在[!DNL Analytics]內部映射的自訂命名空間，而不是在namespace服務中。 這會直接依原始請求所指定的方式傳入，但沒有命名空間ID |
| `target` | [!DNL Target]在內部可理解的自訂命名空間，而不是在namespace服務中。 這會直接依原始請求所指定的方式傳入，但沒有命名空間ID |

{style=&quot;table-layout:auto&quot;}

## 接受的產品值

下表概述了在作業建立請求的`include`屬性中指定Adobe產品的接受值。

| 產品 | 用於`include`屬性的值 |
| --- | --- |
| Adobe Advertising Cloud | `AdCloud` |
| Adobe Analytics | `Analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `Campaign` |
| Adobe Experience Platform | `aepDataLake` |
| Adobe Primetime認證 | `primetimeAuthentication` |
| Adobe Target | `Target` |
| 客戶記錄服務 | `CRS` |
| 即時客戶個人檔案 | `ProfileService` |

{style=&quot;table-layout:auto&quot;}