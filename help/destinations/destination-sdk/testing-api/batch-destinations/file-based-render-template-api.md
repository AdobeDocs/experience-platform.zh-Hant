---
description: 本頁介紹如何使用/authoring/testing/template/render終結點來直觀顯示在目標配置中定義的模板化客戶資料欄位的外觀。
title: 驗證模板化客戶欄位
exl-id: 8ed93f0c-3439-4d11-bb2f-d417a1e0b6a8
source-git-commit: 6bd169075cd3826ae2a0907e6e624fd901076a4a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---


# 驗證模板化客戶欄位

## 總覽 {#overview}

的 `/authoring/testing/template/render` 端點可幫助您直觀地顯示模板化方式 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 在目標配置中定義。

終結點為客戶資料欄位生成隨機值，並在響應中返回這些值。 這有助於驗證客戶資料欄位的語義結構，如儲存段名稱或資料夾路徑。

## 快速入門 {#getting-started}

在繼續之前，請查看 [入門指南](../../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 先決條件 {#prerequisites}

在使用 `/template/render` 端點，確保滿足以下條件：

* 您通過Destination SDK建立了一個現有的基於檔案的目標，您可以在 [目標目錄](../../../ui/destinations-workspace.md)。
* 要成功發出API請求，您需要與要測試的目標實例對應的目標實例ID。 在平台UI中瀏覽與目標的連接時，從URL獲取在API調用中應使用的目標實例ID。

   ![顯示如何從URL獲取目標實例ID的UI影像。](../../assets/testing-api/get-destination-instance-id.png)

## 呈現模板化客戶欄位 {#render-customer-fields}

**API格式**

```http
POST /authoring/testing/template/render/destination
```

要說明此API終結點的行為，讓我們考慮具有以下客戶資料欄位配置的基於檔案的目標：

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

以下請求調用 `/authoring/testing/template/render` endpoint ，它返回具有隨機生成的上述兩個客戶資料欄位值的響應。

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
| `destinationId` | 的ID [目標配置](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 你正在測試。 |
| `templates` | 在您的 [目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md)。 |

**回應**

成功的響應返回 `HTTP 200 OK` 狀態，並且主體包含模板化欄位的隨機生成值。

此響應可以幫助您驗證客戶資料欄位的正確結構，如儲存段名稱或資料夾路徑。


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟 {#next-steps}

閱讀此文檔後，您現在知道如何驗證在您的 [目標伺服器](../../authoring-api/destination-server/create-destination-server.md)。
