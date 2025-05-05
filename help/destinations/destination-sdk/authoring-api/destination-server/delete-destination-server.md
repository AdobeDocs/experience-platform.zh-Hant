---
description: 此頁面是透過Adobe Experience Platform Destination SDK刪除現有目的地伺服器設定的API呼叫範例。
title: 刪除目的地伺服器設定
exl-id: 2322a2ce-220e-4590-a553-b15152412752
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 1%

---

# 刪除目的地伺服器設定

此頁面以範例說明API要求與裝載，您可以使用`/authoring/destination-servers` API端點來刪除現有的目的地伺服器組態。

如需您可透過此端點刪除的功能的詳細說明，請參閱下列文章：

* [使用Destination SDK建立之目的地的伺服器規格](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [使用Destination SDK建立之目的地的範本規格](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [訊息格式](../../../destination-sdk/functionality/destination-server/message-format.md)
* [檔案格式設定](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都會區分大小寫&#x200B;**&#x200B;**。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 開始使用目的地伺服器API作業 {#get-started}

繼續之前，請檢閱[快速入門手冊](../../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 刪除目的地伺服器設定 {#delete}

您可以刪除[現有](create-destination-server.md)目的地伺服器組態，方法是使用您要刪除之目的地伺服器組態的`{INSTANCE_ID}`向`/authoring/destination-servers`端點發出`DELETE`要求。

>[!TIP]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/destination-servers`

若要取得現有的目的地伺服器組態及其對應的`{INSTANCE_ID}`，請參閱有關[擷取目的地伺服器組態](retrieve-destination-server.md)的文章。

**API格式**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 您要刪除的目的地伺服器組態`ID`。 |

+++要求

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++回應

成功的回應會傳回HTTP狀態200以及空的HTTP回應。

## API錯誤處理 {#error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何透過Destination SDK `/authoring/destination-servers` API端點刪除現有的目的地伺服器。

若要深入瞭解您可以使用此端點的功能，請參閱下列文章：

* [建立目的地伺服器組態](create-destination-server.md)
* [擷取目的地伺服器設定](retrieve-destination-server.md)
* [更新目的地伺服器設定](update-destination-server.md)
