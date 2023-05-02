---
solution: Experience Platform
title: 使用流量服務API編輯目的地連線
type: Tutorial
description: 了解如何使用流量服務API編輯目的地連線的各種元件。
source-git-commit: 956ac5d210d54526e886e57b8ea37ab4b3fbab8a
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 2%

---

# 使用流量服務API編輯目的地連線

本教學課程涵蓋編輯目的地連線各種元件的步驟。 了解如何使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> 本教學課程中所述的編輯作業目前僅透過流量服務API受支援。

## 快速入門 {#get-started}

本教程要求您具有有效的資料流ID。 如果您沒有有效的資料流ID，請從 [目的地目錄](../catalog/overview.md) 並依照 [連接到目標](../ui/connect-destination.md) 和 [啟動資料](../ui/activation-overview.md) ，再嘗試本教學課程。

>[!NOTE]
>
> 詞語 *流量* 和 *資料流* 在本教學課程中可互換使用。 在本教學課程的內容中，這些函式有相同的意義。

本教學課程也需要您妥善了解下列Adobe Experience Platform元件：

* [目的地](../home.md): [!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。
* [沙箱](../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供了您需要了解的其他資訊，以便使用成功更新資料流 [!DNL Flow Service] API。

### 讀取範例API呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難排解指南中。

### 收集必要標題的值 {#gather-values-for-required-headers}

若要呼叫Platform API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，所有Experience PlatformAPI呼叫中每個必要標題的值都會顯示，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform中的所有資源，包括 [!DNL Flow Service]，會與特定虛擬沙箱隔離。 對Platform API提出的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>若 `x-sandbox-name` 標題未指定，則會在 `prod` 沙箱。

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* `Content-Type: application/json`

## 查找資料流詳細資訊 {#look-up-dataflow-details}

編輯目標連接的第一步是使用流ID檢索資料流詳細資訊。 您可以向發出GET請求，以檢視現有資料流的目前詳細資訊 `/flows` 端點。

>[!TIP]
>
>您可以使用Experience PlatformUI來獲取目標所需的資料流ID。 前往 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]**，請選取所需的目的地資料流，然後在右側邊欄中尋找目的地ID。 目的地ID是您將在下一個步驟中用作流程ID的值。
>
> ![使用Experience PlatformUI取得目的地ID](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 唯一 `id` 要檢索的目標資料流的值。 |

**要求**

下列要求會擷取關於您的流程ID的資訊。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回資料流的當前詳細資訊，包括其版本、唯一標識符(`id`)及其他相關資訊。 與本教學課程最相關的是以下回應中強調顯示的目標連線和基本連線ID。 您會在後續章節使用這些ID來更新目的地連線的各種元件。

```json {line-numbers="true" start-line="1" highlight="27,38"}
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            "shortened for brevity"
         ]
      }
   ]
```

>[!ENDSHADEBOX]

## 編輯目標連接元件（儲存位置和其他元件） {#patch-target-connection}

目標連接的元件因目的地而異。 例如， [!DNL Amazon S3] 目的地，您可以更新檔案匯出的貯體和路徑。 針對 [!DNL Pinterest] 目的地，您可以更新 [!DNL Pinterest Advertiser ID] 和 [!DNL Google Customer Match] 您可以更新 [!DNL Pinterest Account ID].

若要更新目標連線的元件，請向 `/targetConnections/{TARGET_CONNECTION_ID}` 端點，同時提供您要使用的目標連線ID、版本和新值。 請記住，在上一步中，當您檢查到所需目標的現有資料流時，您的目標連接ID已得到。

>[!IMPORTANT]
>
>此 `If-Match` 提出PATCH請求時需要標題。 此標題的值是您要更新的目標連線的唯一版本。 etag值會隨著流實體（如資料流、目標連接等）的每次成功更新而更新。
>
> 若要取得etag值的最新版本，請向 `/targetConnections/{TARGET_CONNECTION_ID}` 端點，其中 `{TARGET_CONNECTION_ID}` 是您要更新的目標連線ID。

以下是更新不同目的地類型目標連線規格參數的幾個範例。 但更新任何目的地參數的一般規則如下：

獲取連接的資料流ID >獲取目標連接ID >PATCH目標連接，並獲取所需參數的更新值。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

下列請求會更新 `bucketName` 和 `path` 參數 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目標連線。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "bucketName": "newBucketName",
      "path": "updatedPath"
    }
  }
]'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`, `replace`，和 `remove`. |
| `path` | 定義要更新的流程的部分。 |
| `value` | 您要用更新參數的新值。 |

**回應**

成功的回應會傳回您的Target連線ID和更新的Etag。 您可以向 [!DNL Flow Service] API，同時提供您的Target連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google廣告管理員和Google廣告管理員360]

**要求**

下列請求會更新 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) 或 [[!DNL Google Ad Manager 360] 目的地](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 連線以新增 [**[!UICONTROL 將區段ID附加至區段名稱]**](/help/release-notes/2023/april-2023.md#destinations) 欄位。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/params/appendSegmentId",
    "value": true
  }
]'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`, `replace`，和 `remove`. |
| `path` | 定義要更新的流程的部分。 |
| `value` | 您要用更新參數的新值。 |

**回應**

成功的回應會傳回您的Target連線ID和更新的etag。 您可以向 [!DNL Flow Service] API，同時提供您的Target連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**要求**

下列請求會更新 `advertiserId` 參數 [[!DNL Pinterest] 目的地連線](/help/destinations/catalog/advertising/pinterest.md#parameters).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "advertiser_id": "1234567890"
    }
  }
]'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`, `replace`，和 `remove`. |
| `path` | 定義要更新的流程的部分。 |
| `value` | 您要用更新參數的新值。 |

**回應**

成功的回應會傳回您的Target連線ID和更新的etag。 您可以向 [!DNL Flow Service] API，同時提供您的Target連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## 編輯基本連接元件（驗證參數和其他元件） {#patch-base-connection}

基本連接的元件因目的而異。 例如， [!DNL Amazon S3] 目的地，您可以將存取金鑰和機密金鑰更新至您的 [!DNL Amazon S3] 位置。

要更新基本連接的元件，請執行PATCH請求 `/connections` 端點，同時提供您要使用的基本連線ID、版本和新值。

請記住，在上一步中，當您檢查到所需目標的現有資料流時，您的基本連接ID已獲得。

>[!IMPORTANT]
>
>此 `If-Match` 提出PATCH請求時需要標題。 此標題的值是要更新的基本連接的唯一版本。 etag值會隨著流實體（如資料流、基本連接等）的每次成功更新而更新。
>
> 若要取得最新版的Etag值，請向 `/connections/{BASE_CONNECTION_ID}` 端點，其中 `{BASE_CONNECTION_ID}` 是您要更新的基本連線ID。

以下是更新不同目的地類型基本連線規格參數的幾個範例。 但更新任何目的地參數的一般規則如下：

獲取連接的資料流ID >獲取基本連接ID >用所需參數的更新值PATCH基本連接。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

下列請求會更新 `accessId` 和 `secretKey` 參數 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目標連線。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "accessId": "exampleAccessId",
      "secretKey": "exampleSecretKey"
    }
  }
]'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`, `replace`，和 `remove`. |
| `path` | 定義要更新的流程的部分。 |
| `value` | 您要用更新參數的新值。 |

**回應**

成功的回應會傳回基本連線ID和更新的etag。 您可以向 [!DNL Flow Service] API，同時提供基本連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**要求**

下列請求會更新 [[!DNL Azure Blob] 目的地](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) 連接以更新連接到Azure Blob實例所需的連接字串。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "connectionString": "updatedString"
    }
  }
]'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`, `replace`，和 `remove`. |
| `path` | 定義要更新的流程的部分。 |
| `value` | 您要用更新參數的新值。 |

**回應**

成功的回應會傳回基本連線ID和更新的etag。 您可以向 [!DNL Flow Service] API，同時提供基本連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](/help/landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](/help/landing/troubleshooting.md#request-header-errors) 以取得解譯錯誤回應的詳細資訊，請參閱Platform疑難排解指南。

## 後續步驟 {#next-steps}

依照本教學課程，您已了解如何使用 [!DNL Flow Service] API。 如需目的地的詳細資訊，請參閱 [目的地概述](../home.md).
