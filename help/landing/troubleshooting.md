---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform常見問答集與疑難排解指南
topic: getting started
translation-type: tm+mt
source-git-commit: d9aa21a7439a6c40f6f51dfbdf5c7b3690c4593a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 平台常見問答集與疑難排解指南

本檔案提供有關Adobe Experience Platform的常見問題解答，以及任何Experience Platform API中常見錯誤的高階疑難排解指南。 如需個別平台服務的疑難排解指南，請參閱下 [列服務疑難排解目錄](#service-troubleshooting-directory) 。

## 常見問題集 {#faq}

以下是有關Adobe Experience Platform常見問題的解答清單。

## 什麼是Experience Platform API? {#what-are-experience-platform-apis}

Experience Platform提供多個REST風格的API，可使用HTTP請求存取平台資源。 這些服務API每個都會顯示多個端點，並允許您執行列出(GET)、查閱(GET)、編輯（PUT和／或修補）和刪除(DELETE)資源的操作。 如需每項服務可用之特定端點和作業的詳細資訊，請參閱Adobe I/O的 [API參考檔案](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) 。

## 如何設定API要求的格式？ {#how-do-i-format-an-api-request}

請求格式會依使用的平台API而異。 瞭解如何建構API呼叫的最佳方式，是依循您所使用之特定平台服務檔案中提供的範例。

### 閱讀範例API呼叫

Experience Platform的檔案以兩種不同的方式顯示範例API呼叫。 首先，呼叫以其 **API格式呈現**，其範本表示僅顯示操作(GET、POST、PUT、PATCH、DELETE)和所使用的端點(例如 `/global/classes`)。 某些範本也會顯示變數的位置，以協助說明如何制定呼叫，例如 `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`。

然後，呼叫會在 **Request**（請求）中顯示為cURL命令，其中包含成功與API互動所需的必要標題和完整「基本路徑」。 基本路徑應預先附加到所有端點。 例如，前述端點 `/global/classes` 變為 `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`。 您會在整個檔案中看到API格式／請求模式，而且在對平台API進行自己的呼叫時，預期會使用範例「請求」中顯示的完整路徑。

### 範例API要求

以下是範例API要求，示範您將在檔案中遇到的格式。

**API格式**

API格式顯示操作(GET)和所使用的端點。 變數會以大括弧表示(在本例中為 `{CONTAINER_ID}`)。

```http
GET /{CONTAINER_ID}/classes
```

**請求**

在此範例請求中，API格式的變數會在請求路徑中指定實際值。 所有必要的標題也會顯示，例如範例標題值或應包含敏感資訊（例如安全性Token和存取ID）的變數。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應說明在成功呼叫API後，您會根據所傳送的請求收到什麼。 有時候，回應會因空間而截斷，這表示您可能會看到範例中顯示的更多資訊或其他資訊。

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

如需平台API中特定端點的詳細資訊，包括必要的標題和要求主體，請參閱 [API參考檔案](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)。

## 我的IMS組織是什麼？ {#what-is-my-ims-organization}

IMS組織是客戶的Adobe代表。 任何授權的Adobe解決方案皆與此客戶組織整合。 當IMS組織有權使用Experience Platform時，它可指派存取權給開發人員。 IMS組織ID(`x-gw-ims-org-id`)代表應執行API呼叫的組織，因此是所有API請求中的標題。 此ID可透過 [Adobe Developer Console找到](https://www.adobe.com/go/devs_console_ui): 在「整 **合** 」標籤中，導覽至任何特定整合的「概述」區段，以在「用戶端認證」下尋找 **ID******。 如需如何驗證至平台的逐步逐步說明，請參閱驗 [證教學課程](../tutorials/authentication.md)。

## 我可以在哪裡找到API金鑰？ {#where-can-i-find-my-api-key}

所有API請求中都需要API金鑰作為標題。 您可從 [Adobe Developer Console找到它](https://www.adobe.com/go/devs_console_ui)。 在主控台的「整合 **」索引標籤上，導覽至特定整合的「概述** 」區段，然後在「用戶端認證」下方找到 **金鑰******。 如需如何驗證至平台的逐步逐步說明，請參閱驗 [證教學課程](../tutorials/authentication.md)。

## 我要如何取得存取Token? {#how-do-i-get-an-access-token}

所有API呼叫的「授權」標題中都需要存取Token。 只要您擁有IMS組織 `curl` 整合的存取權，就可以使用命令產生。 存取Token僅有24小時有效，之後必須產生新Token才能繼續使用API。 如需有關產生存取Token的詳細資訊，請參閱驗 [證教學課程](../tutorials/authentication.md)。

## 如何使用查詢參數？ {#how-do-i-user-query-parameters}

有些平台API端點會接受查詢參數，以找出特定資訊並篩選回應中傳回的結果。 查詢參數會附加至具有問號(`?`)符號的請求路徑，後面接著一或多個使用該格式的查詢參數 `paramName=paramValue`。 在單一呼叫中結合多個參數時，您必須使用&amp;符號(`&`)來分隔個別參數。 下列範例說明如何使用多個查詢參數的請求在檔案中呈現。

常用查詢參數的範例包括：

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

有關特定服務或端點可使用哪些查詢參數的詳細資訊，請參閱特定服務的文檔。

## 如何在PATCH請求中指定要更新的JSON欄位？ {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

平台API中的許多PATCH作業都使 [用JSON指標字串](https://tools.ietf.org/html/rfc6901) ，以指出要更新的JSON屬性。 這些通常會包含在使用 [JSON修補程式格式的請求載入中](https://tools.ietf.org/html/rfc6902) 。 如需這些 [技術所需語法的詳細資訊](api-fundamentals.md) ，請參閱API基礎指南。

## 我可以使用Postman呼叫平台API嗎？ {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.getpostman.com/) 是一種實用的工具，用於可視化對REST風格API的調用。 此 [中篇貼文](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) ，說明如何設定Postman以自動執行驗證，並使用它來使用Experience Platform API。

## 平台的系統需求為何？ {#what-are-the-system-requirements-for-platform}

視您使用的是UI或API而定，會套用下列系統需求：

**對於基於UI的操作：**
- 現代化、標準的網頁瀏覽器。 雖然建議使用最新版Chrome，但也支援目前和舊版的Firefox、Internet Explorer和Safari。
   - 每次發行新的主要版本時，平台就會開始支援最新版本，而放棄支援最新的第三個版本。
- 所有瀏覽器都必須啟用Cookie和JavaScript。

**針對API和開發人員互動：**
- 針對REST、串流和Webhook整合進行開發的開發環境。

## 錯誤和疑難排解 {#errors-and-troubleshooting}

以下是您使用任何Experience Platform服務時可能遇到的錯誤清單。 如需個別平台服務的疑難排解指南，請參閱下 [列服務疑難排解目錄](#service-troubleshooting-directory) 。

## API狀態代碼 {#api-status-codes}

在任何Experience Platform API上都可能遇到下列狀態代碼。 每個原因都有各種原因，因此本節中的解釋是一般性的。 有關個別平台服務中特定錯誤的詳細資訊，請參閱以下 [服務疑難排解目錄](#service-troubleshooting-directory) 。

| 狀態代碼 | 說明 | 可能的原因 |
--- | --- | ---
| 400 | 錯誤請求 | 請求的建構不當、遺失關鍵資訊及／或語法不正確。 |
| 401 | 驗證失敗 | 請求未通過驗證檢查。 您的存取Token可能遺失或無效。 如需詳細 [資訊，請參閱下方](#oauth-token-is-missing) 「OAuth Token錯誤」一節。 |
| 403 | 禁止 | 已找到資源，但您沒有查看該資源的正確憑據。 |
| 404 | 找不到 | 在伺服器上找不到所請求的資源。 資源可能已刪除，或請求的路徑輸入錯誤。 |
| 500 | 內部伺服器錯誤 | 這是伺服器端錯誤。 如果您同時進行許多呼叫，可能已達到API限制，需要篩選結果。 (如需詳細資訊，請參閱Catalog Service API開發人員指南中 [的資料篩選](../catalog/api/filter-data.md) 子指南)。 請稍候片刻，然後再次嘗試您的請求，如果問題仍然存在，請聯絡您的管理員。 |

## 請求標題錯誤 {#request-header-errors}

平台中的所有API呼叫都需要特定的請求標題。 若要查看個別服務需要哪些標題，請參閱 [API參考檔案](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)。 若要尋找所需驗證標題的值，請參閱驗 [證教學課程](../tutorials/authentication.md)。 如果在進行API呼叫時這些標題中有任何遺失或無效，可能會發生下列錯誤。

### 遺失OAuth代號 {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

當API請求中遺失標 `Authorization` 題時，會顯示此錯誤訊息。 在再次嘗試之前，請確定授權標題已包含有效的存取Token。

### OAuth Token無效

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

當標題中提供的存取Token無效時，會 `Authorization` 顯示此錯誤訊息。 請確定Token已正確輸入，或 [在Adobe I/O Console中產生](../tutorials/authentication.md) 新Token。

### 需要API金鑰

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

當API請求中遺失API金鑰標`x-api-key`題()時，會顯示此錯誤訊息。 請先確定標題已包含有效的API金鑰，然後再再試一次。

### API金鑰無效

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

當提供的API金鑰標題(`x-api-key`)的值無效時，會顯示此錯誤訊息。 請確定您已正確輸入密鑰，然後再次嘗試。 如果您不知道您的API金鑰，可在 [Adobe I/O Console中找到它](https://console.adobe.io): 在「整 **合** 」索引標籤中，導覽至特定整合的「概述」區段，以在「用戶端認證」下尋找API **金鑰******。


### 遺失標題

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

當API請求中遺失IMS組織標題(`x-gw-ims-org-id`)時，會顯示此錯誤訊息。 請確定標題已包含在您IMS組織的ID中，然後再試一次。

### 描述檔無效

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

當使用者或Adobe I/O整合(由標題中的 [存取Token](#how-do-i-get-an-access-token) )無權呼叫標題中提供之IMS組織的Experience Platform API時，會顯示此錯誤 `Authorization``x-gw-ims-org-id` 訊息。 請確定您已在頁首中為您的IMS組織提供正確的ID，然後再次嘗試。 如果您不知道您的組織ID，可在 [Adobe I/O主控台中找到它](https://console.adobe.io): 在「整 **合** 」索引標籤中，導覽至特定整合的「概述 **」區段，以在「用戶端認證」下尋找** ID ****。

### 未指定有效的內容類型

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

當POST、PUT或PATCH請求的標題無效或遺失時，會顯示此錯誤 `Content-Type` 訊息。 請確定請求中包含標題，且其值為 `application/json`。


## 服務疑難排解目錄 {#service-troubleshooting-directory}

以下是Experience Platform API的疑難排解指南和API參考檔案清單。 每個疑難排解指南都提供常見問題的解答，以及個別平台服務特定問題的解決方案。 API參考檔案提供每個服務所有可用端點的完整指南，並顯示您可能收到的範例要求主體、回應和錯誤碼。

| 服務 | API 參考 | 疑難排解 |
--- | --- | ---
| 存取控制 | [存取控制API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [存取控制疑難排解指南](../access-control/troubleshooting-guide.md) |
| 目錄 | [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| 資料擷取（批次） | [資料擷取API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [批次擷取疑難排解指南](../ingestion/batch-ingestion/troubleshooting.md) |
| 資料擷取（串流） | [資料擷取API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [串流擷取疑難排解指南](../ingestion/streaming-ingestion/troubleshooting.md) |
| 資料科學工作區 | [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [Data Science Workspace疑難排解指南](../data-science-workspace/troubleshooting-guide.md) |
| 資料使用標籤與實施(DULE) | [DULE Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| 體驗資料模型(XDM) | [方案註冊表API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [XDM系統常見問答集和疑難排解指南](../xdm/troubleshooting-guide.md) |
| Identity 服務 | [Identity Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [Identity Service疑難排解指南](../identity-service/troubleshooting-guide.md) |
| 查詢服務 | [查詢服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [查詢服務疑難排解指南](../query-service/troubleshooting-guide.md) |
| 即時客戶個人檔案 | [即時客戶個人檔案API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) |  |
| 沙盒 | [沙盒API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [沙盒疑難排解指南](../sandboxes/troubleshooting-guide.md) |
| 區段 | [區段API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |