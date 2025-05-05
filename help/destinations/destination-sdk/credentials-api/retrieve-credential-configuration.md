---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK擷取認證設定的API呼叫的範例。
title: 擷取認證設定
exl-id: cec55073-6e2f-4412-a9dd-1aeb445279c0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 擷取認證設定

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/credentials`

此頁面是您可用來使用`/authoring/credentials` API端點擷取認證組態的API要求與承載的範例。

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

## 擷取認證設定 {#retrieve}

您可以對`/authoring/credentials`端點發出`GET`要求，擷取[現有](create-credential-configuration.md)認證組態。

**API格式**

使用以下API格式來擷取您帳戶的所有認證設定。

```http
GET /authoring/credentials
```

使用下列API格式來擷取由`{INSTANCE_ID}`引數定義的特定認證組態。

```http
GET /authoring/credentials/{INSTANCE_ID}
```

以下兩個要求會擷取您IMS組織的所有認證設定，或特定的認證設定，端視您是否在要求中傳遞`INSTANCE_ID`引數而定。

選取下方的每個索引標籤以檢視對應的裝載。

>[!BEGINTABS]

>[!TAB 擷取所有認證設定]

+++要求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++回應

成功的回應會根據您使用的[!DNL IMS Org ID]和沙箱名稱，傳回HTTP狀態200，其中包含您可存取的認證設定清單。 一個`instanceId`對應至一個認證組態。

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
},
{
   "instanceId":"a25bffa0-3127-4030-895d-1d1236bb3680",
   "createdDate":"2022-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2022-08-07T06:41:48.641943Z",
   "type":"basic",
   "name":"yourdestination",
   "s3Authentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

+++

>[!TAB 擷取特定的認證組態]

+++要求

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 您要擷取的認證設定ID。 |

+++

+++回應

成功的回應會傳回HTTP狀態200，其中包含與要求上提供的`instanceId`對應的認證組態的詳細資料。

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

+++

>[!ENDTABS]

## API錯誤處理 {#error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何使用`/authoring/credentials` API端點擷取認證組態的詳細資料。 閱讀[如何使用Destination SDK來設定您的目的地](../guides/configure-destination-instructions.md)，以瞭解此步驟在設定目的地的程式中的位置。
