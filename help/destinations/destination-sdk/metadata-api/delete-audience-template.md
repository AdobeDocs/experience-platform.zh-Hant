---
description: 本頁說明透過Adobe Experience Platform Destination SDK刪除現有對象範本所使用的API呼叫。
title: 刪除對象範本
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---


# 刪除對象範本

>[!IMPORTANT]
>
>**API端點**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

此頁面是API要求和裝載的範例，您可使用 `/authoring/audience-templates` API端點。

如需可透過此端點設定的功能詳細說明，請參閱 [對象中繼資料管理](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 對象範本API操作快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 刪除對象範本 {#delete}

您可以刪除 [現有](create-audience-template.md) 透過建立 `DELETE` 請求 `/authoring/audience-templates` 端點為 `{INSTANCE_ID}`對象範本中。

若要取得現有的對象範本及其對應 `{INSTANCE_ID}`，請參閱關於 [擷取對象範本](retrieve-audience-template.md).

**API格式**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 此 `ID` 對象範本中。 |

+++請求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++回應

成功的回應會傳回HTTP狀態200，並傳回空的HTTP回應。

+++

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何使用 `/authoring/audience-templates` API端點。 閱讀 [如何使用Destination SDK來設定您的目的地](../guides/configure-destination-instructions.md) 了解此步驟在設定目的地程式中的適用位置。
