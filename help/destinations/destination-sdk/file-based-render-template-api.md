---
description: 本頁說明如何使用/authoring/testing/template/render端點來視覺化目標配置中定義的模板化客戶資料欄位的外觀。
title: 驗證範本化客戶欄位
exl-id: 8ed93f0c-3439-4d11-bb2f-d417a1e0b6a8
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---

# 驗證範本化客戶欄位

## 總覽 {#overview}

此 `/authoring/testing/template/render` 端點可協助您將範本化情形視覺化 [客戶資料欄位](file-based-destination-configuration.md#customer-data-fields) 在目的地設定中定義的結果會類似。

端點會為您的客戶資料欄位產生隨機值，並在回應中傳回。 這可協助您驗證客戶資料欄位的語義結構，例如貯體名稱或資料夾路徑。

## 快速入門 {#getting-started}

繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 先決條件 {#prerequisites}

您可以使用 `/template/render` 端點，確定您符合下列條件：

* 您已透過Destination SDK建立現有的檔案型目的地，並可在 [目的地目錄](../ui/destinations-workspace.md).
* 若要成功提出API請求，您需要與要測試的目的地執行個體對應的目的地執行個體ID。 在Platform UI中瀏覽與目的地的連線時，從URL取得應用於API呼叫的目的地執行個體ID。

   ![顯示如何從URL取得目的地執行個體ID的UI影像。](assets/get-destination-instance-id.png)

## 呈現範本化客戶欄位 {#render-customer-fields}

**API格式**

```http
POST /authoring/testing/template/render/destination
```

為了說明此API端點的行為，讓我們考慮使用下列客戶資料欄位設定的檔案型目的地：

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

以下請求會呼叫 `/authoring/testing/template/render` 端點，會針對上述兩個客戶資料欄位，以隨機產生的值傳回回應。

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
| `destinationId` | 的ID [目的地配置](file-based-destination-configuration.md) 你在測試。 |
| `templates` | 在您的 [目標伺服器配置](server-and-file-configuration.md). |

**回應**

成功的回應會傳回 `HTTP 200 OK` 狀態，而內文則包含範本欄位的隨機產生值。

此回應可協助您驗證客戶資料欄位（例如貯體名稱或資料夾路徑）的正確結構。


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何驗證中定義的客戶資料欄位設定 [目的地伺服器](server-and-file-configuration.md).
