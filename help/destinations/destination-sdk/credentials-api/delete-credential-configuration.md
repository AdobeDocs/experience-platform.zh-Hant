---
description: 此頁面是用來刪除認證設定Adobe Experience Platform Destination SDK的API呼叫的範例。
title: 刪除認證設定
exl-id: a540e349-043c-4f04-8ca8-f650b9943492
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# 刪除認證設定

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/credentials`

此頁面是您可用來刪除認證設定的API要求與裝載範例，使用 `/authoring/credentials` api端點。

## 何時使用 `/credentials` API端點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，您 ***不要*** 需要使用 `/credentials` api端點。 您可以改為透過以下方式設定目的地的驗證資訊： `customerAuthenticationConfigurations` 的引數 `/destinations` 端點。
> 
>讀取 [客戶驗證設定](../functionality/destination-configuration/customer-authentication.md) 以取得支援驗證型別的詳細資訊。

只有在Adobe和您的目的地平台之間存在全域驗證系統，而且 [!DNL Platform] 客戶不需要提供任何驗證認證即可連線至您的目的地。 在此情況下，您必須使用 `/credentials` api端點。

使用全域驗證系統時，您必須設定 `"authenticationRule":"PLATFORM_AUTHENTICATION"` 在 [目的地傳遞](../functionality/destination-configuration/destination-delivery.md) 設定，當 [建立新的目的地組態](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值如下 **區分大小寫**. 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 認證API操作快速入門 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 如需您成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 刪除認證設定 {#delete}

您可以刪除 [現有](create-credential-configuration.md) 認證設定，透過發出 `DELETE` 要求給 `/authoring/credentials` 端點與 `{INSTANCE_ID}`您要刪除的認證設定的ID。

若要取得現有的目的地組態及其對應組態 `{INSTANCE_ID}`，請參閱「 」一文，瞭解 [擷取認證設定](retrieve-credential-configuration.md).

**API格式**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 此 `ID` 您要刪除的認證設定的。 |

以下請求會刪除由定義的認證組態 `{INSTANCE_ID}` 引數。

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

成功的回應會傳回HTTP狀態200以及空的HTTP回應。

+++

## API錯誤處理 {#error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何使用 `/authoring/credentials` api端點。 讀取 [如何使用Destination SDK來設定您的目的地](../guides/configure-destination-instructions.md) 以瞭解此步驟在設定目的地的程式中的適用位置。
