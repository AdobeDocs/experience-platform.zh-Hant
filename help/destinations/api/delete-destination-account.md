---
keywords: Experience Platform；首頁；熱門主題；流程服務；刪除目的地帳戶；刪除；api
solution: Experience Platform
title: 使用流程服務API刪除目的地帳戶
type: Tutorial
description: 瞭解如何使用流量服務API刪除目的地帳戶。
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 16%

---

# 使用流程服務API刪除目的地帳戶

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

在啟用資料之前，您必須先設定目的地帳戶，以連線至目的地。 本教學課程涵蓋使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)刪除不再需要的目的地帳戶的步驟。

>[!NOTE]
>
>目前僅流程服務API支援刪除目的地帳戶。 無法使用Experience Platform UI刪除目的地帳戶。

## 快速入門 {#get-started}

本教學課程要求您具備有效的連線ID。 連線ID代表與目的地的帳戶連線。 如果您沒有有效的連線ID，請從[目的地目錄](../catalog/overview.md)中選取您選擇的目的地，然後依照概述的步驟[連線至目的地](../ui/connect-destination.md)，再嘗試進行此教學課程。

本教學課程也要求您實際瞭解下列Adobe Experience Platform元件：

* [目的地](../home.md)： [!DNL Destinations]是預先建立的與目的地平台的整合，可順暢地從Adobe Experience Platform啟用資料。 您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。
* [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功刪除目的地帳戶。

### 讀取範例 API 呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值 {#gather-values-for-required-headers}

若要呼叫[!DNL Experience Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定的虛擬沙箱隔離。 對[!DNL Experience Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果未指定`x-sandbox-name`標頭，則在`prod`沙箱下解析請求。

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* `Content-Type: application/json`

## 尋找要刪除的目的地帳戶的連線ID {#find-connection-id}

>[!NOTE]
>本教學課程以[飛艇目的地](../catalog/mobile-engagement/airship-attributes.md)為例，但概述的步驟適用於任何[可用的目的地](../catalog/overview.md)。

刪除目的地帳戶的第一步，是找出與您要刪除的目的地帳戶對應的連線ID。

在Experience Platform UI中，瀏覽至&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 帳戶]**，並選取&#x200B;**[!UICONTROL 目的地]**&#x200B;欄中的數字，以選取您要刪除的帳戶。

![選取要刪除的目的地帳戶](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

接著，您可以從瀏覽器的URL擷取目的地帳戶的連線ID。

![從URL擷取連線ID](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

<!--

## Look up connection ID {#look-up-connection-id}

The first step in updating your connection information is to retrieve connection details using your connection ID.

**API format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | The unique `id` value for the connection you want to retrieve. |

**Request**

The following request retrieves information regarding your connection ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the current details of your connection including its credentials, unique identifier (`id`), and version.

```json
{
    "items": [
        {
            "id": "c8622ec7-7d94-44a5-a35a-ffcc6bdcc384",
            "createdAt": 1640103419202,
            "updatedAt": 1640104751063,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Airship Attributes",
            "description": "test account connection to Airship Attributes destination",
            "connectionSpec": {
                "id": "34cd3131-b208-474b-b779-b487b5a2bd01",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Bearer Token",
                "params": {
                    "authorizedDate": "2021-12-21",
                    "token": "xxxx"
                }
            },
            "version": "\"8c01091c-0000-0200-0000-61c2032f0000\"",
            "etag": "\"8c01091c-0000-0200-0000-61c2032f0000\""
        }
    ]
}
```

-->

## 刪除連線 {#delete-connection}

>[!IMPORTANT]
>
>在刪除目的地帳戶之前，您必須刪除任何傳送到目的地帳戶的現有資料流。
>若要刪除現有的資料流，請參閱以下頁面：
>* [使用Experience Platform UI](../ui/delete-destinations.md)刪除現有的資料流；
>* [使用流程服務API](delete-destination-dataflow.md)刪除現有的資料流。

當您有連線ID並已確保目的地帳戶沒有資料流時，請對[!DNL Flow Service] API執行DELETE請求。

**API格式**

```http
DELETE /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您要刪除之連線的唯一`id`值。 |

**要求**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。 您可以嘗試向連線提出查詢(GET)請求以確認刪除。 此API將傳回HTTP 404 （找不到）錯誤，這表示已刪除目的地帳戶。

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點會遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟

依照此教學課程，您已成功使用[!DNL Flow Service] API刪除現有的目的地帳戶。 如需使用目的地的詳細資訊，請參閱[目的地概觀](/help/destinations/home.md)。