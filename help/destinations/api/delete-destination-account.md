---
keywords: Experience Platform；首頁；熱門主題；流程服務；刪除目的地帳戶；刪除；API
solution: Experience Platform
title: 使用流量服務API刪除目標帳戶
type: Tutorial
description: 了解如何使用流量服務API刪除目標帳戶。
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# 使用流量服務API刪除目標帳戶

[!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

在啟用資料之前，您必須先設定目的地帳戶，才能連線至目的地。 本教學課程涵蓋使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>目前僅支援在流程服務API中刪除目標帳戶。 無法使用Experience PlatformUI刪除目標帳戶。

## 快速入門 {#get-started}

本教學課程要求您具備有效的連線ID。 連線ID代表與目的地的帳戶連線。 如果您沒有有效的連線ID，請從 [目的地目錄](../catalog/overview.md) 並依照 [連接到目標](../ui/connect-destination.md) ，再嘗試本教學課程。

本教學課程也需要您妥善了解下列Adobe Experience Platform元件：

* [目的地](../home.md): [!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便使用成功刪除目的地帳戶 [!DNL Flow Service] API。

### 讀取範例API呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值 {#gather-values-for-required-headers}

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括 [!DNL Flow Service]，會與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>若 `x-sandbox-name` 標題未指定，則會在 `prod` 沙箱。

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* `Content-Type: application/json`

## 找到您要刪除的目的地帳戶的連線ID {#find-connection-id}

>[!NOTE]
>本教學課程使用 [飛艇目的地](../catalog/mobile-engagement/airship-attributes.md) 例如，但所列步驟適用於任何 [可用目的地](../catalog/overview.md).

刪除目標帳戶的第一步是找出與您要刪除的目標帳戶對應的連線ID。

在Experience PlatformUI中，瀏覽至 **[!UICONTROL 目的地]** > **[!UICONTROL 帳戶]** ，並選取 **[!UICONTROL 目的地]** 欄。

![選擇要刪除的目標帳戶](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

接下來，您可以從瀏覽器的URL中擷取目的地帳戶的連線ID。

![從URL中擷取連線ID](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

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

## 刪除連接 {#delete-connection}

>[!IMPORTANT]
>
>刪除目標帳戶之前，必須刪除目標帳戶的任何現有資料流。
>要刪除現有資料流，請參閱以下頁：
>* [使用Experience PlatformUI](../ui/delete-destinations.md) 刪除現有資料流；
>* [使用流量服務API](delete-destination-dataflow.md) 刪除現有資料流。


一旦您擁有連線ID並確保目標帳戶不存在資料流，請對 [!DNL Flow Service] API。

**API格式**

```http
DELETE /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 唯一 `id` 值。 |

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

成功的回應會傳回HTTP狀態204（無內容）和空白內文。 您可以嘗試對連線進行查詢(GET)以確認刪除。 API會傳回HTTP 404（找不到）錯誤，指出已刪除目標帳戶。

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟

依照本教學課程，您已成功使用 [!DNL Flow Service] API可刪除現有的目的地帳戶。 如需使用目的地的詳細資訊，請參閱 [目的地概述](/help/destinations/home.md).