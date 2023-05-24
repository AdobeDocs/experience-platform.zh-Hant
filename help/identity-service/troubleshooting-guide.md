---
keywords: Experience Platform；首頁；熱門主題；標識名稱空間；標識名稱空間
solution: Experience Platform
title: Identity Service故障排除指南
description: 本文檔提供有關Adobe Experience Platform身份服務的常見問題解答以及常見錯誤的故障排除指南。
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '2176'
ht-degree: 0%

---

# Identity Service故障排除指南

本文檔提供有關Adobe Experience Platform的常見問題解答 [!DNL Identity Service]以及常見錯誤的故障排除指南。 有關 [!DNL Platform] API一般，請參見 [Adobe Experience PlatformAPI故障排除指南](../landing/troubleshooting.md)。

標識單個客戶的資料通常分散於他們用於與您的品牌接洽的各種設備和系統。 [!DNL Identity Service] 將這些分散的身份資訊匯集到一起，以便全面瞭解客戶行為，以便您能夠即時提供有影響的數字型驗。 有關詳細資訊，請參見 [Identity Service概述](./home.md)。

## 常見問題集

以下是有關 [!DNL Identity Service]。

## 什麼是身份資料？

身份資料是可用於標識個人的任何資料。 根據組織內使用資料的上下文，身份資料可以包括CRM系統中的用戶名、電子郵件地址和ID。 身份資料不限於您的網站或服務的註冊用戶，因為匿名用戶也可以通過其設備或cookie ID來標識。

## 將資料欄位標籤為標識有何好處？

將某些資料欄位標籤為記錄和時間序列資料中的標識，使您能夠在資料的自然結構中映射標識關係，並協調跨通道的重複資料。 查看 [Identity Service概述](./home.md) 的子菜單。

## 已知和匿名身份是什麼？

已知標識是指可以單獨使用或與其他資訊一起使用的標識值，以識別、聯繫或查找個人。 已知身份的示例可能包括電子郵件地址、電話號碼和CRM ID。

匿名身份是指不能單獨使用或與其他資訊一起使用以識別、聯繫或查找個人（如cookie ID）的身份值。

## 什麼是私有身份圖？

專用標識圖是縫合標識和連結標識之間關係的專用映射，僅對您的組織可見。

當從流端點接收的任何資料中包含多個標識或將其發送到啟用 [!DNL Identity Service]，這些身份在私有身份圖中連結。 [!DNL Identity Service] 利用此圖表為給定的使用者或實體收集標識，從而允許標識拼接和配置檔案合併。

## 如何在XDM架構中建立多個標識欄位？

[體驗資料模型(XDM)](../xdm/home.md) 架構支援多個標識欄位。 任何類型的資料欄位 `string` 在實現XDM Individual Profile或XDM ExperienceEvent類的架構中，可以將其標籤為標識欄位。 標籤後，這些欄位中包含的任何資料都會添加到配置檔案的標識映射中。

有關如何使用用戶介面將XDM欄位標籤為標識欄位的步驟，請參見 [標識部分](../xdm/tutorials/create-schema-ui.md) 在架構編輯器教程中。 如果使用API，請參閱 [標識描述符節](../xdm/tutorials/create-schema-api.md) 在架構註冊表API教程中。

## 是否存在某些欄位不應標籤為標識的上下文？

標識欄位應保留給每個個人唯一的值。 例如，考慮客戶忠誠度計畫的資料集。 「忠誠度」欄位（金、銀、銅）將不是有用的身份欄位，而忠誠度ID（唯一值）將是。

ZIP代碼和IP地址等欄位不應被標籤為個人身份，因為這些值可以應用於多個個人。 這些類型的領域只應被標籤為家庭級營銷策略的標識。

## 為什麼我的身份欄位沒有與我期望的方式連結？

使用 [`/cluster/members` 端點](./api/list-cluster-identites.md) 在Identity Service API中，可以查看一個或多個標識欄位的關聯標識。 如果響應未返回您期望的連結標識，請確保您在XDM資料中提供了適當的標識資訊。 請參閱 [向Identity Service提供XDM資料](./home.md) 以瞭解詳細資訊。

## 什麼是標識命名空間？

標識名稱空間提供了標識欄位如何與客戶標識相關的上下文。 例如，「電子郵件」命名空間下的標識欄位應符合標準電子郵件格式（名稱）<span>@emailprovider.com)，而使用「Phone」命名空間的欄位應符合標準電話號碼（如北美的987-555-1234）。

命名空間區分不同CRM系統之間的相似標識值。 例如，請考慮包含與公司獎勵計畫關聯的數字忠誠ID的配置檔案。 「Loyalty」的命名空間將此值與電子商務系統的類似數字ID分開，該數字ID也顯示在同一配置檔案中。

查看 [標識命名空間概述](./home.md) 的子菜單。

## 如何將標識與標識命名空間關聯？

建立標識欄位時，必須將它們與現有標識命名空間關聯。 任何新命名空間都必須 [使用API建立](#how-do-i-create-a-custom-namespace-for-my-organization) 將它們與標識欄位關聯之前。

有關在使用API建立標識描述符時定義命名空間的逐步說明，請參見上的部分 [建立描述符](../xdm/tutorials/create-schema-ui.md) 在「架構註冊表開發人員指南」中。 要在UI中將架構欄位標籤為標識，請按照 [架構編輯器教程](../xdm/tutorials/create-schema-api.md)。

## Experience Platform提供的標準標識命名空間是什麼？ {#standard-namespaces}

標準標識命名空間可用於所有組織。 查看 [標識命名空間概述](./namespaces.md) 的子菜單。

## 在哪裡可以找到可用於我的組織的標識命名空間清單？

使用 [標識服務API](https://www.adobe.io/experience-platform-apis/references/identity-service)，通過向組織發出GET請求，可以列出組織的所有可用標識命名空間 `/idnamespace/identities` 端點。 請參閱 [列出可用命名空間](./api/list-namespaces.md) 詳細資訊，請參閱Identity Service API概述。

## 如何為我的組織建立自定義命名空間？

使用 [標識服務API](https://www.adobe.io/experience-platform-apis/references/identity-service)，通過向組織發出POST請求，可以為組織建立自定義標識命名空間 `/idnamespace/identities` 端點。 請參閱 [建立自定義命名空間](./api/create-custom-namespace.md) 詳細資訊，請參閱Identity Service API概述。

## 什麼是複合身份和XID?

標識在API調用中由其組合標識或XID引用。 組合標識是包含ID值和命名空間的標識的表示。 XID是單值標識符，它表示與組合標識（ID和命名空間）相同的構造，並且當Identity Service保留時，會自動將其分配給新標識。 查看 [Identity Service API概述](./home.md) 的子菜單。

## Identity Service如何處理個人身份資訊(PII)?

Identity Service具有標準命名空間，可支援接收已散列的電話號碼和電子郵件的標識值。 但是，您負責對值進行散列。 要瞭解有關接收到平台中的散列資料的詳細資訊，請參閱 [[!DNL Data Prep] 映射函式指南](../data-prep/functions.md#hashing)。

## 散列基於PII的標識時是否有考慮因素？

如果要將散列的PII值發送到Identity Service，則必須在資料集上使用相同的加密方法。 這可確保跨資料集的相同身份值生成相同的散列值，並能夠在身份圖中正確匹配和連結。

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

## 為什麼無法訪問標識圖頁或API?

您的平台管理員必須為您提供 `view-identity-graph` 以便您查看身份圖資料。 如果沒有此權限，您將在標識圖查看器頁面上和調用平台API時收到拒絕的權限消息。 查看 [訪問控制概述](../access-control/home.md) 的子菜單。

## 疑難排解

以下部分提供了有關特定錯誤代碼和使用時可能遇到的意外行為的故障排除建議 [!DNL Identity Service] API。

## [!DNL Identity Service] 錯誤消息

以下是使用 [!DNL Identity Service] API。

### 缺少必需的查詢參數

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

當請求路徑中未包括所需的查詢參數時，將顯示此錯誤。 的 `detail` 錯誤消息的名稱提供了缺少的參數的名稱。 此錯誤消息的變體包括：

- 缺少必需的查詢參數 — nsId
- 缺少必需的查詢參數 — ID
- 缺少必需的查詢參數 — xid或(nsid,id)
- 缺少必需的查詢參數 — targetNs
- 缺少必需的查詢參數 — xids或compositeXids

再次嘗試之前，請檢查是否在請求路徑中正確地包含了指定的參數。

### 時間戳應在最近180天內

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] 清除超過180天的資料。 當您嘗試訪問早於此時間的資料時，將顯示此錯誤消息。

### 單個呼叫中的XID限制為1000個

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

當嘗試檢索身份資訊的次數超過 [XID](#what-are-composite-identities-and-xids) 在單個API調用中允許。 將請求中的XID數量減少到所顯示的限制以下，以解決此問題。


### 單個呼叫中有1000個複合Xid的限制

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

當嘗試檢索身份資訊的次數超過 [複合身份](#what-are-composite-identities-and-xids) 在單個API調用中允許。 將請求中的複合標識數減少到顯示限制以下，以解決此問題。

### 指定的圖形類型無效

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

當 `graph-type` 查詢參數在請求路徑中賦值無效。 請參閱 [標識圖](./home.md) 的 [!DNL Identity Service] 概述，瞭解支援哪些圖形類型。

### 服務令牌沒有有效的作用域

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

當您的組織尚未為其設定適當的權限時，將顯示此錯誤消息 [!DNL Identity Service]。 請與系統管理員聯繫以解決此問題。

### 網關服務令牌無效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

如果出現此錯誤，則訪問令牌無效。 訪問令牌每24小時過期一次，必須重新生成才能繼續使用 [!DNL Platform] API。 查看 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en) 有關生成新訪問令牌的說明。

### 授權服務令牌無效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

如果出現此錯誤，則訪問令牌無效。 訪問令牌每24小時過期一次，必須重新生成才能繼續使用 [!DNL Platform] API。 查看 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en) 有關生成新訪問令牌的說明。

### 用戶令牌沒有有效的產品上下文

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

未從中生成訪問令牌時顯示此錯誤消息 [!DNL Experience Platform] 整合。 查看 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en) 有關為 [!DNL Experience Platform] 整合。

### 從標識和命名空間代碼獲取本機XID時出現內部錯誤

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

當 [!DNL Identity Service] 持續身份，為標識的ID和關聯的命名空間ID分配稱為XID的唯一標識符。 在查找給定ID值和命名空間的XID過程中發生錯誤時，將顯示此消息。

### 未為IMS組織設定 [!DNL Identity Service] 使用

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

當您的組織尚未為其設定適當的權限時，將顯示此錯誤消息 [!DNL Identity Service]。 請與系統管理員聯繫以解決此問題。

### 內部伺服器錯誤

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

執行時出現意外異常時，將顯示此錯誤 [!DNL Platform] 服務呼叫。 最佳做法是，在收到此錯誤時，對自動呼叫進行寫程式，以在定時間隔內重試其請求幾次。 如果問題仍然存在，請與系統管理員聯繫。

## 批接收錯誤代碼

[!DNL Identity Service] 從上載到的記錄和時間序列資料中接收標識資料 [!DNL Platform] 使用批處理接收。 由於批處理接收是非同步進程，因此必須查看批處理的詳細資訊才能查看錯誤。 錯誤將隨著批處理的進行而累積，直到批處理完成。

以下是與 [!DNL Identity Service] 使用 [批處理接收API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)。

### 未知的XDM架構

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] 僅使用符合記錄的或時間系列資料的標識 [!DNL Profile] 或 [!DNL ExperienceEvent] 類。 嘗試為 [!DNL Identity Service] 不符合任一類的將觸發此錯誤。

### 已處理批處理的前100行中有0個有效標識

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

當批的前100行未顯示標識時，將顯示此錯誤。 但是，此錯誤沒有確切地表明在後續記錄中未找到任何身份。

### 跳過記錄，因為每個XDM記錄只有1個標識

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] 僅當單個記錄顯示兩個或多個標識值時連結標識。 此錯誤消息針對每個接收的批發生一次，並顯示只能找到一個身份且導致對身份圖沒有更改的記錄數。

### 未為此IMS組織註冊命名空間代碼

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

當接收的記錄顯示其關聯命名空間不存在或貴組織無法訪問的標識時，將顯示此錯誤。

### 正在跳過批處理接收，因為IMS組織未為專用標識圖設定

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

在接收批處理資料時，當您的組織尚未為 [!DNL Identity Service]。 請與系統管理員聯繫以解決此問題。

### 內部錯誤

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

當批處理接收期間發生意外異常時，將顯示此錯誤。 最佳做法是，在收到此錯誤時，對自動呼叫進行寫程式，以在定時間隔內重試其請求幾次。 如果問題仍然存在，請與系統管理員聯繫。
