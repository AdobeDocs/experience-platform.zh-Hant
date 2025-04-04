---
solution: Experience Platform
title: 使用流程服務API編輯目的地連線
type: Tutorial
description: 瞭解如何使用流量服務API編輯目的地連線的各種元件。
exl-id: d6d27d5a-e50c-4170-bb3a-c4cbf2b46653
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 5%

---

# 使用流程服務API編輯目的地連線

本教學課程涵蓋編輯目的地連線各種元件的步驟。 瞭解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)更新驗證認證、匯出位置等。

>[!NOTE]
>
> 本教學課程中說明的編輯作業目前僅透過「流量服務API」支援。

## 快速入門 {#get-started}

本教學課程要求您具備有效的資料流ID。 如果您沒有有效的資料流ID，請從[目的地目錄](../catalog/overview.md)中選取您選擇的目的地，並依照概述的步驟[連線至目的地](../ui/connect-destination.md)和[啟用資料](../ui/activation-overview.md)，然後再嘗試進行此教學課程。

>[!NOTE]
>
> 在本教學課程中，術語&#x200B;*流程*&#x200B;和&#x200B;*資料流程*&#x200B;可互換使用。 在本教學課程的上下文中，兩者含義相同。

本教學課程也要求您實際瞭解下列Adobe Experience Platform元件：

* [目的地](../home.md)： [!DNL Destinations]是預先建立的與目的地平台的整合，可順暢地從Adobe Experience Platform啟用資料。 您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。
* [沙箱](../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功更新資料流。

### 讀取範例 API 呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱Experience Platform疑難排解指南中有關[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的章節。

### 收集所需標頭的值 {#gather-values-for-required-headers}

若要呼叫Experience Platform API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程，在所有Experience Platform API呼叫中提供每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定的虛擬沙箱隔離。 對Experience Platform API的所有請求都要求標頭，用於指定將在其中進行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果未指定`x-sandbox-name`標頭，則在`prod`沙箱下解析請求。

包含裝載(`POST`、`PUT`、`PATCH`)的所有要求都需要額外的媒體型別標頭：

* `Content-Type: application/json`

## 查詢資料流詳細資料 {#look-up-dataflow-details}

編輯目的地連線的第一個步驟，是使用流量ID擷取資料流詳細資訊。 您可以對`/flows`端點發出GET要求，以檢視現有資料流的目前詳細資料。

>[!TIP]
>
>您可以使用Experience Platform UI來取得目的地所需的資料流ID。 前往&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]**，選取所需的目的地資料流，然後在右側邊欄中尋找目的地ID。 目的地ID是您將在下一個步驟中作為流量ID使用的值。
>
> ![使用Experience Platform UI取得目的地ID](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 您要擷取之目的地資料流的唯一`id`值。 |

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

成功的回應會傳回資料流的目前詳細資料，包括其版本、唯一識別碼(`id`)及其他相關資訊。 與本教學課程最相關的內容，是下列回應中醒目提示的目標連線和基本連線ID。 您將在下一節中使用這些ID來更新目的地連線的各種元件。

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

目標連線的元件會依目的地而有所不同。 例如，對於[!DNL Amazon S3]目的地，您可以更新檔案匯出的貯體和路徑。 若為[!DNL Pinterest]目的地，您可以更新您的[!DNL Pinterest Advertiser ID]，若為[!DNL Google Customer Match]，您可以更新[!DNL Pinterest Account ID]。

若要更新目標連線的元件，請對`/targetConnections/{TARGET_CONNECTION_ID}`端點執行`PATCH`要求，同時提供您的目標連線ID、版本以及您要使用的新值。 請記住，您在上一個步驟中取得目標連線ID，當時您檢查到所要目的地的現有資料流。

>[!IMPORTANT]
>
>發出`PATCH`請求時需要`If-Match`標頭。 此標頭的值是您要更新之目標連線的唯一版本。 每次成功更新資料流、目標連線等流程實體時，etag值都會隨之更新。
>
> 若要取得etag值的最新版本，請對`/targetConnections/{TARGET_CONNECTION_ID}`端點執行GET要求，其中`{TARGET_CONNECTION_ID}`是您要更新的目標連線ID。
>
> 提出`PATCH`請求時，請務必將`If-Match`標頭的值括在雙引號中，如下例所示。

以下是一些為不同型別的目的地更新目標連線規格中引數的範例。 但更新任何目的地引數的一般規則如下：

取得連線的資料流ID >取得目標連線識別碼> `PATCH`目標連線，並更新所需引數的值。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

下列要求會更新[[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)目的地連線的`bucketName`和`path`引數。

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`、`replace`和`remove`。 |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回目標連線ID和更新的Etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的目標連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google廣告管理員與Google廣告管理員360]

**要求**

下列要求會更新[[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md)或[[!DNL Google Ad Manager 360] 目的地](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details)連線的引數，以將新的[**[!UICONTROL 附加對象ID新增至對象名稱]**](/help/release-notes/2023/april-2023.md#destinations)欄位。

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`、`replace`和`remove`。 |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回目標連線ID和更新的etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的目標連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**要求**

下列要求會更新[[!DNL Pinterest] 目的地連線](/help/destinations/catalog/advertising/pinterest.md#parameters)的`advertiserId`引數。

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`、`replace`和`remove`。 |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回目標連線ID和更新的etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的目標連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## 編輯基本連線元件（驗證引數和其他元件） {#patch-base-connection}

當您想要更新目的地的認證時，請編輯基本連線。 基礎連線的元件會因目的地而異。 例如，對於[!DNL Amazon S3]目的地，您可以將存取金鑰和秘密金鑰更新至您的[!DNL Amazon S3]位置。

若要更新基底連線的元件，請在提供您的基底連線ID、版本以及您要使用的新值時，對`/connections`端點執行`PATCH`要求。

請記住，當您在[先前的步驟](#look-up-dataflow-details)中檢查到引數`baseConnection`所需目的地的現有資料流時，已取得您的基礎連線ID。

>[!IMPORTANT]
>
>發出`PATCH`請求時需要`If-Match`標頭。 此標頭的值是您要更新的基礎連線的唯一版本。 每次成功更新資料流、基本連線等流程實體時，etag值都會隨之更新。
>
> 若要取得最新版Etag值，請對`/connections/{BASE_CONNECTION_ID}`端點執行GET要求，其中`{BASE_CONNECTION_ID}`是您要更新的基本連線ID。
>
> 提出`PATCH`請求時，請務必將`If-Match`標頭的值括在雙引號中，如下例所示。

以下是一些範例，說明如何為不同型別的目的地更新基本連線規格中的引數。 但更新任何目的地引數的一般規則如下：

取得連線的資料流識別碼>取得基底連線識別碼> `PATCH`具有所需引數更新值的基底連線。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

下列要求會更新[[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)目的地連線的`accessId`和`secretKey`引數。

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`、`replace`和`remove`。 |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回您的基本連線ID和更新的etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的基本連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**要求**

下列要求會更新[[!DNL Azure Blob] 目的地](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate)連線的引數，以更新連線至Azure Blob執行個體所需的連線字串。

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`、`replace`和`remove`。 |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回您的基本連線ID和更新的etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的基本連線ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點會遵循一般Experience Platform API錯誤訊息原則。 如需解譯錯誤回應的詳細資訊，請參閱Experience Platform疑難排解指南中的[API狀態碼](/help/landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](/help/landing/troubleshooting.md#request-header-errors)。

## 後續步驟 {#next-steps}

依照本教學課程，您已瞭解如何使用[!DNL Flow Service] API更新目的地連線的各種元件。 如需目的地的詳細資訊，請參閱[目的地概觀](../home.md)。
