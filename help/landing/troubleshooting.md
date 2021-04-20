---
keywords: Experience Platform;home；熱門主題；API錯誤代碼；API錯誤代碼；錯誤代碼API；錯誤代碼API;API請求錯誤；API疑難排解；API錯誤
solution: Experience Platform
title: Adobe Experience Platform常見問答集與疑難排解指南
description: 尋找常見問題的解答，以及針對 Experience Platform 中的常見錯誤進行疑難排解的指南。
landing-page-description: 尋找常見問題的解答，以及針對 Experience Platform 中的常見錯誤進行疑難排解的指南。
topic: getting started
type: Documentation
translation-type: tm+mt
source-git-commit: 83cc3ddbf067f413cb524a3a685d985d5853eafd
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 4%

---


# [!DNL Platform] 常見問答集與疑難排解指南

本檔案提供有關Adobe Experience Platform常見問題的解答，以及高階疑難排解指南，說明在任何[!DNL Experience Platform] API中可能遇到的常見錯誤。 有關各個[!DNL Platform]服務的故障排除指南，請參見下面的[服務故障排除目錄](#service-troubleshooting-directory)。

## 常見問題集 {#faq}

以下是關於Adobe Experience Platform的常見問題的解答清單。

## 什麼是[!DNL Experience Platform] API?{#what-are-experience-platform-apis}

[!DNL Experience Platform] 提供多個使用HTTP請求來存取資源的REST風格 [!DNL Platform] API。這些服務API每個都會顯示多個端點，並允許您執行列出(GET)、查閱(GET)、編輯(PUT和／或PATCH)和刪除(DELETE)資源的操作。 有關每項服務可用的特定端點和操作的詳細資訊，請參閱[API參考文檔](http://www.adobe.com/go/platform-api-reference-en)中的Adobe I/O。

## 如何設定API要求的格式？{#how-do-i-format-an-api-request}

請求格式會依使用的[!DNL Platform] API而異。 瞭解如何建構API呼叫的最佳方式，是依循您所使用之特定[!DNL Platform]服務的說明檔案中提供的範例。

如需有關建立API要求的詳細資訊，請造訪平台API快速入門手冊[閱讀範例API呼叫](./api-guide.md#sample-api)一節。

## 我的IMS組織是什麼？{#what-is-my-ims-organization}

IMS組織是客戶的Adobe表示。 任何授權的Adobe解決方案皆與此客戶組織整合。 當IMS組織有權使用[!DNL Experience Platform]時，它可指派存取權給開發人員。 IMS組織ID(`x-gw-ims-org-id`)代表應執行API呼叫的組織，因此在所有API請求中都是必要的標題。 此ID可透過[Adobe開發人員主控台](https://www.adobe.com/go/devs_console_ui)找到：在&#x200B;**Integrations**&#x200B;標籤中，導覽至&#x200B;**Overview**&#x200B;區段以取得任何特定整合，以在&#x200B;**Client Credentials**&#x200B;下尋找ID。 有關如何驗證到[!DNL Platform]的逐步說明，請參見[驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 我可以在哪裡找到API金鑰？{#where-can-i-find-my-api-key}

所有API請求中都需要API金鑰作為標題。 您可透過[Adobe開發人員主控台](https://www.adobe.com/go/devs_console_ui)找到。 在控制台內，在&#x200B;**Integrations**&#x200B;標籤上，導覽至&#x200B;**Overview**&#x200B;區段以取得特定整合，您將在&#x200B;**Client Credentials**&#x200B;下找到金鑰。 有關如何驗證到[!DNL Platform]的逐步說明，請參見[驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 我要如何取得存取Token?{#how-do-i-get-an-access-token}

所有API呼叫的「授權」標題中都需要存取Token。 只要您擁有IMS組織整合的存取權，就可使用`curl`命令產生。 存取Token僅有24小時有效，之後必須產生新Token才能繼續使用API。 有關生成訪問Token的詳細資訊，請參閱[驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。

## 如何使用查詢參數？{#how-do-i-user-query-parameters}

有些[!DNL Platform] API端點會接受查詢參數，以找出特定資訊並篩選回應中傳回的結果。 查詢參數會附加至具有問號(`?`)符號的請求路徑，後面接著使用格式`paramName=paramValue`的一或多個查詢參數。 在單一呼叫中結合多個參數時，您必須使用&amp;符號(`&`)來分隔個別參數。 下列範例說明如何使用多個查詢參數的請求在檔案中呈現。

常用查詢參數的範例包括：

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

有關特定服務或端點可使用哪些查詢參數的詳細資訊，請參閱特定服務的文檔。

## 如何在PATCH請求中指定要更新的JSON欄位？{#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

[!DNL Platform] API中的許多PATCH操作使用[JSON Pointer](https://tools.ietf.org/html/rfc6901)字串來指示要更新的JSON屬性。 這些通常包含在使用[JSON Patch](https://tools.ietf.org/html/rfc6902)格式的請求負載中。 如需這些技術所需語法的詳細資訊，請參閱[API基礎指南](api-fundamentals.md)。

## 我可以使用Postman呼叫[!DNL Platform] API嗎？{#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postmanis](https://www.postman.com/) 是可視化對REST風格的API呼叫的實用工具。[平台API快速入門手冊](api-guide.md)包含視訊和匯入Postman系列的指示。 此外，還提供每個服務的郵遞員收集清單。

## [!DNL Platform]的系統需求為何？{#what-are-the-system-requirements-for-platform}

視您使用的是UI或API而定，會套用下列系統需求：

**對於基於UI的操作：**
- 現代化、標準的網頁瀏覽器。 雖然建議使用最新版[!DNL Chrome]，但也支援目前和舊版的[!DNL Firefox]、[!DNL Internet Explorer]和Safari。
   - 每次發行新的主版本時，[!DNL Platform]會開始支援最新版本，而放棄支援第三個最新版本。
- 所有瀏覽器都必須啟用Cookie和JavaScript。

**針對API和開發人員互動：**
- 針對REST、串流和Webhook整合進行開發的開發環境。

## {#errors-and-troubleshooting}錯誤和疑難排解

以下是使用任何[!DNL Experience Platform]服務時可能遇到的錯誤清單。 有關各個[!DNL Platform]服務的故障排除指南，請參見下面的[服務故障排除目錄](#service-troubleshooting-directory)。

## API狀態代碼{#api-status-codes}

在任何[!DNL Experience Platform] API上都可能遇到以下狀態代碼。 每個原因都有各種原因，因此本節中的解釋是一般性的。 有關個別[!DNL Platform]服務中特定錯誤的詳細資訊，請參閱以下[服務疑難排解目錄](#service-troubleshooting-directory)。

| 狀態代碼 | 說明 | 可能的原因 |
--- | --- | ---
| 400 | 錯誤請求 | 請求的建構不當、遺失關鍵資訊及／或語法不正確。 |
| 401 | 驗證失敗 | 請求未通過驗證檢查。 您的存取Token可能遺失或無效。 如需詳細資訊，請參閱下方的[OAuth Token錯誤](#oauth-token-is-missing)一節。 |
| 403 | 禁止 | 已找到資源，但您沒有查看該資源的正確憑據。 |
| 404 | 找不到 | 在伺服器上找不到所請求的資源。 資源可能已刪除，或請求的路徑輸入錯誤。 |
| 500 | 內部伺服器錯誤 | 這是伺服器端錯誤。 如果您同時進行許多呼叫，可能已達到API限制，需要篩選結果。 （如需詳細資訊，請參閱[篩選資料](../catalog/api/filter-data.md)上的[!DNL Catalog Service] API開發人員指南子指南。） 請稍候片刻，然後再次嘗試您的請求，如果問題仍然存在，請聯絡您的管理員。 |

## 請求標題錯誤{#request-header-errors}

[!DNL Platform]中的所有API呼叫都需要特定的請求標題。 若要瞭解個別服務需要哪些標題，請參閱[API參考檔案](http://www.adobe.com/go/platform-api-reference-en)。 要查找所需驗證標題的值，請參閱[驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 如果在進行API呼叫時這些標題中有任何遺失或無效，可能會發生下列錯誤。

### OAuth Token遺失{#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

當API請求中缺少`Authorization`標題時，會顯示此錯誤訊息。 在再次嘗試之前，請確定授權標題已包含有效的存取Token。

### OAuth Token無效

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

當`Authorization`標題中提供的存取Token無效時，會顯示此錯誤訊息。 請確定Token已正確輸入，或[在Adobe I/O主控台中產生新Token](https://www.adobe.com/go/platform-api-authentication-en)。

### 需要API金鑰

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

當API請求中遺失API金鑰標題(`x-api-key`)時，會顯示此錯誤訊息。 請先確定標題已包含有效的API金鑰，然後再再試一次。

### API金鑰無效

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

當提供的API金鑰標題(`x-api-key`)的值無效時，會顯示此錯誤訊息。 請確定您已正確輸入密鑰，然後再次嘗試。 如果您不知道您的API金鑰，則可在[Adobe I/O控制台](https://console.adobe.io)中找到：在&#x200B;**Integrations**&#x200B;標籤中，導覽至&#x200B;**Overview**&#x200B;區段以取得特定整合，以在&#x200B;**Client Credentials**&#x200B;下尋找API金鑰。


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

當使用者或Adobe I/O整合（由`Authorization`標題中的[存取Token](#how-do-i-get-an-access-token)識別）無權呼叫[!DNL Experience Platform] API（用於`x-gw-ims-org-id`標題中提供的IMS組織）時，會顯示此錯誤訊息。 請確定您已在頁首中為您的IMS組織提供正確的ID，然後再次嘗試。 如果您不知道您的組織ID，可在[Adobe I/O控制台](https://console.adobe.io)中找到：在&#x200B;**Integrations**&#x200B;標籤中，導覽至&#x200B;**Overview**&#x200B;區段以取得特定整合，以在&#x200B;**Client Credentials**&#x200B;下尋找ID。

### 未指定有效的內容類型

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

當POST、PUT或PATCH請求的標題無效或缺少`Content-Type`標題時，將顯示此錯誤消息。 請確定請求中包含標題，且其值為`application/json`。


## 服務疑難排解目錄{#service-troubleshooting-directory}

以下是[!DNL Experience Platform] API的疑難排解指南和API參考檔案清單。 每個疑難排解指南都提供有關個別[!DNL Platform]服務所特有問題的常見問答和解決方案。 API參考檔案提供每個服務所有可用端點的完整指南，並顯示您可能收到的範例要求主體、回應和錯誤碼。

| 服務 | API 參考 | 疑難排解 |
| --- | --- | --- |
| 存取控制 | [存取控制API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [存取控制疑難排解指南](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform資料擷取 | [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [批次擷取疑難排解](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[指南串流擷取疑難排解指南](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform資料科學工作區 | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] 疑難排解指南](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform資料管理 | [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] 疑難排解指南](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform查詢服務 | [[!DNL Query Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] 疑難排解指南](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform Segmentation | [[!DNL Segmentation API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] 常見問答集與疑難排解指南](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] 和 [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] 疑難排解指南](../profile/troubleshooting.md) |
| 沙盒 | [沙盒API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [沙盒疑難排解指南](../sandboxes/troubleshooting-guide.md) |

