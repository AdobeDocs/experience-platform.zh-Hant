---
keywords: Experience Platform；首頁；熱門主題；API錯誤代碼；API錯誤代碼；錯誤代碼API；錯誤代碼API；錯誤代碼API;API請求錯誤；API疑難解答；API錯誤
solution: Experience Platform
title: Adobe Experience Platform常見問題解答和故障排除指南
description: 尋找常見問題的解答，以及針對 Experience Platform 中的常見錯誤進行疑難排解的指南。
landing-page-description: 尋找常見問題的解答，以及針對 Experience Platform 中的常見錯誤進行疑難排解的指南。
short-description: 尋找常見問題的解答，以及針對 Experience Platform 中的常見錯誤進行疑難排解的指南。
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1868'
ht-degree: 4%

---

# [!DNL Platform] 常見問題解答和故障排除指南

本文檔提供有關Adobe Experience Platform的常見問題的解答，並提供高級故障排除指南，以瞭解在任何情況下可能遇到的常見錯誤 [!DNL Experience Platform] API。 有關各個故障排除指南的資訊 [!DNL Platform] 服務，請參閱 [服務疑難解答目錄](#service-troubleshooting-directory) 下。

## 常見問題集 {#faq}

以下是關於Adobe Experience Platform的常見問題解答清單。

## 什麼是 [!DNL Experience Platform] API? {#what-are-experience-platform-apis}

[!DNL Experience Platform] 提供多個使用HTTP請求訪問的REST風格API [!DNL Platform] 資源。 這些服務API每個都會顯示多個端點，並允許您執行清單(GET)、查找(GET)、編輯(PUT和/或PATCH)和刪除(DELETE)資源的操作。 有關每個服務的特定終結點和操作的詳細資訊，請參閱 [API參考文檔](https://www.adobe.com/go/platform-api-reference-en) Adobe I/O。

## 如何格式化API請求？ {#how-do-i-format-an-api-request}

請求格式因 [!DNL Platform] 正在使用的API。 學習如何構造API調用的最佳方法是，隨附特定API調用文檔中提供的示例 [!DNL Platform] 服務。

有關建立API請求的詳細資訊，請訪問平台API入門指南 [讀取示例API調用](./api-guide.md#sample-api) 的子菜單。

## 我的組織是什麼？ {#what-is-my-ims-organization}

組織是客戶的Adobe表示。 任何經許可的Adobe解決方案都與此客戶組織整合。 當組織有權 [!DNL Experience Platform]，它可以將訪問權限分配給開發人員。 組織ID(`x-gw-ims-org-id`)表示應為執行API調用的組織，因此在所有API請求中都需要作為標頭。 此ID可通過 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui):的 **整合** 頁籤，導航到 **概述** 的ID **客戶端憑據**。 有關如何驗證到 [!DNL Platform]，請參見 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 在哪裡可以找到我的API密鑰？ {#where-can-i-find-my-api-key}

所有API請求中都需要API密鑰作為頭。 可以通過 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui)。 在控制台中， **整合** 頁籤，導航到 **概述** 的下一頁，您將在 **客戶端憑據**。 有關如何驗證到的逐步步驟 [!DNL Platform]，請參見 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 如何獲得訪問令牌？ {#how-do-i-get-an-access-token}

所有API調用的授權標頭中都需要訪問令牌。 如果您有權訪問組織的整合，則可以使用CURL命令生成它們。 訪問令牌僅有24小時有效，此後必須生成新令牌才能繼續使用API。 有關生成訪問令牌的詳細資訊，請參閱 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 如何使用查詢參數？ {#how-do-i-user-query-parameters}

部分 [!DNL Platform] API端點接受查詢參數以定位特定資訊並過濾在響應中返回的結果。 查詢參數將附加在帶有問號(`?`)符號，後跟一個或多個查詢參數，使用格式 `paramName=paramValue`。 在單個調用中組合多個參數時，必須使用「和」符號(`&`)以分離各個參數。 下面的示例演示如何使用多個查詢參數的請求在文檔中的表示方式。

常用查詢參數的示例包括：

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

有關特定服務或端點可用的查詢參數的詳細資訊，請查看特定於服務的文檔。

## 如何指示要在PATCH請求中更新的JSON欄位？ {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

許多PATCH操作 [!DNL Platform] API使用 [JSON指針](https://tools.ietf.org/html/rfc6901) 字串，以指示要更新的JSON屬性。 這些通常包含在請求負載中，使用 [JSON修補程式](https://tools.ietf.org/html/rfc6902) 的子菜單。 查看 [API基礎指南](api-fundamentals.md) 的子菜單。

## 我能用Postman打電話給 [!DNL Platform] API? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) 是用於可視化對REST風格API的調用的有用工具。 的 [平台API入門指南](api-guide.md) 包含用於導入Postman收藏的視頻和說明。 此外，還提供了每項服務的Postman收藏清單。

## 系統要求 [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

根據您是使用UI還是API，應用以下系統要求：

**對於基於UI的操作：**
- 現代標準的Web瀏覽器。 而 [!DNL Chrome] 建議，當前和以前的主要版本 [!DNL Firefox]。 [!DNL Internet Explorer]，也支援Safari。
   - 每次新的主版本發佈， [!DNL Platform] 開始支援最新版本，同時放棄對第三個最新版本的支援。
- 所有瀏覽器都必須啟用Cookie和JavaScript。

**對於API和開發人員交互：**
- 為REST、流和Webhook整合開發的開發環境。

## 錯誤和故障排除 {#errors-and-troubleshooting}

以下是使用任何 [!DNL Experience Platform] 服務。 有關各個故障排除指南的資訊 [!DNL Platform] 服務，請參閱 [服務疑難解答目錄](#service-troubleshooting-directory) 下。

## API狀態代碼 {#api-status-codes}

在任何 [!DNL Experience Platform] API。 各有各種原因，因此本節的解釋具有一般性。 有關單個中特定錯誤的詳細資訊 [!DNL Platform] 服務，請參閱 [服務疑難解答目錄](#service-troubleshooting-directory) 下。

| 狀態代碼 | 說明 | 可能的原因 |
|--- | --- | ---|
| 400 | 錯誤請求 | 請求構造不正確、缺少關鍵資訊和/或包含不正確的語法。 |
| 401 | 身份驗證失敗 | 請求未通過身份驗證檢查。 您的訪問令牌可能丟失或無效。 查看 [OAuth標籤錯誤](#oauth-token-is-missing) 的子菜單。 |
| 403 | 禁止 | 已找到該資源，但您沒有查看該資源的正確憑據。 |
| 404 | 未找到 | 在伺服器上找不到請求的資源。 資源可能已被刪除，或請求的路徑輸入不正確。 |
| 500 | 內部伺服器錯誤 | 這是伺服器端錯誤。 如果同時進行許多調用，則可能已達到API限制，需要篩選結果。 (請參閱 [!DNL Catalog Service] API開發人員指南子指南 [過濾資料](../catalog/api/filter-data.md) 瞭解更多資訊。) 請等待片刻，然後再次嘗試您的請求，如果問題仍然存在，請與管理員聯繫。 |

## 請求標頭錯誤 {#request-header-errors}

中的所有API調用 [!DNL Platform] 需要特定的請求標頭。 要查看各個服務需要哪些標頭，請參閱 [API參考文檔](https://www.adobe.com/go/platform-api-reference-en)。 要查找所需驗證標頭的值，請參閱 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 如果在進行API調用時丟失或無效這些標頭中的任何一個，則可能會出現以下錯誤。

### 缺少OAuth令牌 {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

當 `Authorization` API請求中缺少標頭。 在重試之前，請確保授權標頭包含有效的訪問令牌。

### OAuth令牌無效 {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

在中提供的訪問令牌 `Authorization` 標頭無效。 確保已正確輸入令牌，或 [生成新令牌](https://www.adobe.com/go/platform-api-authentication-en) 的下界。

### 需要API密鑰 {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

當API密鑰標頭(`x-api-key`)在API請求中缺失。 在重試之前，請確保標頭包含有效的API密鑰。

### API密鑰無效 {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

當提供的API密鑰標頭的值(`x-api-key`)無效。 請確保在再次嘗試之前已正確輸入密鑰。 如果您不知道您的API密鑰，則可以在 [Adobe I/O控制台](https://console.adobe.io):的 **整合** 頁籤，導航到 **概述** 的子目錄。 **客戶端憑據**。

### 缺少標題 {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

當組織標題(`x-gw-ims-org-id`)在API請求中缺失。 在重試之前，請確保頭包含在您組織的ID中。

### 配置檔案無效 {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

當用戶或Adobe I/O整合(由 [訪問令牌](#how-do-i-get-an-access-token) 的 `Authorization` 頭)無權撥打 [!DNL Experience Platform] 中提供的組織的API `x-gw-ims-org-id` 標題。 在重試之前，請確保在標題中為組織提供了正確的ID。 如果您不知道您的組織ID，可以在 [Adobe I/O控制台](https://console.adobe.io):的 **整合** 頁籤，導航到 **概述** 的ID **客戶端憑據**。

### 刷新etag錯誤 {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

如果其他API調用方對任何源實體或目標實體（如流、連接、源連接器或目標連接）進行了更改，則可能會收到etag錯誤。 由於版本不匹配，您嘗試進行的更改將不會應用於實體的最新版本。

要解決此問題，您需要再次獲取實體，確保更改與實體的新版本相容，然後將新etag放在 `If-Match` 頭，最後進行API調用。

### 未指定有效的內容類型 {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

當POST、PUT或PATCH請求無效或丟失時，將顯示此錯誤消息 `Content-Type` 標題。 確保在請求中包含報頭，並且其值 `application/json`。

### 用戶區域缺失 {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

以下兩種情況中的一種顯示此錯誤消息：
- 當組織ID標頭不正確或格式不正確時(`x-gw-ims-org-id`)。 在重試之前，請確保包含您組織的正確ID。
- 當您的帳戶（如所提供的身份驗證憑據所表示）未與產品配置檔案關聯以進行Experience Platform時。 按照上的步驟操作 [生成訪問憑據](./api-authentication.md#authentication-for-each-session) 在平台API驗證教程中，將平台添加到您的帳戶並相應地更新您的驗證憑據。

## 服務疑難解答目錄 {#service-troubleshooting-directory}

以下是故障排除指南和API參考文檔的清單 [!DNL Experience Platform] API。 每個故障排除指南都提供針對特定問題的常見問題和解決方案的答案 [!DNL Platform] 服務。 API參考文檔提供了每個服務的所有可用端點的全面指南，並顯示您可能接收的示例請求體、響應和錯誤代碼。

| 服務 | API 參考 | 疑難排解 |
| --- | --- | --- |
| 存取控制 | [訪問控制API](https://www.adobe.io/experience-platform-apis/references/access-control/) | [訪問控制故障排除指南](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform資料接收 | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [批量攝取故障排除指南](../ingestion/batch-ingestion/troubleshooting.md) |
| Adobe Experience Platform資料接收 | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [流攝入故障排除指南](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform資料科學工作區 | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] 故障排除指南](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform資料治理 | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] 故障排除指南](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform查詢服務 | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] 故障排除指南](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform分割 | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] 常見問題解答和故障排除指南](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] 和 [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] 故障排除指南](../profile/troubleshooting.md) |
| 沙箱 | [沙盒API](https://www.adobe.io/experience-platform-apis/references/sandbox) | [沙箱故障排除指南](../sandboxes/troubleshooting-guide.md) |
