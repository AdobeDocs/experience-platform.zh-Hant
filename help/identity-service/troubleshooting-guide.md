---
keywords: Experience Platform；首頁；熱門主題；身分命名空間；身分命名空間
solution: Experience Platform
title: Identity服務疑難排解指南
description: 本檔案提供Adobe Experience Platform Identity Service常見問題的解答，以及常見錯誤的疑難排解指南。
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '2176'
ht-degree: 0%

---

# Identity Service疑難排解指南

本檔案提供關於Adobe Experience Platform常見問題的解答 [!DNL Identity Service]，以及常見錯誤的疑難排解指南。 若有下列問題和疑難排解： [!DNL Platform] 一般而言，請參閱 [Adobe Experience Platform API疑難排解指南](../landing/troubleshooting.md).

識別單一客戶的資料通常會分散在客戶與您的品牌互動所使用的各種裝置和系統中。 [!DNL Identity Service] 會將這些分散的身分資料收集在一起，協助您全面了解客戶行為，以便您即時提供具影響力的數位體驗。 如需詳細資訊，請參閱 [Identity服務概述](./home.md).

## 常見問題集

以下是關於 [!DNL Identity Service].

## 什麼是身分資料？

身分資料是可用來識別個別人員的任何資料。 根據您組織內使用資料的方式，身分資料可以包含CRM系統的使用者名稱、電子郵件地址和ID。 身分資料不限於您網站或服務的註冊使用者，因為匿名使用者也可透過其裝置或Cookie ID來識別。

## 將資料欄位標示為身分有何好處？

將某些資料欄位標示為記錄和時間系列資料中的身分，可讓您在資料的自然結構中對應身分關係，並跨管道調解重複資料。 請參閱 [Identity服務概述](./home.md) 以取得更多資訊。

## 什麼是已知和匿名身分？

已知身分是指可單獨使用，或搭配其他資訊使用，以識別、聯絡或尋找個別人員的身分值。 已知身分識別的範例可能包括電子郵件地址、電話號碼及CRM ID。

匿名身分是指無法單獨使用或搭配其他資訊使用，以識別、聯絡或尋找個別人員（例如Cookie ID）的身分值。

## 什麼是私人身分圖？

「私人身分圖」是已連結身分與已連結身分之間關係的私人地圖，只會顯示給您的組織。

從串流端點擷取的任何資料中，若包含多個身分，或傳送至已啟用 [!DNL Identity Service]，則這些身分會在「私人身分圖表」中連結。 [!DNL Identity Service] 可運用此圖表來蒐集指定消費者或實體的身分，以便進行身分拼接和設定檔合併。

## 如何在XDM架構中建立多個身分欄位？

[Experience Data Model(XDM)](../xdm/home.md) 結構支援多個身分欄位。 任何類型的資料欄位 `string` 在實作XDM個別設定檔或XDM ExperienceEvent類別的架構中，可以標示為身分欄位。 標示後，這些欄位中包含的任何資料都會新增至設定檔的身分對應。

如需如何使用使用者介面將XDM欄位標示為身分欄位的步驟，請參閱 [身分區段](../xdm/tutorials/create-schema-ui.md) 在結構編輯器教學課程中。 如果您使用API，請參閱 [標識描述符節](../xdm/tutorials/create-schema-api.md) （位於Schema Registry API教學課程中）。

## 是否有些欄位不應標示為身分的內容？

應為每個個人專屬的值保留身分欄位。 例如，將資料集視為客戶忠誠度計畫。 「忠誠度」欄位（金、銀、銅）不會是有用的身分欄位，而忠誠度ID（唯一值）則會是。

郵遞區號和IP位址等欄位不應標示為個人的身分，因為這些值可套用至多個個人。 這些類型的欄位只應標示為家庭層級行銷策略的身分。

## 為什麼我的身分欄位無法連結我預期的方式？

使用 [`/cluster/members` 端點](./api/list-cluster-identites.md) 在身分識別服務API中，您可以檢視一或多個身分欄位的相關身分識別。 如果回應未傳回您預期的連結身分，請務必在XDM資料中提供適當的身分資訊。 請參閱 [提供XDM資料至Identity Service](./home.md) （位於Identity Service概述中），以了解詳細資訊。

## 什麼是身分命名空間？

身分命名空間提供身分欄位與客戶身分相關的內容。 例如，「電子郵件」命名空間下的身分欄位應符合標準電子郵件格式(名稱<span>@emailprovider.com)，而使用「電話」命名空間的欄位則應符合標準電話號碼(例如北美的987-555-1234)。

命名空間可區分不同CRM系統之間的類似身分值。 例如，假設設定檔包含與公司獎勵計畫相關聯的數值忠誠度ID。 「忠誠度」的命名空間會將此值與您電子商務系統的類似數值ID（也顯示在相同的設定檔中）區隔開。

請參閱 [身分命名空間概述](./home.md) 以取得更多資訊。

## 如何將身分識別與身分命名空間建立關聯？

身分欄位建立時，必須與現有的身分命名空間相關聯。 任何新的命名空間必須 [使用API建立](#how-do-i-create-a-custom-namespace-for-my-organization) 將其與身分欄位關聯之前。

有關在使用API建立身份描述符時定義命名空間的逐步說明，請參閱 [建立描述符](../xdm/tutorials/create-schema-ui.md) （在Schema Registry開發人員指南中）。 若要在UI中將結構欄位標示為身分，請遵循 [結構編輯器教學課程](../xdm/tutorials/create-schema-api.md).

## Experience Platform提供的標準身分命名空間為何？ {#standard-namespaces}

標準身分識別命名空間是所有組織皆可使用的命名空間。 請參閱 [身分識別命名空間概觀](./namespaces.md) ，取得可用標準命名空間的完整清單。

## 我可以在哪裡找到組織可用的身分識別命名空間清單？

使用 [Identity服務API](https://www.adobe.io/experience-platform-apis/references/identity-service)，您可以向發出GET要求，以列出組織的所有可用身分命名空間 `/idnamespace/identities` 端點。 請參閱 [清單可用命名空間](./api/list-namespaces.md) （位於身分識別服務API概觀中）以取得詳細資訊。

## 如何為組織建立自訂命名空間？

使用 [Identity服務API](https://www.adobe.io/experience-platform-apis/references/identity-service)，您可以向您的組織提出POST要求，以建立自訂身分命名空間 `/idnamespace/identities` 端點。 請參閱 [建立自訂命名空間](./api/create-custom-namespace.md) （位於身分識別服務API概觀中）以取得詳細資訊。

## 什麼是複合身份和XID?

身分識別在API呼叫中會透過其複合身分識別或XID參考。 複合身分代表包含ID值和命名空間的身分。 XID是單值識別碼，代表與複合身分識別（ID和命名空間）相同的建構，且會在Identity Service保存時自動指派給新身分識別。 請參閱 [Identity服務API概述](./home.md) 以取得更多資訊。

## Identity Service如何處理個人識別資訊(PII)?

Identity Service具有標準的命名空間，可支援擷取電話號碼及電子郵件的雜湊身分值。 不過，您應負責值的雜湊處理。 若要進一步了解擷取至Platform的雜湊資料，請參閱 [[!DNL Data Prep] 映射函式指南](../data-prep/functions.md#hashing).

## 雜湊PII型身分識別時是否有任何考量？

如果您要將雜湊PII值傳送至Identity Service，必須在資料集中使用相同的加密方法。 這可確保資料集中的相同身分值會產生相同的雜湊值，且能在身分圖表中正確比對及連結。

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

## 為何無法存取身分圖表頁面或API?

您的平台管理員必須透過 `view-identity-graph` 權限來檢視身分圖資料。 若沒有此權限，您會在身分圖表檢視器頁面和呼叫平台API時收到拒絕的權限訊息。 請參閱 [訪問控制概述](../access-control/home.md) 以取得權限的詳細資訊。

## 疑難排解

下節提供特定錯誤碼和使用時可能遇到的意外行為的疑難排解建議 [!DNL Identity Service] API。

## [!DNL Identity Service] 錯誤訊息

以下是使用 [!DNL Identity Service] API。

### 缺少必需的查詢參數

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

當要求路徑中未包含必要的查詢參數時，就會顯示此錯誤。 此 `detail` 錯誤訊息的名稱會提供遺失參數的名稱。 此錯誤訊息的變數包括：

- 缺少必需的查詢參數 — nsId
- 缺少必需的查詢參數 — id
- 缺少必需的查詢參數 — xid或(nsid,id)
- 缺少必需的查詢參數 — targetNs
- 缺少必需的查詢參數 — xids或compositeXids

再次嘗試之前，請先檢查您是否已在請求路徑中正確加入指示的參數。

### 時間戳記應為最近180天內

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] 清除180天以前的資料。 當您嘗試存取早於此版本的資料時，會顯示此錯誤訊息。

### 單一呼叫中有1000個XID的限制

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

當您嘗試檢索身份資訊的次數超過 [XID](#what-are-composite-identities-and-xids) 允許在單一API呼叫中使用。 將請求中的XID數量減少至顯示限制以解決此問題。


### 單個呼叫中有1000個compositeXid的限制

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

當您嘗試檢索身份資訊的次數超過 [複合身份](#what-are-composite-identities-and-xids) 允許在單一API呼叫中使用。 將請求中的複合身分識別數量減少至所顯示限制以下，以解決此問題。

### 指定的圖形類型無效

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

當 `graph-type` 查詢參數在請求路徑中的值無效。 請參閱 [身分圖](./home.md) 在 [!DNL Identity Service] 概觀，了解支援哪些圖形類型。

### 服務令牌沒有有效範圍

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

若您的組織尚未布建適當的權限，則會顯示此錯誤訊息 [!DNL Identity Service]. 請連絡您的系統管理員以解決此問題。

### 網關服務令牌無效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

如果發生此錯誤，您的存取權杖無效。 存取權杖每24小時過期一次，必須重新產生才能繼續使用 [!DNL Platform] API。 請參閱 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以取得產生新存取權杖的相關指示。

### 授權服務令牌無效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

如果發生此錯誤，您的存取權杖無效。 存取權杖每24小時過期一次，必須重新產生才能繼續使用 [!DNL Platform] API。 請參閱 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以取得產生新存取權杖的相關指示。

### 用戶令牌沒有有效的產品上下文

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

未從 [!DNL Experience Platform] 整合。 請參閱 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 有關為 [!DNL Experience Platform] 整合。

### 從身分和命名空間程式碼取得原生XID時發生內部錯誤

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

當 [!DNL Identity Service] 只要保存身份，就會為標識的ID和關聯的命名空間ID分配一個稱為XID的唯一標識符。 當在尋找指定ID值和命名空間的XID過程中發生錯誤時，會顯示此訊息。

### 未針對布建IMS組織 [!DNL Identity Service] 使用狀況

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

若您的組織尚未布建適當的權限，則會顯示此錯誤訊息 [!DNL Identity Service]. 請連絡您的系統管理員以解決此問題。

### 內部伺服器錯誤

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

執行 [!DNL Platform] 服務呼叫。 最佳實務是讓自動呼叫在收到此錯誤時，以計時間隔重試其請求幾次。 如果問題仍然存在，請與系統管理員聯繫。

## 批次擷取錯誤碼

[!DNL Identity Service] 從記錄和上傳到的時間序列資料中嵌入身份資料 [!DNL Platform] 使用批次內嵌。 由於批次內嵌是非同步流程，因此您必須檢視批次的詳細資訊才能檢視錯誤。 錯誤會隨著批次進行而累積，直到批次完成為止。

以下是與 [!DNL Identity Service] 使用 [批次內嵌API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).

### 未知XDM架構

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] 僅會針對符合的記錄或時間序列資料取用身分 [!DNL Profile] 或 [!DNL ExperienceEvent] 類別。 嘗試為內嵌資料 [!DNL Identity Service] 不符合任一類別的URL將觸發此錯誤。

### 處理批次的前100列中有0個有效身分

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

當批次的前100列未顯示身分時，即會顯示此錯誤。 但是，此錯誤並未明確指出在後續記錄中找不到任何身分。

### 已略過記錄，因為每個XDM記錄只有1個身分

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] 只有在單一記錄顯示兩個或多個身分值時，才會連結身分。 此錯誤訊息會針對每個擷取的批次發出一次，並顯示只能找到一個身分的記錄數，且導致身分圖表未變更。

### 未為此IMS組織註冊命名空間代碼

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

擷取的記錄呈現的身分不存在或您的組織無法存取其相關命名空間時，就會顯示此錯誤。

### 由於未針對私人身分圖布建IMS組織，因此略過批次內嵌

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

擷取批次資料時，當貴組織尚未布建適當的權限， [!DNL Identity Service]. 請連絡您的系統管理員以解決此問題。

### 內部錯誤

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

批次擷取期間發生非預期的例外時，就會顯示此錯誤。 最佳實務是讓自動呼叫在收到此錯誤時，以計時間隔重試其請求幾次。 如果問題仍然存在，請與系統管理員聯繫。
