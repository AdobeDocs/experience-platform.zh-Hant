---
description: 瞭解如何格式化API呼叫，以透過Adobe Experience Platform Destination SDK提交目的地發佈請求。
title: 建立目的地發佈請求
exl-id: 913be9de-a699-4756-885d-b3761ec729cb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---

# 建立目的地發佈請求

>[!IMPORTANT]
>
>如果您要提交產品化（公用）目的地以供其他Experience Platform客戶使用，則只需使用此API端點即可。 如果您要建立私人目的地以供您自用，則不需要使用發佈API正式提交目的地。

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/destinations/publish`

設定並測試目的地後，您就可以將其提交至Adobe進行檢閱和發佈。 閱讀[針對在Destination SDK](../guides/submit-destination.md)中撰寫的目的地，提交以供檢閱作為目的地提交程式一部分而必須執行的所有其他步驟。

發生下列情況時，請使用發佈目的地API端點提交發佈請求：

* 身為Destination SDK合作夥伴，您想要讓所有Experience Platform組織都能使用您的產品化目的地，供所有Experience Platform客戶使用；
* 您對設定進行了&#x200B;*任何更新*。 只有在您提交經Experience Platform團隊核准的新發佈請求後，設定更新才會反映在目的地中。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都會區分大小寫&#x200B;**&#x200B;**。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## Destination Publishing API操作快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 提交目標設定以進行發佈 {#create}

您可以透過向`/authoring/destinations/publish`端點發出POST要求，提交要發佈的目的地設定。

**API格式**

```http
POST /authoring/destinations/publish
```

+++要求

以下請求會針對由裝載中提供的引數所設定的組織，提交要發佈的目的地。 以下承載包含`/authoring/destinations/publish`端點接受的所有引數。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `destinationId` | 字串 | 您要提交以進行發佈的目的地設定的目的地ID。 使用[擷取目的地組態](../authoring-api/destination-configuration/retrieve-destination-configuration.md) API呼叫，取得目的地組態的目的地識別碼。 |
| `destinationAccess` | 字串 | 使用`ALL`讓您的目的地出現在所有Experience Platform客戶的目錄中。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態201以及目的地發佈請求的詳細資料。

+++

## API錯誤處理

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在知道如何提交目的地的發佈要求。 Adobe Experience Platform團隊將審閱您的發佈請求，並在五個工作日內回覆您。
