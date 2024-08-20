---
keywords: Experience Platform；首頁；熱門主題；身分名稱空間；身分名稱空間
solution: Experience Platform
title: Identity Service疑難排解指南
description: 本檔案提供有關Adobe Experience Platform Identity Service常見問題的解答，以及常見錯誤的疑難排解指南。
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '2165'
ht-degree: 0%

---

# Identity Service疑難排解指南

本檔案提供有關Adobe Experience Platform [!DNL Identity Service]常見問題的解答，以及常見錯誤的疑難排解指南。 如需[!DNL Platform] API的一般問題和疑難排解，請參閱[Adobe Experience Platform API疑難排解指南](../landing/troubleshooting.md)。

用來識別單一客戶的資料，通常分散於客戶用來與您的品牌互動的各種裝置和系統中。 [!DNL Identity Service]將這些分散的身分識別集合在一起，有助於全面瞭解客戶行為，以便您即時提供具影響力的數位體驗。 如需詳細資訊，請參閱[Identity Service概觀](./home.md)。

## 常見問題集

以下為關於[!DNL Identity Service]常見問題的解答清單。

## 什麼是身分資料？

身分資料是可用於識別個人身分的任何資料。 根據組織內使用資料的方式，身分資料可以包含來自CRM系統的使用者名稱、電子郵件地址和ID。 身分資料不限於您網站或服務的註冊使用者，因為匿名使用者也可以透過其裝置或Cookie ID識別。

## 將資料欄位標示為身分有什麼好處？

將特定資料欄位標示為記錄和時間序列資料中的身分，可讓您在資料的自然結構中對應身分關係，並在跨管道協調重複資料。 如需詳細資訊，請參閱[Identity Service概觀](./home.md)。

## 什麼是已知和匿名的身分？

已知身分是指可單獨使用或搭配其他資訊使用來識別、聯絡或尋找個人身分的值。 已知的身分範例可能包括電子郵件地址、電話號碼和CRMID。

匿名身分是指無法單獨使用或搭配其他資訊使用來識別、聯絡或尋找個人身分的值（例如Cookie ID）。

## 什麼是私人身分圖表？

私人身分圖表是拼接和連結的身分之間關係的私人對應，僅對您的組織可見。

當從串流端點擷取的任何資料中包含一個以上的身分或傳送到為[!DNL Identity Service]啟用的資料集時，這些身分會在私人身分圖表中進行連結。 [!DNL Identity Service]會利用此圖表來取得特定消費者或實體的身分，以允許身分拼接和設定檔合併。

## 如何在XDM結構描述中建立多個身分欄位？

[體驗資料模型(XDM)](../xdm/home.md)結構描述支援多個身分欄位。 在實作XDM Individual Profile或XDM ExperienceEvent類別的結構描述中，型別`string`的任何資料欄位都可標示為身分欄位。 在標籤之後，這些欄位中包含的任何資料都會新增到設定檔的身分對應中。

有關如何使用使用者介面將XDM欄位標示為身分欄位的步驟，請參閱結構描述編輯器教學課程中的[身分割槽段](../xdm/tutorials/create-schema-ui.md)。 如果您使用API，請參閱Schema Registry API教學課程中的[身分描述項區段](../xdm/tutorials/create-schema-api.md)。

## 是否有某些欄位不應標示為身分的上下文？

身分欄位應該保留給每個人的唯一值。 例如，考慮客戶忠誠度計畫的資料集。 「忠誠度」欄位（金級、銀級、銅級）並非有效的身分欄位，而「忠誠度ID」（唯一值）則為。

郵遞區號和IP位址等欄位不應標籤為個人的身分，因為這些值可套用至多個個人。 這些型別的欄位應該僅標籤為家庭層級行銷策略的身分。

## 為什麼我的身分欄位沒有依照我預期的方式連結？

使用身分服務API中的[`/cluster/members`端點](./api/list-cluster-identites.md)，您可以檢視一或多個身分欄位的關聯身分。 如果回應未傳回您預期的連結身分，請確定您在XDM資料中提供適當的身分資訊。 如需詳細資訊，請參閱Identity Service概觀中有關[將XDM資料提供給Identity Service](./home.md)的章節。

## 什麼是身分名稱空間？

身分名稱空間會提供身分欄位如何與客戶身分相關的內容。 例如，「電子郵件」名稱空間下的身分欄位應符合標準電子郵件格式(名稱<span>@emailprovider.com)，而使用「電話」名稱空間的欄位應符合標準電話號碼（例如北美的987-555-1234）。

名稱空間會區分不同CRM系統之間的類似身分值。 例如，假設某個設定檔包含與公司獎勵方案相關聯的數值「忠誠度ID」。 「忠誠度」名稱空間會將此值與也出現在相同設定檔中的電子商務系統的類似數值ID分開。

如需詳細資訊，請參閱[身分名稱空間概觀](./home.md)。

## 如何將身分與身分名稱空間建立關聯？

身分欄位建立時，必須與現有的身分名稱空間相關聯。 任何新名稱空間都必須使用API](#how-do-i-create-a-custom-namespace-for-my-organization)建立[，才能與身分欄位建立關聯。

如需在使用API建立身分描述項時定義名稱空間的逐步指示，請參閱Schema Registry開發人員指南中[建立描述項](../xdm/tutorials/create-schema-ui.md)的相關章節。 若要在UI中將結構描述欄位標示為身分，請依照[結構描述編輯器教學課程](../xdm/tutorials/create-schema-api.md)中的步驟操作。

## Experience Platform提供哪些標準身分名稱空間？ {#standard-namespaces}

標準身分名稱空間是可供所有組織使用的名稱空間。 如需可用標準名稱空間的完整清單，請參閱[身分識別名稱空間概觀](./features/namespaces.md)。

## 我可以在哪裡找到我的組織可用的身分識別名稱空間清單？

使用[身分識別服務API](https://www.adobe.io/experience-platform-apis/references/identity-service)，您可以透過向`/idnamespace/identities`端點發出GET要求，列出您組織的所有可用身分識別名稱空間。 如需詳細資訊，請參閱Identity Service API概觀中[列出可用名稱空間](./api/list-namespaces.md)一節。

## 如何為我的組織建立自訂名稱空間？

您可以使用[身分識別服務API](https://www.adobe.io/experience-platform-apis/references/identity-service)，透過向`/idnamespace/identities`端點發出POST要求，為您的組織建立自訂身分識別名稱空間。 如需詳細資訊，請參閱Identity Service API概觀中有關[建立自訂名稱空間](./api/create-custom-namespace.md)的章節。

## 什麼是複合身分和XID？

在API呼叫中，身分會由其複合身分或XID參照。 複合身分是包含ID值和名稱空間的身分的表示法。 XID是單值識別碼，代表與複合身分相同的結構（ID和名稱空間），當身分服務持續存在時，會自動指派給新身分。 如需詳細資訊，請參閱[身分識別服務API總覽](./home.md)。

## Identity Service如何處理個人識別資訊(PII)？

Identity Service具有標準名稱空間，可支援擷取電話號碼和電子郵件的雜湊身分值。 不過，您應負責值的雜湊處理。 若要深入瞭解擷取到Platform的雜湊資料，請參閱[[!DNL Data Prep] 對應函式指南](../data-prep/functions.md#hashing)。

## 雜湊處理PII型身分時，是否有任何考量事項？

如果您將雜湊PII值傳送至Identity Service，您必須在資料集中使用相同的加密方法。 這可確保跨資料集的相同身分值會產生相同的雜湊值，並能夠在身分圖表中正確比對和連結。

<!-- Documentation does not show any methods of editing the identityMap directly, and this table never overtly recommends using identityMap anyway. This should probably be removed unless PM thinks otherwise. -->
<!-- ## When should I use the Identity map rather than labeling individual XDM schema fields?

The following table describes when the recommended approach for including identity data in your XDM would be identity map and when an identity field is the better method.

>[!NOTE]
>
>An advantage `identityMap` has is the ability to include multiple identity values for a single namespace.

Write|XDM identity field|`identityMap`
---|---|---
UI|Supported|Supported
Developer|Recommended|Supported
ETL|Recommended|Avoid - While this is supported, data should be formatted naturally when using an ETL, favoring identity fields over `identityMap`.
Internal solutions|Preferred|Common

--- -->

## 為何無法存取身分圖表頁面或API？

您的Platform管理員必須布建您具有`view-identity-graph`許可權，您才能檢視身分圖表資料。 若沒有此許可權，您將在身分圖表檢視器頁面上及呼叫Platform API時，收到許可權遭拒訊息。 如需許可權的詳細資訊，請參閱[存取控制概述](../access-control/home.md)。

## 疑難排解

下節針對您在使用[!DNL Identity Service] API時可能會遇到的特定錯誤碼和意外行為，提供疑難排解建議。

## [!DNL Identity Service]則錯誤訊息

以下是您在使用[!DNL Identity Service] API時可能會遇到的錯誤訊息清單。

### 缺少必要的查詢引數

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

當要求的查詢引數未包含在要求路徑中時，便會顯示此錯誤。 錯誤訊息的`detail`提供遺失引數的名稱。 此錯誤訊息的變化包括：

- 缺少必要的查詢引數 — nsId
- 缺少必要的查詢引數 — id
- 缺少必要的查詢引數 — xid或(nsid，id)
- 缺少必要的查詢引數 — targetNs
- 缺少必要的查詢引數 — xids或compositeXids

在重試之前，請檢查您在請求路徑中是否正確包含指示的引數。

### 時間戳記應在過去180天內

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service]會清除超過180天的資料。 當您嘗試存取超過此的資料時，此錯誤訊息便會顯示。

### 單一呼叫中有1000個XID的限制

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

當您嘗試擷取超過單一API呼叫中允許的[XID](#what-are-composite-identities-and-xids)最大數目的身分資訊時，會顯示此錯誤訊息。 將請求中的XID數量減少至顯示限制以下，即可解決此問題。


### 單一呼叫中有1000個compositeXid的限制

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

當您嘗試擷取超過單一API呼叫中允許的[複合身分](#what-are-composite-identities-and-xids)最大數目的身分資訊時，會顯示此錯誤訊息。 將請求中的複合身分數量減少到顯示限制以下，即可解決此問題。

### 指定的圖表型別無效

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

當請求路徑中為`graph-type`查詢引數指定無效值時，會顯示此錯誤訊息。 請參閱[!DNL Identity Service]總覽中有關[身分圖表](./home.md)的章節，以瞭解支援的圖表型別。

### 服務權杖沒有有效的範圍

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

當您的組織尚未布建適當的[!DNL Identity Service]許可權時，便會顯示此錯誤訊息。 請連絡您的系統管理員以解決此問題。

### 閘道服務權杖無效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

發生此錯誤時，您的存取權杖無效。 存取權杖每24小時過期一次，必須重新產生才能繼續使用[!DNL Platform] API。 請參閱[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，瞭解產生新存取權杖的說明。

### 授權服務權杖無效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

發生此錯誤時，您的存取權杖無效。 存取權杖每24小時過期一次，必須重新產生才能繼續使用[!DNL Platform] API。 請參閱[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，瞭解產生新存取權杖的說明。

### 使用者權杖並沒有有效的產品內容

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

當您的存取權杖尚未從[!DNL Experience Platform]整合產生時，此錯誤訊息便會顯示。 請參閱[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，瞭解如何產生[!DNL Experience Platform]整合的新存取權杖說明。

### 從身分和名稱空間程式碼取得原生XID時發生內部錯誤

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

當[!DNL Identity Service]儲存身分時，身分識別碼和關聯的名稱空間識別碼會指派一個稱為XID的唯一識別碼。 在尋找指定ID值和名稱空間的XID過程中發生錯誤時，會顯示此訊息。

### 未針對[!DNL Identity Service]使用情況布建IMS組織

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

當您的組織尚未布建適當的[!DNL Identity Service]許可權時，便會顯示此錯誤訊息。 請連絡您的系統管理員以解決此問題。

### 內部伺服器錯誤

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

執行[!DNL Platform]服務呼叫時發生未預期的例外狀況時，便會顯示此錯誤。 最佳實務是在收到此錯誤時，以固定的間隔設定程式來重試自動呼叫的請求。 如果問題仍然存在，請聯絡您的系統管理員。

## 批次擷取錯誤代碼

[!DNL Identity Service]會使用批次擷取，從已上傳至[!DNL Platform]的記錄和時間序列資料中擷取身分資料。 由於批次擷取為非同步流程，因此您必須檢視批次的詳細資料才能檢視錯誤。 錯誤會隨著批次進行而累積，直到批次完成。

以下是使用[批次擷取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)時，您可能會遇到的與[!DNL Identity Service]相關的錯誤訊息清單。

### 未知的XDM結構描述

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service]只會使用分別符合[!DNL Profile]或[!DNL ExperienceEvent]類別的記錄或時間序列資料的身分。 嘗試擷取不符合任一類別的[!DNL Identity Service]資料將觸發此錯誤。

### 已處理批次的前100列中有0個有效身分

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

當批次的前100列未顯示任何身分時，會顯示此錯誤。 不過，此錯誤並未明確表示在後續記錄中找不到身分。

### 已略過記錄，因為每個XDM記錄只有1個身分

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service]只會在單一記錄呈現兩個或多個身分值時連結身分。 此錯誤訊息會針對每個擷取的批次出現一次，並顯示僅能找到一個身分且不會導致身分圖表發生任何變更的記錄數量。

### 此IMS組織未註冊名稱空間程式碼

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

當內嵌的記錄呈現的身分識別相關聯名稱空間不存在或您的組織無法存取時，便會顯示此錯誤。

### 正在跳過批次內嵌，因為未針對私人身分圖表布建IMS組織

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

擷取批次資料時，如果您的組織尚未布建適當的[!DNL Identity Service]許可權，則會顯示此錯誤訊息。 請連絡您的系統管理員以解決此問題。

### 內部錯誤

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

批次擷取期間發生非預期的例外狀況時，便會顯示此錯誤。 最佳實務是在收到此錯誤時，以固定的間隔設定程式來重試自動呼叫的請求。 如果問題仍然存在，請聯絡您的系統管理員。
