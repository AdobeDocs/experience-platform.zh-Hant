---
solution: Experience Platform
title: 使用流程服務API編輯目的地連線
type: Tutorial
description: 瞭解如何使用流量服務API編輯目的地連線的各種元件。
exl-id: d6d27d5a-e50c-4170-bb3a-c4cbf2b46653
source-git-commit: 2a72f6886f7a100d0a1bf963eedaed8823a7b313
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 4%

---

# 使用流程服務API編輯目的地連線

本教學課程涵蓋編輯目的地連線各種元件的步驟。 瞭解如何使用，更新驗證認證、匯出位置等 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> 本教學課程中說明的編輯作業目前僅透過「流量服務API」支援。

## 快速入門 {#get-started}

本教學課程要求您具備有效的資料流ID。 如果您沒有有效的資料流ID，請從「 」中選擇您選擇的目的地 [目的地目錄](../catalog/overview.md) 並依照下列步驟進行 [連線到目的地](../ui/connect-destination.md) 和 [啟用資料](../ui/activation-overview.md) 在嘗試本教學課程之前。

>[!NOTE]
>
> 條款 *流量* 和 *資料流* 在本教學課程中可互換使用。 在本教學課程的上下文中，兩者含義相同。

本教學課程也要求您實際瞭解下列Adobe Experience Platform元件：

* [目的地](../home.md)： [!DNL Destinations] 是預先建立的與目的地平台的整合，可順暢地從Adobe Experience Platform啟用資料。 您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。
* [沙箱](../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供您需要瞭解的其他資訊，以使用 [!DNL Flow Service] API。

### 讀取範例 API 呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑難排解指南中。

### 收集所需標頭的值 {#gather-values-for-required-headers}

若要呼叫Platform API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程，在所有Experience Platform API呼叫中提供每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform中的所有資源，包括屬於 [!DNL Flow Service]，會隔離至特定的虛擬沙箱。 對Platform API的所有請求都需要標頭，以指定將在其中進行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果 `x-sandbox-name` 標頭未指定，請求解析於 `prod` 沙箱。

包含裝載(`POST`， `PUT`， `PATCH`)需要其他媒體型別標頭：

* `Content-Type: application/json`

## 查詢資料流詳細資料 {#look-up-dataflow-details}

編輯目的地連線的第一個步驟，是使用流量ID擷取資料流詳細資訊。 您可以透過向以下網站發出GET請求，檢視現有資料流的目前詳細資料： `/flows` 端點。

>[!TIP]
>
>您可以使用Experience PlatformUI來取得目的地所需的資料流ID。 前往 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]**，選取所需的目的地資料流，然後在右側欄中尋找目的地ID。 目的地ID是您將在下一個步驟中作為流量ID使用的值。
>
> ![使用Experience PlatformUI取得目的地ID](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 唯一的 `id` 您要擷取之目的地資料流的值。 |

**要求**

以下請求會擷取有關您的流量ID的資訊。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回資料流的目前詳細資料，包括其版本、唯一識別碼(`id`)，以及其他相關資訊。 與本教學課程最相關的內容，是下列回應中醒目提示的目標連線和基本連線ID。 您將在下一節中使用這些ID來更新目的地連線的各種元件。

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

## 編輯目標連線元件（儲存位置和其他元件） {#patch-target-connection}

目標連線的元件會依目的地而有所不同。 例如， [!DNL Amazon S3] 目的地，您可以更新檔案匯出的貯體和路徑。 的 [!DNL Pinterest] 目的地，您可以更新 [!DNL Pinterest Advertiser ID] 和 [!DNL Google Customer Match] 您可以更新 [!DNL Pinterest Account ID].

若要更新目標連線的元件，請執行 `PATCH` 要求給 `/targetConnections/{TARGET_CONNECTION_ID}` 端點，同時提供您的目標連線ID、版本以及您要使用的新值。 請記住，您在上一個步驟中取得目標連線ID，當時您檢查到所要目的地的現有資料流。

>[!IMPORTANT]
>
>此 `If-Match` 進行下列動作時需要頁首： `PATCH` 要求。 此標頭的值是您要更新之目標連線的唯一版本。 每次成功更新資料流、目標連線等流程實體時，etag值都會隨之更新。
>
> GET若要取得最新版etag值，請對 `/targetConnections/{TARGET_CONNECTION_ID}` 端點，其中 `{TARGET_CONNECTION_ID}` 是您要更新的目標連線ID。
>
> 請務必將 `If-Match` 標頭使用雙引號，如下例所示， `PATCH` 要求。

以下是一些為不同型別的目的地更新目標連線規格中引數的範例。 但更新任何目的地引數的一般規則如下：

取得連線的資料流ID >取得目標連線ID > `PATCH` 具有所需引數更新值的目標連線。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

以下請求會更新 `bucketName` 和 `path` 的引數 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目的地連線。

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回目標連線ID和更新的Etag。 您可以透過向以下發出GET請求來驗證更新： [!DNL Flow Service] API，同時提供您的目標連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager與Google Ad Manager 360]

**要求**

以下請求會更新 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) 或 [[!DNL Google Ad Manager 360] 目的地](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 連線以新增新的 [**[!UICONTROL 將對象ID附加至對象名稱]**](/help/release-notes/2023/april-2023.md#destinations) 欄位。

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回目標連線ID和更新的etag。 您可以透過向以下發出GET請求來驗證更新： [!DNL Flow Service] API，同時提供您的目標連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB pinterest]

**要求**

以下請求會更新 `advertiserId` 的引數 [[!DNL Pinterest] 目的地連線](/help/destinations/catalog/advertising/pinterest.md#parameters).

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回目標連線ID和更新的etag。 您可以透過向以下發出GET請求來驗證更新： [!DNL Flow Service] API，同時提供您的目標連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## 編輯基本連線元件（驗證引數和其他元件） {#patch-base-connection}

當您想要更新目的地的認證時，請編輯基本連線。 基礎連線的元件會因目的地而異。 例如， [!DNL Amazon S3] 目的地，您可以將存取金鑰和秘密金鑰更新至 [!DNL Amazon S3] 位置。

若要更新基礎連線的元件，請執行 `PATCH` 要求給 `/connections` 端點，並提供您的基本連線ID、版本以及您要使用的新值。

請記住，您的基本連線ID位於 [上一步](#look-up-dataflow-details)，當您檢查現有的資料流到您想要的引數目的地時 `baseConnection`.

>[!IMPORTANT]
>
>此 `If-Match` 進行下列動作時需要頁首： `PATCH` 要求。 此標頭的值是您要更新的基礎連線的唯一版本。 每次成功更新資料流、基本連線等流程實體時，etag值都會隨之更新。
>
> GET若要取得最新版Etag值，請對 `/connections/{BASE_CONNECTION_ID}` 端點，其中 `{BASE_CONNECTION_ID}` 是您要更新的基本連線ID。
>
> 請務必將 `If-Match` 標頭使用雙引號，如下例所示， `PATCH` 要求。

以下是一些範例，說明如何為不同型別的目的地更新基本連線規格中的引數。 但更新任何目的地引數的一般規則如下：

取得連線的資料流ID >取得基本連線ID > `PATCH` 具有所需引數更新值的基底連線。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

以下請求會更新 `accessId` 和 `secretKey` 的引數 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目的地連線。

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回您的基本連線ID和更新的etag。 您可以透過向以下發出GET請求來驗證更新： [!DNL Flow Service] API，同時提供您的基本連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**要求**

以下請求會更新 [[!DNL Azure Blob] 目的地](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) 連線以更新連線至Azure Blob執行個體所需的連線字串。

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 操作包括： `add`， `replace`、和 `remove`. |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回您的基本連線ID和更新的etag。 您可以透過向以下發出GET請求來驗證更新： [!DNL Flow Service] API，同時提供您的基本連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](/help/landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](/help/landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中），以取得有關解譯錯誤回應的詳細資訊。

## 後續步驟 {#next-steps}

依照本教學課程，您已瞭解如何使用更新目的地連線的各種元件。 [!DNL Flow Service] API。 如需有關目的地的詳細資訊，請參閱 [目的地概觀](../home.md).
