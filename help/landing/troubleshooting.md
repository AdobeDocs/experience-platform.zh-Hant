---
keywords: Experience Platform；首頁；熱門主題；API錯誤碼；API錯誤碼；錯誤碼API；錯誤碼API;API要求錯誤；API疑難排解；API錯誤
solution: Experience Platform
title: Adobe Experience Platform常見問題集和疑難排解指南
description: 尋找常見問題的解答，以及針對 Experience Platform 中的常見錯誤進行疑難排解的指南。
landing-page-description: 尋找常見問題的解答，以及針對 Experience Platform 中的常見錯誤進行疑難排解的指南。
topic-legacy: getting started
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: b47a52920f82a962ff044a0dacf9777b6eeae447
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 4%

---

# [!DNL Platform] 常見問題集和疑難排解指南

本檔案提供Adobe Experience Platform常見問題的解答，以及任何[!DNL Experience Platform] API中可能遇到的常見錯誤的高階疑難排解指南。 有關單個[!DNL Platform]服務的疑難解答指南，請參閱下面的[服務疑難解答目錄](#service-troubleshooting-directory)。

## 常見問題集 {#faq}

以下是關於Adobe Experience Platform常見問題的解答清單。

## 什麼是[!DNL Experience Platform] API? {#what-are-experience-platform-apis}

[!DNL Experience Platform] 提供多個RESTful API，可使用HTTP請求來存取 [!DNL Platform] 資源。這些服務API分別會公開多個端點，並可讓您執行列出(GET)、查詢(GET)、編輯(PUT和/或PATCH)和刪除(DELETE)資源的作業。 有關每個服務可用的特定端點和操作的詳細資訊，請參閱[API參考檔案](https://www.adobe.com/go/platform-api-reference-en)Adobe I/O。

## 如何設定API請求的格式？ {#how-do-i-format-an-api-request}

請求格式會依使用的[!DNL Platform] API而異。 若要了解如何建構API呼叫，最佳方式是遵循檔案中提供的範例，以了解您所使用的特定[!DNL Platform]服務。

如需設定API請求的詳細資訊，請參閱Platform API快速入門手冊[閱讀範例API呼叫](./api-guide.md#sample-api)一節。

## 什麼是我的IMS組織？ {#what-is-my-ims-organization}

IMS組織是Adobe的代表。 任何經授權的Adobe解決方案都與此客戶組織整合。 當IMS組織有權[!DNL Experience Platform]時，它可將存取權指派給開發人員。 IMS組織ID(`x-gw-ims-org-id`)代表應執行API呼叫的組織，因此在所有API請求中都是標題。 此ID可透過[Adobe開發人員控制台](https://www.adobe.com/go/devs_console_ui)找到：在&#x200B;**整合**&#x200B;標籤中，導覽至任何特定整合的&#x200B;**概述**&#x200B;區段，以在&#x200B;**用戶端憑證**&#x200B;下尋找ID。 有關如何驗證到[!DNL Platform]的逐步說明，請參閱[authentication教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 在哪裡可以找到我的API金鑰？ {#where-can-i-find-my-api-key}

所有API請求中都須有API金鑰作為標題。 可透過[Adobe開發人員控制台](https://www.adobe.com/go/devs_console_ui)找到。 在主控台內，在&#x200B;**Integrations**&#x200B;標籤上，導覽至&#x200B;**Overview**&#x200B;區段以取得特定整合，您會在&#x200B;**Client Credentials**&#x200B;下找到索引鍵。 有關如何驗證[!DNL Platform]的逐步說明，請參閱[authentication教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 如何取得存取權杖？ {#how-do-i-get-an-access-token}

所有API呼叫的「授權」標題中都需要存取權杖。 只要您擁有IMS組織整合的存取權，即可使用`curl`命令產生。 存取權杖的有效期限僅為24小時，之後必須產生新權杖，才能繼續使用API。 如需產生存取權杖的詳細資訊，請參閱[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。

## 如何使用查詢參數？ {#how-do-i-user-query-parameters}

某些[!DNL Platform] API端點會接受查詢參數，以找出特定資訊並篩選回應中傳回的結果。 查詢參數會附加至帶有問號(`?`)符號的請求路徑，後面接著一或多個使用`paramName=paramValue`格式的查詢參數。 在單一呼叫中結合多個參數時，您必須使用&amp;符號(`&`)來分隔個別參數。 下列範例將示範如何使用多個查詢參數的要求在檔案中的呈現方式。

常用的查詢參數範例包括：

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

有關特定服務或端點可用的查詢參數的詳細資訊，請查看特定服務的文檔。

## 如何在PATCH請求中指出要更新的JSON欄位？ {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

[!DNL Platform] API中的許多PATCH操作都使用[ JSON指標](https://tools.ietf.org/html/rfc6901)字串來指出要更新的JSON屬性。 這些值通常包含在使用[JSON Patch](https://tools.ietf.org/html/rfc6902)格式的要求裝載中。 如需這些技術所需語法的詳細資訊，請參閱[API基礎指南](api-fundamentals.md)。

## 我可以使用Postman來呼叫[!DNL Platform] API嗎？ {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[](https://www.postman.com/) Postman是將對RESTful API的呼叫視覺化的實用工具。[Platform API快速入門手冊](api-guide.md)包含匯入Postman集合的影片和指示。 此外，還提供每項服務的Postman集合清單。

## [!DNL Platform]的系統要求是什麼？{#what-are-the-system-requirements-for-platform}

視您使用的是UI或API而定，適用下列系統需求：

**針對以UI為基礎的作業：**
- 現代化的標準網頁瀏覽器。 雖然建議使用最新版本的[!DNL Chrome]，但也支援目前和先前的主要版本[!DNL Firefox]、[!DNL Internet Explorer]和Safari。
   - 每次發行新的主要版本時，[!DNL Platform]都會開始支援最新版本，而不再支援最新的第三個版本。
- 所有瀏覽器都必須啟用Cookie和JavaScript。

**若是API與開發人員互動：**
- 針對REST、串流和Webhook整合進行開發的開發環境。

## 錯誤和疑難排解 {#errors-and-troubleshooting}

以下是使用任何[!DNL Experience Platform]服務時可能遇到的錯誤清單。 有關單個[!DNL Platform]服務的疑難解答指南，請參閱下面的[服務疑難解答目錄](#service-troubleshooting-directory)。

## API狀態代碼 {#api-status-codes}

在任何[!DNL Experience Platform] API上可能會遇到以下狀態代碼。 每個原因各有不同，因此本節中的解釋一般性。 有關各個[!DNL Platform]服務中的具體錯誤的詳細資訊，請參閱下面的[服務疑難解答目錄](#service-troubleshooting-directory)。

| 狀態代碼 | 說明 | 可能的原因 |
|--- | --- | ---|
| 400 | 錯誤請求 | 請求的建構不正確、遺失重要資訊，和/或包含錯誤的語法。 |
| 401 | 驗證失敗 | 請求未通過驗證檢查。 您的存取權杖可能遺失或無效。 如需詳細資訊，請參閱下方的[OAuth代號錯誤](#oauth-token-is-missing)一節。 |
| 403 | 禁止 | 找到資源，但您沒有查看該資源的正確憑據。 |
| 404 | 找不到 | 在伺服器上找不到請求的資源。 資源可能已刪除，或請求的路徑輸入不正確。 |
| 500 | 內部伺服器錯誤 | 這是伺服器端錯誤。 如果您同時進行許多呼叫，可能已達到API限制，因此需要篩選結果。 （若要深入了解，請參閱[篩選資料](../catalog/api/filter-data.md)上的[!DNL Catalog Service] API開發人員指南子指南。） 請等候片刻，然後再次嘗試您的請求，如果問題仍然存在，請聯絡您的管理員。 |

## 請求標題錯誤 {#request-header-errors}

[!DNL Platform]中的所有API呼叫都需要特定的請求標題。 若要查看個別服務需要哪些標題，請參閱[ API參考檔案](https://www.adobe.com/go/platform-api-reference-en)。 若要尋找所需驗證標題的值，請參閱[Authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 如果進行API呼叫時，這些標題中有任何一個遺失或無效，可能會發生下列錯誤。

### 缺少OAuth代號 {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

當API請求中缺少`Authorization`標題時，會顯示此錯誤訊息。 再次嘗試之前，請確保Authorization標頭包含有效的存取權杖。

### OAuth代號無效

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

當`Authorization`標題中提供的存取權杖無效時，會顯示此錯誤訊息。 請確定已正確輸入代號，或在Adobe I/O主控台中產生新代號](https://www.adobe.com/go/platform-api-authentication-en)。[

### 需要API金鑰

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

當API請求中缺少API金鑰標題(`x-api-key`)時，會顯示此錯誤訊息。 再次嘗試之前，請確定標題已包含有效的API金鑰。

### API密鑰無效

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

提供的API金鑰標題(`x-api-key`)的值無效時，會顯示此錯誤訊息。 請確定您已正確輸入金鑰，然後再次嘗試。 如果您不知道您的API金鑰，可在[Adobe I/O主控台](https://console.adobe.io)中找到：在&#x200B;**整合**&#x200B;標籤中，導覽至&#x200B;**概觀**&#x200B;區段以取得特定整合，以在&#x200B;**用戶端憑證**&#x200B;下尋找API金鑰。


### 缺少標題

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

當API請求中缺少IMS組織標題(`x-gw-ims-org-id`)時，會顯示此錯誤訊息。 再次嘗試之前，請確定標題已包含在您IMS組織的ID中。

### 配置檔案無效

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

當使用者或Adobe I/O整合（由`Authorization`標題中的[存取權杖](#how-do-i-get-an-access-token)識別）無權呼叫[!DNL Experience Platform]標題中提供之IMS組織的`x-gw-ims-org-id` API時，便會顯示此錯誤訊息。 在再次嘗試之前，請確定您已在標題中為您的IMS組織提供正確的ID。 如果您不知道組織ID，可以在[Adobe I/O控制台](https://console.adobe.io)中找到：在&#x200B;**整合**&#x200B;標籤中，導覽至&#x200B;**概述**&#x200B;區段以尋找特定整合的&#x200B;**用戶端憑證**&#x200B;底下的ID。

### 未指定有效的內容類型

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

當POST、PUT或PATCH請求的標題無效或缺少`Content-Type`時，將顯示此錯誤消息。 請確定請求中包含標題，且其值為`application/json`。

### 缺少用戶區域

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

當您的帳戶（如所提供的驗證憑證所示）未與產品設定檔建立關聯以供Experience Platform時，會顯示此錯誤訊息。 請依照Platform API驗證教學課程中[產生存取憑證](./api-authentication.md#authentication-for-each-session)的步驟，將Platform新增至您的帳戶並據此更新您的驗證憑證。

## 服務故障排除目錄 {#service-troubleshooting-directory}

以下是[!DNL Experience Platform] API的疑難排解指南和API參考檔案清單。 每個故障排除指南都提供針對各[!DNL Platform]服務特定問題的常見問題解答和解決方案。 API參考檔案提供每個服務所有可用端點的完整指南，並顯示您可能收到的範例要求本文、回應和錯誤碼。

| 服務 | API 參考 | 疑難排解 |
| --- | --- | --- |
| 存取控制 | [存取控制API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [存取控制疑難排解指南](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform資料擷取 | [[!DNL Data Ingestion API]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) | [批次內嵌疑難排解](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[指南串流內嵌疑難排解指南](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] 疑難排解指南](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform資料控管 | [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] 疑難排解指南](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform查詢服務 | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] 疑難排解指南](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform Segmentation | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] 常見問題集和疑難排解指南](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] 和 [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] 疑難排解指南](../profile/troubleshooting.md) |
| 沙盒 | [沙箱API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [沙箱疑難排解指南](../sandboxes/troubleshooting-guide.md) |
