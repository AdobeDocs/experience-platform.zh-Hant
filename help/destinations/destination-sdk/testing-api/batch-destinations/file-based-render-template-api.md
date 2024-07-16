---
description: 此頁面說明如何使用/authoring/testing/template/render端點，以視覺效果呈現目的地設定中定義的範本化客戶資料欄位外觀。
title: 驗證範本化客戶欄位
exl-id: 8ed93f0c-3439-4d11-bb2f-d417a1e0b6a8
source-git-commit: 6bd169075cd3826ae2a0907e6e624fd901076a4a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---


# 驗證範本化客戶欄位

## 概觀 {#overview}

`/authoring/testing/template/render`端點可協助您視覺化目的地設定中定義的範本[客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md)的外觀。

端點會產生客戶資料欄位的隨機值，並在回應中傳回。 這可幫助您驗證客戶資料欄位的語意結構，例如貯體名稱或資料夾路徑。

## 快速入門 {#getting-started}

繼續之前，請檢閱[快速入門手冊](../../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 先決條件 {#prerequisites}

在使用`/template/render`端點之前，請確定您符合下列條件：

* 您有一個透過Destination SDK建立的檔案型目的地，且您可以在[目的地目錄](../../../ui/destinations-workspace.md)中看到它。
* 若要成功提出API請求，您需要與要測試的目的地執行個體對應的目的地執行個體ID。 在Platform UI中瀏覽與目的地的連線時，從URL取得應在API呼叫中使用的目的地執行個體ID。

  ![UI影像顯示如何從URL取得目的地執行個體識別碼。](../../assets/testing-api/get-destination-instance-id.png)

## 呈現範本化客戶欄位 {#render-customer-fields}

**API格式**

```http
POST /authoring/testing/template/render/destination
```

為了說明此API端點的行為，讓我們考慮具有下列客戶資料欄位設定的檔案型目的地：

```json
"fileBasedS3Destination":{
   "bucket":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.bucket}}"
   },
   "path":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.path}}"
   }
}
```

**要求**

以下請求會呼叫`/authoring/testing/template/render`端點，而端點會針對上述兩個客戶資料欄位傳回包含隨機產生值的回應。

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render/destination' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "destinationId": "{DESTINATION_CONFIGURATION_ID}",
    "templates": {
        "bucket": "{{customerData.bucket}}",
        "path": "{{customerData.bucket}}/{{customerData.path}}"
    }
}'
```

| 參數 | 說明 |
| -------- | ----------- |
| `destinationId` | 您正在測試的[目的地組態](../../authoring-api/destination-configuration/retrieve-destination-configuration.md)的識別碼。 |
| `templates` | 在您的[目的地伺服器組態](../../authoring-api/destination-server/create-destination-server.md)中定義的範本化欄位名稱。 |

**回應**

成功的回應會傳回`HTTP 200 OK`狀態，而且內文會包含範本化欄位的隨機產生值。

此回應可協助您驗證客戶資料欄位的正確結構，例如貯體名稱或檔案夾路徑。


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## API錯誤處理 {#api-error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Platform疑難排解指南中的[API狀態碼](../../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何驗證[目的地伺服器](../../authoring-api/destination-server/create-destination-server.md)中定義的客戶資料欄位組態。
