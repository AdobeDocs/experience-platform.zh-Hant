---
solution: Experience Platform
title: 使用流服務API編輯目標連接
type: Tutorial
description: 瞭解如何使用流服務API編輯目標連接的各個元件。
source-git-commit: 956ac5d210d54526e886e57b8ea37ab4b3fbab8a
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 2%

---

# 使用流服務API編輯目標連接

本教程介紹了編輯目標連接的各種元件的步驟。 瞭解如何使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

>[!NOTE]
>
> 本教程中描述的編輯操作目前僅通過流服務API受支援。

## 快速入門 {#get-started}

本教程要求您具有有效的資料流ID。 如果沒有有效的資料流ID，請從 [目標目錄](../catalog/overview.md) 並按照 [連接到目標](../ui/connect-destination.md) 和 [激活資料](../ui/activation-overview.md) 在嘗試本教程之前。

>[!NOTE]
>
> 術語 *流* 和 *資料流* 在本教程中可互換使用。 在本教程的上下文中，它們具有相同的含義。

本教程還要求您對以下Adobe Experience Platform元件有一定的瞭解：

* [目標](../home.md): [!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。
* [沙箱](../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

### 讀取示例API調用 {#reading-sample-api-calls}

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難解答指南。

### 收集所需標題的值 {#gather-values-for-required-headers}

要調用平台API，必須先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成Experience Platform教程將提供所有驗證API調用中每個必需標頭的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Experience Platform內所有資源，包括屬於 [!DNL Flow Service]，與特定虛擬沙箱隔離。 所有對平台API的請求都需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如果 `x-sandbox-name` 未指定標頭，請求在 `prod` 沙盒。

所有包含負載(POST、PUT、PATCH)的請求都需要附加的媒體類型報頭：

* `Content-Type: application/json`

## 查找資料流詳細資訊 {#look-up-dataflow-details}

編輯目標連接的第一步是使用流ID檢索資料流詳細資訊。 您可以通過向以下站點發出GET請求來查看現有資料流的當前詳細資訊 `/flows` 端點。

>[!TIP]
>
>可以使用Experience PlatformUI獲取目標所需的資料流ID。 轉到 **[!UICONTROL 目標]** > **[!UICONTROL 瀏覽]**，選擇所需的目標資料流，然後在右欄中查找目標ID。 目標ID是您將在下一步中用作流ID的值。
>
> ![使用Experience PlatformUI獲取目標ID](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**API格式**

```http
GET /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 獨特 `id` 要檢索的目標資料流的值。 |

**要求**

以下請求檢索有關流ID的資訊。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回資料流的當前詳細資訊，包括其版本、唯一標識符(`id`等相關資訊。 本教程最相關的是以下響應中突出顯示的目標連接和基本連接ID。 您將在下一節中使用這些ID來更新目標連接的各個元件。

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

目標連接的元件因目標而異。 例如， [!DNL Amazon S3] 目標，您可以更新導出檔案的儲存桶和路徑。 對於 [!DNL Pinterest] 目標，您可以更新 [!DNL Pinterest Advertiser ID] 和 [!DNL Google Customer Match] 您可以 [!DNL Pinterest Account ID]。

要更新目標連接的元件，請執行PATCH請求 `/targetConnections/{TARGET_CONNECTION_ID}` 提供目標連接ID、版本和要使用的新值時使用端點。 請記住，在檢查到所需目標的現有資料流時，在上一步中獲得了目標連接ID。

>[!IMPORTANT]
>
>的 `If-Match` 發出PATCH請求時需要標頭。 此標頭的值是要更新的目標連接的唯一版本。 etag值會隨著流實體（如資料流、目標連接等）的每次成功更新而更新。
>
> 要獲取etag值的最新版本，請向 `/targetConnections/{TARGET_CONNECTION_ID}` 端點，其中 `{TARGET_CONNECTION_ID}` 是您要更新的目標連接ID。

下面是更新目標連接規範中不同類型目標的參數的幾個示例。 但更新任何目標參數的一般規則如下：

獲取連接的資料流ID >獲取目標連接ID >用所需參數的更新值PATCH目標連接。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

以下請求更新 `bucketName` 和 `path` 參數 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目標連接。

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
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 |
| `path` | 定義要更新的流的部分。 |
| `value` | 要用更新參數的新值。 |

**回應**

成功的響應將返回目標連接ID和更新的Etag。 您可以通過向Web站點發出GET請求來驗證更新 [!DNL Flow Service] API，同時提供目標連接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google廣告經理和Google廣告經理360]

**要求**

以下請求更新 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) 或 [[!DNL Google Ad Manager 360] 目標](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 連接以添加新 [**[!UICONTROL 將段ID追加到段名稱]**](/help/release-notes/2023/april-2023.md#destinations) 的子菜單。

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
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 |
| `path` | 定義要更新的流的部分。 |
| `value` | 要用更新參數的新值。 |

**回應**

成功的響應將返回目標連接ID和更新的etag。 您可以通過向Web站點發出GET請求來驗證更新 [!DNL Flow Service] API，同時提供目標連接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**要求**

以下請求更新 `advertiserId` 參數 [[!DNL Pinterest] 目標連接](/help/destinations/catalog/advertising/pinterest.md#parameters)。

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
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 |
| `path` | 定義要更新的流的部分。 |
| `value` | 要用更新參數的新值。 |

**回應**

成功的響應將返回目標連接ID和更新的etag。 您可以通過向Web站點發出GET請求來驗證更新 [!DNL Flow Service] API，同時提供目標連接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## 編輯基本連接元件（驗證參數和其他元件） {#patch-base-connection}

基本連接的元件因目標而異。 例如， [!DNL Amazon S3] 目標，您可以將訪問密鑰和密鑰更新到 [!DNL Amazon S3] 位置。

要更新基本連接的元件，請向 `/connections` 終結點，同時提供您要使用的基本連接ID、版本和新值。

請記住，在前一步中，您檢查了到所需目標的現有資料流時，獲得了基本連接ID。

>[!IMPORTANT]
>
>的 `If-Match` 發出PATCH請求時需要標頭。 此標頭的值是要更新的基本連接的唯一版本。 etag值會隨著流實體（如資料流、基連接等）的每次成功更新而更新。
>
> 要獲取Etag值的最新版本，請向 `/connections/{BASE_CONNECTION_ID}` 端點，其中 `{BASE_CONNECTION_ID}` 是您要更新的基本連接ID。

下面是更新不同目標類型基本連接規範中參數的幾個示例。 但更新任何目標參數的一般規則如下：

獲取連接的資料流ID >獲取基本連接ID >用所需參數的更新值PATCH基本連接。

>[!BEGINSHADEBOX]

**API格式**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

以下請求更新 `accessId` 和 `secretKey` 參數 [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 目標連接。

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
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 |
| `path` | 定義要更新的流的部分。 |
| `value` | 要用更新參數的新值。 |

**回應**

成功的響應將返回基本連接ID和更新的etag。 您可以通過向Web站點發出GET請求來驗證更新 [!DNL Flow Service] API，同時提供基本連接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**要求**

以下請求更新 [[!DNL Azure Blob] 目標](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) 連接以更新連接到Azure Blob實例所需的連接字串。

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
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 |
| `path` | 定義要更新的流的部分。 |
| `value` | 要用更新參數的新值。 |

**回應**

成功的響應將返回基本連接ID和更新的etag。 您可以通過向Web站點發出GET請求來驗證更新 [!DNL Flow Service] API，同時提供基本連接ID。

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## API錯誤處理 {#api-error-handling}

本教程中的API端點遵循一般Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](/help/landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](/help/landing/troubleshooting.md#request-header-errors) 有關解釋錯誤響應的詳細資訊，請參閱「Platform troubleshooting guide（平台故障排除指南）」。

## 後續步驟 {#next-steps}

通過本教程，您已學習了如何使用 [!DNL Flow Service] API。 有關目標的詳細資訊，請參閱 [目標概述](../home.md)。
