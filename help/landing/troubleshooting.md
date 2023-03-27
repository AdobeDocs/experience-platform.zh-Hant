---
keywords: Experience Platform；首頁；熱門主題；API錯誤碼；API錯誤碼；錯誤碼API；錯誤碼API;API要求錯誤；API疑難排解；API錯誤
solution: Experience Platform
title: Adobe Experience Platform常見問題集和疑難排解指南
description: 尋找常見問題的解答，以及針對 Experience Platform 中的常見錯誤進行疑難排解的指南。
landing-page-description: 尋找常見問題的解答，以及針對 Experience Platform 中的常見錯誤進行疑難排解的指南。
short-description: Find answers to frequently asked questions and a guide for troubleshooting common errors in Experience Platform.
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 3%

---

# [!DNL Platform] 常見問題集和疑難排解指南

本檔案提供Adobe Experience Platform常見問題的解答，以及任何常見錯誤的高階疑難排解指南 [!DNL Experience Platform] API。 個別的疑難排解指南 [!DNL Platform] 服務，請參閱 [服務疑難排解目錄](#service-troubleshooting-directory) 下方。

## 常見問題集 {#faq}

以下是關於Adobe Experience Platform常見問題的解答清單。

## 內容 [!DNL Experience Platform] API? {#what-are-experience-platform-apis}

[!DNL Experience Platform] 提供多個RESTful API，可使用HTTP請求來存取 [!DNL Platform] 資源。 這些服務API分別會公開多個端點，並可讓您執行列出(GET)、查詢(GET)、編輯(PUT和/或PATCH)和刪除(DELETE)資源的作業。 有關每個服務可用的特定端點和操作的詳細資訊，請參閱 [API參考檔案](https://www.adobe.com/go/platform-api-reference-en) Adobe I/O。

## 如何設定API請求的格式？ {#how-do-i-format-an-api-request}

請求格式會依 [!DNL Platform] 使用的API。 若要了解如何建構API呼叫，最佳方式是遵循檔案中提供的特定 [!DNL Platform] 您使用的服務。

如需建立API請求的詳細資訊，請參閱Platform API快速入門手冊 [讀取範例API呼叫](./api-guide.md#sample-api) 區段。

## 什麼是我的IMS組織？ {#what-is-my-ims-organization}

IMS組織是Adobe的代表。 任何經授權的Adobe解決方案都與此客戶組織整合。 當IMS組織有權使用 [!DNL Experience Platform]，則可指派開發人員的存取權。 IMS組織ID(`x-gw-ims-org-id`)代表應為執行API呼叫的組織，因此在所有API請求中都是標題。 此ID可透過 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui):在 **整合** 頁簽，導航到 **概述** 區段，以尋找下方的ID **客戶端憑據**. 如何驗證的逐步說明 [!DNL Platform]，請參閱 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en).

## 在哪裡可以找到我的API金鑰？ {#where-can-i-find-my-api-key}

所有API請求中都須有API金鑰作為標題。 您可以透過 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). 在主控台內， **整合** 頁簽，導航到 **概述** 區段，您會在 **客戶端憑據**. 如何驗證的逐步說明 [!DNL Platform]，請參閱 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en).

## 如何取得存取權杖？ {#how-do-i-get-an-access-token}

所有API呼叫的「授權」標題中都需要存取權杖。 可使用 `curl` 命令，前提是您有權存取IMS組織的整合。 存取權杖的有效期限僅為24小時，之後必須產生新權杖，才能繼續使用API。 如需產生存取權杖的詳細資訊，請參閱 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en).

## 如何使用查詢參數？ {#how-do-i-user-query-parameters}

部分 [!DNL Platform] API端點接受查詢參數以尋找特定資訊並篩選回應中傳回的結果。 查詢參數會附加至含有問號(`?`)符號，後面接著一或多個查詢參數（使用格式） `paramName=paramValue`. 在單一呼叫中結合多個參數時，您必須使用&amp;符號(`&`)以區隔個別參數。 下列範例將示範如何使用多個查詢參數的要求在檔案中的呈現方式。

常用的查詢參數範例包括：

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

有關特定服務或端點可用的查詢參數的詳細資訊，請查看特定服務的文檔。

## 如何在PATCH請求中指出要更新的JSON欄位？ {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

中的許多PATCH操作 [!DNL Platform] API使用 [JSON指標](https://tools.ietf.org/html/rfc6901) 表示要更新的JSON屬性的字串。 這些通常包含在要求裝載中，使用 [JSON修補程式](https://tools.ietf.org/html/rfc6902) 格式。 請參閱 [API基礎指南](api-fundamentals.md) 以取得這些技術所需語法的詳細資訊。

## 我可以使用Postman來呼叫 [!DNL Platform] API? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) 是將對RESTful API的呼叫視覺化的實用工具。 此 [Platform API快速入門手冊](api-guide.md) 包含匯入Postman集合的影片和說明。 此外，也提供每項服務的Postman集合清單。

## 針對 [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

視您使用的是UI或API而定，適用下列系統需求：

**針對以UI為基礎的作業：**
- 現代化的標準網頁瀏覽器。 若 [!DNL Chrome] 建議使用目前和過去主要版本 [!DNL Firefox], [!DNL Internet Explorer]也支援、和Safari。
   - 每次發行新的主要版本時， [!DNL Platform] 開始支援最新版本，而放棄支援最新第三版。
- 所有瀏覽器都必須啟用Cookie和JavaScript。

**若是API與開發人員互動：**
- 針對REST、串流和Webhook整合進行開發的開發環境。

## 錯誤和疑難排解 {#errors-and-troubleshooting}

以下是使用任何 [!DNL Experience Platform] 服務。 個別的疑難排解指南 [!DNL Platform] 服務，請參閱 [服務疑難排解目錄](#service-troubleshooting-directory) 下方。

## API狀態代碼 {#api-status-codes}

可能會在任何 [!DNL Experience Platform] API。 每個原因各有不同，因此本節中的解釋一般性。 如需有關個別中特定錯誤的詳細資訊 [!DNL Platform] 服務，請參閱 [服務疑難排解目錄](#service-troubleshooting-directory) 下方。

| 狀態代碼 | 說明 | 可能的原因 |
|--- | --- | ---|
| 400 | 錯誤請求 | 請求的建構不正確、遺失重要資訊，和/或包含錯誤的語法。 |
| 401 | 驗證失敗 | 請求未通過驗證檢查。 您的存取權杖可能遺失或無效。 請參閱 [OAuth代號錯誤](#oauth-token-is-missing) 一節以取得詳細資訊。 |
| 403 | 禁止 | 找到資源，但您沒有查看該資源的正確憑據。 |
| 404 | 找不到 | 在伺服器上找不到請求的資源。 資源可能已刪除，或請求的路徑輸入不正確。 |
| 500 | 內部伺服器錯誤 | 這是伺服器端錯誤。 如果您同時進行許多呼叫，可能已達到API限制，因此需要篩選結果。 (請參閱 [!DNL Catalog Service] 上的API開發人員指南子指南 [篩選資料](../catalog/api/filter-data.md) 以了解更多。) 請等候片刻，然後再次嘗試您的請求，如果問題仍然存在，請聯絡您的管理員。 |

## 請求標題錯誤 {#request-header-errors}

中的所有API呼叫 [!DNL Platform] 需要特定的要求標題。 若要查看個別服務需要哪些標題，請參閱 [API參考檔案](https://www.adobe.com/go/platform-api-reference-en). 若要尋找所需驗證標題的值，請參閱 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 如果進行API呼叫時，這些標題中有任何一個遺失或無效，可能會發生下列錯誤。

### 缺少OAuth代號 {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

當 `Authorization` API請求中缺少標題。 在再次嘗試之前，請確保Authorization標頭包含有效的訪問令牌。

### OAuth代號無效 {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

在 `Authorization` 標題無效。 請確定已正確輸入代號，或 [產生新代號](https://www.adobe.com/go/platform-api-authentication-en) 在Adobe I/O主控台中。

### 需要API金鑰 {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

當API金鑰標題(`x-api-key`)缺少。 再次嘗試之前，請確定標題已包含有效的API金鑰。

### API密鑰無效 {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

提供之API金鑰標題的值(`x-api-key`)無效。 請確定您已正確輸入金鑰，然後再次嘗試。 如果您不知道您的API金鑰，可在 [Adobe I/O主控台](https://console.adobe.io):在 **整合** 頁簽，導航到 **概述** 區段，以尋找 **客戶端憑據**.

### 缺少標題 {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

當IMS組織標題(`x-gw-ims-org-id`)缺少。 再次嘗試之前，請確定標題已包含在您IMS組織的ID中。

### 配置檔案無效 {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

當使用者或Adobe I/O整合時(由 [存取權杖](#how-do-i-get-an-access-token) 在 `Authorization` 標題)無權呼叫 [!DNL Experience Platform] 提供於 `x-gw-ims-org-id` 頁首。 請確定您已在標題中為IMS組織提供正確的ID，然後再試一次。 如果您不知道組織ID，可在 [Adobe I/O主控台](https://console.adobe.io):在 **整合** 頁簽，導航到 **概述** 區段，以尋找 **客戶端憑據**.

### 刷新etag錯誤 {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

如果其他API調用方對任何源實體或目標實體（如流、連接、源連接器或目標連接）進行了更改，則可能會收到etag錯誤。 由於版本不符，您嘗試進行的變更不會套用至實體的最新版本。

若要解決此問題，您需要再次擷取實體，確認您的變更與新版本的實體相容，然後將新標籤放入 `If-Match` 標題，最後進行API呼叫。

### 未指定有效的內容類型 {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

當POST、PUT或PATCH請求無效或遺失時，會顯示此錯誤訊息 `Content-Type` 頁首。 確定請求中包含標題，且其值為 `application/json`.

### 缺少用戶區域 {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

此錯誤訊息會顯示在以下兩種情況之一：
- 當IMS組織標題不正確或格式錯誤時(`x-gw-ims-org-id`)會傳遞至API請求。 再試一次之前，請確定已包含正確的ID。
- 當您的帳戶（如提供的驗證憑證所示）未與產品設定檔建立關聯以進行Experience Platform時。 請依照 [生成訪問憑據](./api-authentication.md#authentication-for-each-session) 在Platform API驗證教學課程中，將Platform新增至您的帳戶，並據此更新您的驗證憑證。

## 服務故障排除目錄 {#service-troubleshooting-directory}

以下是的疑難排解指南和API參考檔案清單 [!DNL Experience Platform] API。 每個疑難排解指南都提供個別專屬常見問題的解答和問題解決方案 [!DNL Platform] 服務。 API參考檔案提供每個服務所有可用端點的完整指南，並顯示您可能收到的範例要求本文、回應和錯誤碼。

| 服務 | API 參考 | 疑難排解 |
| --- | --- | --- |
| 存取控制 | [存取控制API](https://www.adobe.io/experience-platform-apis/references/access-control/) | [存取控制疑難排解指南](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform資料擷取 | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [批次內嵌疑難排解指南](../ingestion/batch-ingestion/troubleshooting.md) |
| Adobe Experience Platform資料擷取 | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [串流內嵌疑難排解指南](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] 疑難排解指南](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform資料控管 | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] 疑難排解指南](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform查詢服務 | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] 疑難排解指南](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform區段 | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] 常見問題集和疑難排解指南](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] 和 [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] 疑難排解指南](../profile/troubleshooting.md) |
| 沙箱 | [沙箱API](https://www.adobe.io/experience-platform-apis/references/sandbox) | [沙箱疑難排解指南](../sandboxes/troubleshooting-guide.md) |
