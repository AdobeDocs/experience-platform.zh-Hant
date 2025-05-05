---
description: 此頁面是用來刪除認證設定Adobe Experience Platform Destination SDK的API呼叫的範例。
title: 刪除認證設定
exl-id: a540e349-043c-4f04-8ca8-f650b9943492
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 1%

---

# 刪除認證設定

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/credentials`

此頁面是您可用來使用`/authoring/credentials` API端點刪除認證組態的API要求與裝載範例。

## 何時使用`/credentials` API端點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，您&#x200B;***不***&#x200B;需要使用`/credentials` API端點。 您可以改為透過`/destinations`端點的`customerAuthenticationConfigurations`引數來設定您目的地的驗證資訊。
> 
>閱讀[客戶驗證組態](../functionality/destination-configuration/customer-authentication.md)，以取得支援的驗證型別的詳細資訊。

只有在Adobe和您的目的地平台之間有全域驗證系統，且[!DNL Experience Platform]客戶不需要提供任何驗證認證即可連線至您的目的地時，才使用此API端點來建立認證設定。 在此情況下，您必須使用`/credentials` API端點建立認證組態。

使用全域驗證系統時，在[建立新的目的地組態](../authoring-api/destination-configuration/create-destination-configuration.md)時，您必須在[目的地傳遞](../functionality/destination-configuration/destination-delivery.md)組態中設定`"authenticationRule":"PLATFORM_AUTHENTICATION"`。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都會區分大小寫&#x200B;**&#x200B;**。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 認證API操作快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 刪除認證設定 {#delete}

您可以透過您要刪除認證組態的`{INSTANCE_ID}`向`/authoring/credentials`端點發出`DELETE`要求，以刪除[現有](create-credential-configuration.md)認證組態。

若要取得現有的目的地組態及其對應的`{INSTANCE_ID}`，請參閱有關[擷取認證組態](retrieve-credential-configuration.md)的文章。

**API格式**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 您要刪除的認證組態的`ID`。 |

下列要求會刪除`{INSTANCE_ID}`引數定義的認證組態。

+++要求

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

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟 {#next-steps}

閱讀此檔案後，您現在知道如何使用`/authoring/credentials` API端點刪除認證設定。 閱讀[如何使用Destination SDK來設定您的目的地](../guides/configure-destination-instructions.md)，以瞭解此步驟在設定目的地的程式中的位置。
