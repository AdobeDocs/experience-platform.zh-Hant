---
description: 此頁面是用來刪除憑證設定Adobe Experience Platform Destination SDK的API呼叫的範例。
title: 刪除憑據配置
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---


# 刪除憑據配置

>[!IMPORTANT]
>
>**API端點**: `platform.adobe.io/data/core/activation/authoring/credentials`

此頁面是API要求和裝載的範例，您可以用來刪除憑證設定，使用 `/authoring/credentials` API端點。

## 何時使用 `/credentials` API端點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，您 ***不*** 需要使用 `/credentials` API端點。 反之，您可以透過 `customerAuthenticationConfigurations` 參數 `/destinations` 端點。
> 
>閱讀 [客戶驗證配置](../functionality/destination-configuration/customer-authentication.md) 以取得支援驗證類型的詳細資訊。

只有在Adobe與目的地平台之間有全域驗證系統，且 [!DNL Platform] 客戶不需要提供任何驗證憑證來連線至您的目的地。 在這種情況下，您必須使用 `/credentials` API端點。

使用全局身份驗證系統時，必須設定 `"authenticationRule":"PLATFORM_AUTHENTICATION"` 在 [目的地傳送](../functionality/destination-configuration/destination-delivery.md) 配置時 [建立新目標配置](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 憑證API操作快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 刪除憑據配置 {#delete}

您可以刪除 [現有](create-credential-configuration.md) 通過建立 `DELETE` 請求 `/authoring/credentials` 端點為 `{INSTANCE_ID}`的憑據配置。

要獲取現有目標配置及其對應 `{INSTANCE_ID}`，請參閱關於 [檢索憑據配置](retrieve-credential-configuration.md).

**API格式**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 此 `ID` 要刪除的憑據配置。 |

以下請求將刪除由 `{INSTANCE_ID}` 參數。

+++請求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

閱讀本檔案後，您現在知道如何使用 `/authoring/credentials` API端點。 閱讀 [如何使用Destination SDK來設定您的目的地](../guides/configure-destination-instructions.md) 了解此步驟在設定目的地程式中的適用位置。
