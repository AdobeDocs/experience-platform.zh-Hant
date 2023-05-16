---
description: 本頁說明透過Adobe Experience Platform Destination SDK刪除現有目標伺服器設定的API呼叫。
title: 刪除目標伺服器配置
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---


# 刪除目標伺服器配置

此頁面是API要求和裝載的範例，您可使用來刪除現有的目的地伺服器設定 `/authoring/destination-servers` API端點。

如需可透過此端點刪除之功能的詳細說明，請參閱下列文章：

* [使用Destination SDK建立的目的地的伺服器規格](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [使用Destination SDK建立的目的地的範本規格](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [訊息格式](../../../destination-sdk/functionality/destination-server/message-format.md)
* [檔案格式設定](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 目標伺服器API操作快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 刪除目標伺服器配置 {#delete}

您可以刪除 [現有](create-destination-server.md) 目標伺服器配置，方法是： `DELETE` 請求 `/authoring/destination-servers` 端點為 `{INSTANCE_ID}`目標伺服器配置（要刪除）。

>[!TIP]
>
>**API端點**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

獲取現有目標伺服器配置及其相應配置 `{INSTANCE_ID}`，請參閱關於 [檢索目標伺服器配置](retrieve-destination-server.md).

**API格式**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 此 `ID` 要刪除的目標伺服器配置。 |

+++請求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++回應

成功的回應會傳回HTTP狀態200，並傳回空的HTTP回應。

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何透過Destination SDK刪除現有的目標伺服器 `/authoring/destination-servers` API端點。

若要進一步了解您可以使用此端點執行的操作，請參閱下列文章：

* [建立目標伺服器配置](create-destination-server.md)
* [檢索目標伺服器配置](retrieve-destination-server.md)
* [更新目標伺服器配置](update-destination-server.md)

