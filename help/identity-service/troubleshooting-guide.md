---
keywords: Experience Platform;home；熱門主題；標識命名空間；標識命名空間
solution: Experience Platform
title: Identity Service疑難排解指南
topic-legacy: troubleshooting
description: 本檔案提供有關Adobe Experience Platform身分服務常見問題的解答，以及常見錯誤的疑難排解指南。
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2189'
ht-degree: 0%

---

# Identity Service疑難排解指南

本檔案提供有關Adobe Experience Platform[!DNL Identity Service]常見問題的解答，以及常見錯誤的疑難排解指南。 有關[!DNL Platform] API的一般問題和疑難排解，請參閱[Adobe Experience PlatformAPI疑難排解指南](../landing/troubleshooting.md)。

識別單一客戶的資料通常會分散在他們用來與您的品牌互動的各種裝置和系統上。 [!DNL Identity Service] 將這些零散的身份匯集在一起，以便全面瞭解客戶行為，以便您即時提供具影響力的數位體驗。如需詳細資訊，請參閱[身分服務概觀](./home.md)。

## 常見問題集

以下是有關[!DNL Identity Service]常見問題的解答清單。

## 什麼是身分資料？

身分資料是可用於識別個人的任何資料。 視組織內使用資料的情況而定，識別資料可包含CRM系統的使用者名稱、電子郵件地址和ID。 身分資料不限於您網站或服務的註冊使用者，因為匿名使用者也可透過其裝置或Cookie ID來識別。

## 將資料欄位標示為身分的好處為何？

將某些資料欄位標示為記錄和時間系列資料中的身分識別，可讓您在資料的自然結構中對應身分關係，並協調跨通道的重複資料。 如需詳細資訊，請參閱[身分服務概觀](./home.md)。

## 什麼是已知和匿名身份？

已知身份是指可單獨使用或與其他資訊一起使用的身份值，以識別、聯絡或尋找個人。 已知身分的範例可能包括電子郵件地址、電話號碼和CRM ID。

匿名身分是指無法單獨使用或與其他資訊一起使用的身分值，以識別、聯絡或尋找個別人員（例如Cookie ID）。

## 什麼是私人身分圖？

「私人身分圖」是銜接與連結身分之間關係的私人地圖，僅供您的組織使用。

當從串流端點擷取或傳送至啟用[!DNL Identity Service]的資料集的任何資料中包含多個身分識別時，這些身分識別會連結在「私用身分圖」中。 [!DNL Identity Service] 利用此圖表來收集特定消費者或實體的身分識別，以便進行身分識別拼接和描述檔合併。

## 如何在XDM架構中建立多個識別欄位？

[體驗資料模型(XDM)結構](../xdm/home.md) 支援多個身分欄位。在實現XDM Individual Profile或XDM ExperienceEvent類的架構中，任何類型`string`的資料欄位都可以標籤為標識欄位。 標籤後，這些欄位中包含的任何資料都會新增至描述檔的識別地圖。

有關如何使用用戶介面將XDM欄位標籤為標識欄位的步驟，請參閱「模式編輯器」教程中的[標識部分](../xdm/tutorials/create-schema-ui.md)。 如果您使用API，請參閱「方案註冊表API」教程中的[Identity描述符部分](../xdm/tutorials/create-schema-api.md)。

## 是否有些欄位不應標示為身分的上下文？

身分欄位應保留給每個個人專屬的值。 例如，請考慮客戶忠誠度方案的資料集。 「忠誠度等級」欄位（金、銀、銅）將不是有用的身分識別欄位，而忠誠度ID（唯一值）則是。

郵遞區號和IP位址等欄位不應標示為個人的身分，因為這些值可套用至多個個人。 這些類型的欄位只應標示為家庭層級行銷策略的身分。

## 為什麼我的身份欄位無法連結我的預期？

使用Identity Service API中的[`/cluster/members`端點](./api/list-cluster-identites.md)，您可以查看一個或多個身份欄位的關聯身份。 如果回應未傳回您預期的連結身分，請確定您是在XDM資料中提供適當的身分資訊。 如需詳細資訊，請參閱Identity Service概觀中有關提供XDM資料給Identity Service](./home.md)的章節。[

## 什麼是身分命名空間？

身分名稱空間提供識別欄位與客戶身份相關的上下文。 例如，「電子郵件」名稱空間下的身分欄位應符合標準電子郵件格式（名稱<span>@emailprovider.com），而使用「Phone」名稱空間的欄位應符合標準電話號碼（例如北美地區的987-555-1234）。

名稱空間可區分不同CRM系統之間的相似身分值。 例如，假設描述檔包含與公司獎勵方案相關聯的數值「忠誠度ID」。 「忠誠度」的命名空間會將此值與電子商務系統的類似數值ID（也會顯示在相同的描述檔中）區隔。

如需詳細資訊，請參閱[identity namespace綜覽](./home.md)。

## 如何將身份與身份名稱空間關聯？

身分欄位建立時，必須與現有的身分名稱空間相關聯。 任何新名稱空間都必須使用API](#how-do-i-create-a-custom-namespace-for-my-organization)建立[，才能與識別欄位建立關聯。

有關使用API建立標識描述符時定義命名空間的逐步說明，請參閱《方案註冊表開發人員指南》中有關建立描述符[的部分。 ](../xdm/tutorials/create-schema-ui.md)要在UI中將架構欄位標籤為標識，請遵循[架構編輯器教程](../xdm/tutorials/create-schema-api.md)中的步驟。

## Experience Platform提供的標準身分名稱空間是什麼？{#standard-namespaces}

標準識別名稱空間是所有組織都可用的名稱空間。 如需可用標準名稱空間的完整清單，請參閱[身分名稱空間概觀](./namespaces.md)。

## 我可以在哪裡找到組織可用的身份名稱空間清單？

使用[Identity Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)，您可以向`/idnamespace/identities`端點發出GET請求，列出組織的所有可用身份名稱空間。 如需詳細資訊，請參閱Identity Service API總覽中列出可用名稱空間](./api/list-namespaces.md)的章節。[

## 如何為組織建立自訂命名空間？

使用[Identity Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)，您可以向`/idnamespace/identities`端點發出POST請求，為組織建立自定義身份名稱空間。 如需詳細資訊，請參閱Identity Service API總覽中有關建立自訂命名空間的[一節。](./api/create-custom-namespace.md)

## 什麼是複合身份和XID?

身分識別在API呼叫中會由其複合身分識別或XID參考。 複合身分代表包含ID值和命名空間的身分。 XID是單值識別碼，代表與複合身分識別（ID和命名空間）相同的構造，當Identity Service持續存在時，會自動指派給新身分識別。 如需詳細資訊，請參閱[Identity Service API概觀](./home.md)。

## Identity Service如何處理個人識別資訊(PII)?

Identity Service會在持續值之前建立強大、單向的PII密碼雜湊。 使用SHA-256自動雜湊「電話」和「電子郵件」名稱空間中的身分資料，「電子郵件」值會在雜湊前自動轉換為小寫。

## 我是否應在傳送至平台之前加密所有PII?

在將PII資料收入平台之前，您不需要手動加密PII資料。 透過將`I1`資料使用標籤套用至所有適用的資料欄位，Platform會在擷取時自動將這些欄位轉換為雜湊的ID值。

如需如何套用和管理資料使用標籤的步驟，請參閱[資料使用標籤教學課程](../data-governance/labels/user-guide.md)。

## 在散列基於PII的身份時，是否有考慮事項？

如果您要將雜湊PII值傳送至Identity Service，則必須在資料集上使用相同的加密方法。 如此可確保資料集上的相同身分值會產生相同的雜湊值，並可在身分圖中正確比對及連結。

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

## 疑難排解

下節針對使用[!DNL Identity Service] API時可能遇到的特定錯誤代碼和意外行為提供疑難排解建議。

## [!DNL Identity Service] 錯誤消息

以下是使用[!DNL Identity Service] API時可能遇到的錯誤訊息清單。

### 缺少必需的查詢參數

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

當請求路徑中未包含必要的查詢參數時，會顯示此錯誤。 錯誤消息的`detail`提供缺少參數的名稱。 此錯誤訊息的變化包括：

- 缺少必需的查詢參數- nsId
- 缺少必需的查詢參數- id
- 遺失必要的查詢參數- xid或(nsid,id)
- 遺失必要的查詢參數- targetNs
- 缺少必需的查詢參數- xids或compositeXids

在再次嘗試之前，請先檢查您是否已在請求路徑中正確加入指示的參數。

### 時間戳記應在最近180天內

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] 清除180天以上的資料。當您嘗試存取早於此日期的資料時，會顯示此錯誤訊息。

### 單一呼叫的XID上限為1000個

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

當您嘗試擷取超過單一API呼叫中允許之最大數目[XIDs](#what-are-composite-identities-and-xids)的身分資訊時，會顯示此錯誤訊息。 將請求中的XID數量減少至顯示的限制以解決此問題。


### 單一呼叫中限制1000個compositeXids

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

當您嘗試擷取超過單一API呼叫中允許之最大數目[複合身分識別](#what-are-composite-identities-and-xids)的身分資訊時，會顯示此錯誤訊息。 將請求中的複合身分識別數目減少至顯示的限制以解決此問題。

### 指定的圖形類型無效

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

當`graph-type`查詢參數在請求路徑中被指定為無效值時，會顯示此錯誤訊息。 請參閱[!DNL Identity Service]概觀中關於[identity graphs](./home.md)的章節，瞭解支援哪些圖形類型。

### 服務Token沒有有效範圍

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

當您的IMS組織尚未布建適當的[!DNL Identity Service]權限時，會顯示此錯誤訊息。 請連絡您的系統管理員以解決此問題。

### 閘道服務Token無效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

如果發生此錯誤，您的存取Token無效。 存取Token每24小時過期一次，必須重新產生，才能繼續使用[!DNL Platform] API。 有關生成新訪問Token的說明，請參見[驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。

### 授權服務Token無效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

如果發生此錯誤，您的存取Token無效。 存取Token每24小時過期一次，必須重新產生，才能繼續使用[!DNL Platform] API。 有關生成新訪問Token的說明，請參見[驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。

### 使用者Token沒有有效的產品內容

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

當您的存取Token尚未從[!DNL Experience Platform]整合產生時，會顯示此錯誤訊息。 有關為[!DNL Experience Platform]整合產生新存取Token的指示，請參閱[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。

### 從識別碼和命名空間程式碼取得原生XID時發生內部錯誤

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

當[!DNL Identity Service]保留身分時，會為識別的ID和相關的命名空間ID指派一個稱為XID的唯一識別碼。 當在尋找指定ID值和命名空間的XID過程中發生錯誤時，會顯示此訊息。

### 未針對[!DNL Identity Service]使用情況布建IMS組織

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

當您的IMS組織尚未布建適當的[!DNL Identity Service]權限時，會顯示此錯誤訊息。 請連絡您的系統管理員以解決此問題。

### 內部伺服器錯誤

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

當執行[!DNL Platform]服務呼叫時發生意外異常時，會顯示此錯誤。 最佳實務是，在收到此錯誤時，設定您的自動呼叫程式，以計時間隔重試其要求幾次。 如果問題仍然存在，請與系統管理員聯繫。

## 批次擷取錯誤碼

[!DNL Identity Service] 從使用「批次擷取」上傳至的記錄和時間序列資料擷取 [!DNL Platform] 身分資料。由於批處理提取是非同步流程，因此您必須查看批處理的詳細資訊才能查看錯誤。 錯誤會隨著批處理進行而累積，直到批處理完成為止。

以下是使用[資料擷取API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)時可能會遇到的與[!DNL Identity Service]相關的錯誤訊息清單。

### 未知的XDM模式

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] 僅對分別符合或類的記錄或時間序列資料 [!DNL Profile] 使 [!DNL ExperienceEvent] 用身份。嘗試為[!DNL Identity Service]未符合任一類別的資料收錄，將會觸發此錯誤。

### 處理批的前100行中有0個有效身份

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

當批次的前100列未顯示任何身分時，就會顯示此錯誤。 但是，此錯誤沒有明確表示在後續記錄中找不到任何身份。

### 跳過記錄，因為每個XDM記錄只有1個身份

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] 只有當單一記錄顯示兩個或更多身分值時，才會連結身分。每個收錄的批次都會發生此錯誤訊息一次，並顯示只能找到一個身分的記錄數，且不會造成身分圖表變更。

### 未為此IMS組織註冊命名空間代碼

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

當收錄的記錄呈現您的IMS組織不存在或無法存取其相關名稱空間的身分時，會顯示此錯誤。

### 由於未為「私用身分圖」布建IMS組織，因此正在跳過批次擷取

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

在擷取批次資料時，當您的IMS組織尚未布建適當的[!DNL Identity Service]權限時，會顯示此錯誤訊息。 請連絡您的系統管理員以解決此問題。

### 內部錯誤

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

當批次擷取期間發生意外例外時，會顯示此錯誤。 最佳實務是，在收到此錯誤時，設定您的自動呼叫程式，以計時間隔重試其要求幾次。 如果問題仍然存在，請與系統管理員聯繫。
