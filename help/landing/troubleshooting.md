---
keywords: Experience Platform；首頁；熱門主題；API錯誤代碼；API錯誤代碼；錯誤代碼API；錯誤代碼API；API請求錯誤；API疑難排解；API錯誤
solution: Experience Platform
title: Adobe Experience Platform常見問題集和疑難排解指南
description: 尋找常見問題的解答，以及針對 Adobe Experience Platform 中的常見錯誤進行疑難排解的指南。
landing-page-description: 尋找常見問題的解答，以及針對 Adobe Experience Platform 中的常見錯誤進行疑難排解的指南。
short-description: 尋找常見問題的解答，以及針對 Experience Platform 中的常見錯誤進行疑難排解的指南。
type: Documentation
role: Developer
feature: API, Audiences, Data Ingestion, Datasets, Destinations, Privacy, Queries, Schemas, Sandboxes, Sources
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 4%

---

# [!DNL Experience Platform]常見問題集和疑難排解指南

本檔案提供有關Adobe Experience Platform常見問題的解答，以及任何[!DNL Experience Platform] API中可能遇到的常見錯誤的高層級疑難排解指南。 如需個別[!DNL Experience Platform]服務的疑難排解指南，請參閱下方的[服務疑難排解目錄](#service-troubleshooting-directory)。

## 常見問題集 {#faq}

以下是有關Adobe Experience Platform常見問題的解答清單。

## 什麼是[!DNL Experience Platform] API？ {#what-are-experience-platform-apis}

[!DNL Experience Platform]提供多個使用HTTP要求存取[!DNL Experience Platform]資源的RESTful API。 這些服務API會分別公開多個端點，並允許您執行作業以列出(GET)、查詢(GET)、編輯(PUT和/或PATCH)及刪除(DELETE)資源。 如需每個服務可用的特定端點和作業的詳細資訊，請參閱Adobe I/O上的[API參考檔案](https://www.adobe.com/go/platform-api-reference-en)。

## 如何格式化API請求？ {#how-do-i-format-an-api-request}

要求格式會依使用的[!DNL Experience Platform] API而有所不同。 要瞭解如何建構API呼叫，最好的方式是遵循檔案中針對您使用的特定[!DNL Experience Platform]服務提供的範例。

如需格式化API要求的詳細資訊，請造訪Experience Platform API快速入門手冊[閱讀範例API呼叫](./api-guide.md#sample-api)區段。

## 什麼是我的組織？ {#what-is-my-ims-organization}

組織是客戶的Adobe表示法。 任何授權的Adobe解決方案都會與此客戶組織整合。 當組織有權使用[!DNL Experience Platform]時，它可以指派存取權給開發人員。 組織ID (`x-gw-ims-org-id`)代表應為其執行API呼叫的組織，因此需要作為所有API要求中的標頭。 可以透過[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)找到此ID：在&#x200B;**整合**&#x200B;索引標籤中，瀏覽至&#x200B;**總覽**&#x200B;區段以進行任何特定整合，以在&#x200B;**使用者端認證**&#x200B;下找到此ID。 如需如何向[!DNL Experience Platform]進行驗證的逐步說明，請參閱[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。

## 我可以在哪裡找到我的API金鑰？ {#where-can-i-find-my-api-key}

API金鑰需作為所有API請求中的標頭。 您可透過[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)找到它。 在主控台的&#x200B;**整合**&#x200B;標籤上，瀏覽至&#x200B;**總覽**&#x200B;區段以取得特定的整合，您會在&#x200B;**使用者端認證**&#x200B;下找到金鑰。 如需如何驗證[!DNL Experience Platform]的逐步解說，請參閱[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。

## 如何取得存取Token？ {#how-do-i-get-an-access-token}

所有API呼叫的Authorization標頭中都需要存取權杖。 只要您擁有組織整合的存取權，便可使用CURL指令產生這些專案。 存取權杖僅有效24小時，之後必須產生新權杖才能繼續使用API。 如需有關產生存取權杖的詳細資訊，請參閱[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。

## 如何使用查詢引數？ {#how-do-i-user-query-parameters}

某些[!DNL Experience Platform] API端點會接受查詢引數，以找出特定資訊並篩選回應中傳回的結果。 查詢引數會以問號(`?`)符號附加至要求路徑，後面接著一或多個查詢引數（使用格式`paramName=paramValue`）。 在單一呼叫中組合多個引數時，您必須使用&amp;符號(`&`)來分隔個別引數。 下列範例示範使用多個查詢引數的請求在檔案中如何呈現。

常用的查詢引數範例包括：

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

如需特定服務或端點可使用哪些查詢引數的詳細資訊，請參閱服務特定檔案。

## 如何在PATCH請求中指定要更新的JSON欄位？ {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

[!DNL Experience Platform] API中的許多PATCH作業都會使用[JSON指標](https://tools.ietf.org/html/rfc6901)字串來指示要更新的JSON屬性。 這些通常包含在使用[JSON修補程式](https://tools.ietf.org/html/rfc6902)格式的要求裝載中。 如需這些技術所需語法的詳細資訊，請參閱[API基礎指南](api-fundamentals.md)。

## 我可以使用Postman來呼叫[!DNL Experience Platform] API嗎？ {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/)是視覺化呼叫RESTful API的實用工具。 [Experience Platform API快速入門手冊](api-guide.md)包含匯入Postman集合的影片和指示。 此外，也提供每項服務的Postman集合清單。

## [!DNL Experience Platform]的系統需求為何？{#what-are-the-system-requirements-for-platform}

根據您使用的是UI還是API，以下系統需求適用：

**針對以UI為基礎的作業：**
- 現代的標準網路瀏覽器。 雖然建議使用最新版[!DNL Chrome]，但亦支援[!DNL Firefox]、[!DNL Internet Explorer]和Safari的最新和舊版主要版本。
   - 每次發行新的主要版本時，[!DNL Experience Platform]會開始支援最新版本，而不再支援第三個最新版本。
- 所有瀏覽器都必須啟用Cookie和JavaScript。

**對於API和開發人員互動：**
- 要為REST、串流和Webhook整合開發的開發環境。

## 錯誤與疑難排解 {#errors-and-troubleshooting}

以下是您使用任何[!DNL Experience Platform]服務時可能遇到的錯誤清單。 如需個別[!DNL Experience Platform]服務的疑難排解指南，請參閱下方的[服務疑難排解目錄](#service-troubleshooting-directory)。

## API狀態代碼 {#api-status-codes}

在任何[!DNL Experience Platform] API上可能會遇到下列狀態代碼。 每種原因有多種多樣，因此本節中提供的說明本質上是一般性解釋。 如需個別[!DNL Experience Platform]服務中特定錯誤的詳細資訊，請參閱下方的[服務疑難排解目錄](#service-troubleshooting-directory)。

| 狀態代碼 | 說明 | 可能的原因 |
|--- | --- | ---|
| 400 | 錯誤的請求 | 請求建構不正確、遺漏關鍵資訊和/或包含不正確的語法。 |
| 401 | 驗證失敗 | 請求未通過驗證檢查。 您的存取權杖可能遺失或無效。 如需詳細資訊，請參閱下方的[OAuth權杖錯誤](#oauth-token-is-missing)區段。 |
| 403 | 禁止 | 已找到資源，但您沒有正確的認證可檢視該資源。 <br>發生此錯誤的可能原因是，您可能沒有存取或編輯資源所需的[存取控制許可權](/help/access-control/home.md)。 閱讀如何[取得必要的屬性型存取控制許可權](/help/landing/api-authentication.md#get-abac-permissions)，以使用Experience Platform API。 </p> |
| 404 | 找不到 | 在伺服器上找不到要求的資源。 資源可能已被刪除，或輸入的路徑不正確。 |
| 500 | 內部伺服器錯誤 | 這是伺服器端錯誤。 如果您同時進行多個呼叫，可能會達到API限制，且需要篩選結果。 （如需瞭解詳細資訊，請參閱[篩選資料](../catalog/api/filter-data.md)上的[!DNL Catalog Service] API開發人員指南子指南。） 請稍候片刻，然後再嘗試您的請求，如果問題仍然存在，請聯絡您的管理員。 |

## 請求標頭錯誤 {#request-header-errors}

[!DNL Experience Platform]中的所有API呼叫都需要特定的要求標頭。 若要檢視個別服務所需的標頭，請參閱[API參考檔案](https://www.adobe.com/go/platform-api-reference-en)。 若要尋找所需驗證標頭的值，請參閱[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 如果在進行API呼叫時，缺少這些標頭中的任何一個或這些標頭無效，便可能會發生以下錯誤。

### 缺少OAuth權杖 {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

當API請求中缺少`Authorization`標頭時，會顯示此錯誤訊息。 在重試之前，請確定Authorization標頭包含於有效的存取權杖中。

### OAuth權杖無效 {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

當`Authorization`標頭中提供的存取權杖無效時，此錯誤訊息便會顯示。 請確定已正確輸入權杖，或在Adobe I/O主控台中[產生新權杖](https://www.adobe.com/go/platform-api-authentication-en)。

### 需要API金鑰 {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

當API要求中缺少API金鑰標頭(`x-api-key`)時，此錯誤訊息便會顯示。 在重試之前，請確定標頭包含有效的API金鑰。

### API金鑰無效 {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

當提供的API金鑰標頭(`x-api-key`)的值無效時，會顯示此錯誤訊息。 在重試之前，請確定您已正確輸入金鑰。 如果您不知道您的API金鑰，可以在[Adobe I/O主控台](https://console.adobe.io)中找到：在&#x200B;**整合**&#x200B;索引標籤中，瀏覽至&#x200B;**總覽**&#x200B;區段以取得特定整合，以便在&#x200B;**使用者端認證**&#x200B;下找到API金鑰。

### 標頭遺失 {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

當API請求中缺少組織標頭(`x-gw-ims-org-id`)時，會顯示此錯誤訊息。 在重試之前，請確定您的組織ID中包含標頭。

### 設定檔無效 {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

當使用者或Adobe I/O整合（由`Authorization`標頭中的[存取權杖](#how-do-i-get-an-access-token)識別）無權呼叫`x-gw-ims-org-id`標頭中提供的組織的[!DNL Experience Platform] API時，此錯誤訊息便會顯示。 在重試之前，請確定已在標頭中為您的組織提供正確的ID。 如果您不知道組織ID，可以在[Adobe I/O主控台](https://console.adobe.io)中找到：在&#x200B;**整合**&#x200B;索引標籤中，瀏覽至&#x200B;**總覽**&#x200B;區段以取得特定整合，以便在&#x200B;**使用者端認證**&#x200B;下找到組織ID。

### 重新整理etag錯誤 {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

如果其他API呼叫者對任何來源或目的地實體（例如流量、連線、來源聯結器或目標連線）進行了變更，您可能會收到etag錯誤。 由於版本不符，您嘗試進行的變更將不會套用至實體的最新版本。

若要解決此問題，您必須再次擷取實體、確定您的變更與實體的新版本相容，然後將新的etag放在`If-Match`標頭中，最後進行API呼叫。

### 未指定有效的內容型別 {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

當POST、PUT或PATCH要求具有無效或遺失`Content-Type`標頭時，此錯誤訊息便會顯示。 請確定要求中包含標頭，且其值為`application/json`。

### 缺少使用者區域 {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

此錯誤訊息會在以下兩種情況之一中顯示：
- 在API要求中傳遞不正確或格式錯誤的組織ID標頭(`x-gw-ims-org-id`)時。 在重試之前，請確定已包含您組織的正確ID。
- 當您的帳戶（由提供的驗證憑證表示）未與Experience Platform的產品設定檔建立關聯時。 依照Experience Platform API驗證教學課程中[產生存取認證](./api-authentication.md#authentication-for-each-session)上的步驟操作，將Experience Platform新增至您的帳戶並相應地更新您的驗證認證。

## 服務疑難排解目錄 {#service-troubleshooting-directory}

以下是[!DNL Experience Platform] API的疑難排解指南和API參考檔案清單。 每個疑難排解指南都會提供常見問題的解答，以及個別[!DNL Experience Platform]服務特定問題的解決方案。 API參考檔案提供每個服務所有可用端點的完整指南，並顯示您可能收到的範例要求內文、回應和錯誤代碼。

| 服務 | API參考 | 疑難排解 |
| --- | --- | --- |
| 存取控制 | [存取控制API](https://www.adobe.io/experience-platform-apis/references/access-control/) | [存取控制疑難排解指南](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform資料擷取 | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [批次擷取疑難排解指南](../ingestion/batch-ingestion/troubleshooting.md) |
| Adobe Experience Platform資料擷取 | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [串流擷取疑難排解指南](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform資料科學Workspace | [[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) | [[!DNL Data Science Workspace] 疑難排解指南](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform資料控管 | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] 疑難排解指南](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform查詢服務 | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] 疑難排解指南](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform區段 | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] 常見問題集和疑難排解指南](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] （[!DNL Sources]和[!DNL Destinations]） | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] 疑難排解指南](../profile/troubleshooting.md) |
| 沙箱 | [沙箱API](https://www.adobe.io/experience-platform-apis/references/sandbox) | [沙箱疑難排解指南](../sandboxes/troubleshooting-guide.md) |
