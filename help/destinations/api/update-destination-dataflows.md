---
keywords: Experience Platform；首頁；熱門主題；流服務；更新目標資料流
solution: Experience Platform
title: 使用流服務API更新目標資料流
type: Tutorial
description: 本教程介紹了更新目標資料流的步驟。 瞭解如何使用流服務API啟用或禁用資料流、更新其基本資訊或添加和刪除段和屬性。
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '2408'
ht-degree: 1%

---

# 使用流服務API更新目標資料流

本教程介紹了更新目標資料流的步驟。 瞭解如何啟用或禁用資料流、更新其基本資訊，或使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。 有關使用Experience PlatformUI編輯目標資料流的資訊，請閱讀 [編輯激活流](/help/destinations/ui/edit-activation.md)。

## 快速入門 {#get-started}

本教程要求您具有有效的流ID。 如果沒有有效的流ID，請從 [目標目錄](../catalog/overview.md) 並按照 [連接到目標](../ui/connect-destination.md) 和 [激活資料](../ui/activation-overview.md) 在嘗試本教程之前。

>[!NOTE]
>
> 術語 *流* 和 *資料流* 在本教程中可互換使用。 在本教程的上下文中，其含義相同。

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

更新目標資料流的第一步是使用流ID檢索資料流詳細資訊。 您可以通過向以下站點發出GET請求來查看現有資料流的當前詳細資訊 `/flows` 端點。

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

成功的響應將返回資料流的當前詳細資訊，包括其版本、唯一標識符(`id`等相關資訊。

```json
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
            {
               "name":"GeneralTransform",
               "params":{
                  "profileSelectors":{
                     "selectors":[
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"Email",
                              "operator":"EXISTS",
                              "identity":{
                                 "namespace":"Email"
                              },
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"Email",
                                 "destination":"Email",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"Email",
                                 "destinationXdmPath":"Email"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.firstName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.firstName",
                                 "destination":"person.name.firstName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.firstName",
                                 "destinationXdmPath":"person.name.firstName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"person.name.lastName",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"person.name.lastName",
                                 "destination":"person.name.lastName",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"person.name.lastName",
                                 "destinationXdmPath":"person.name.lastName"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"personalEmail.address",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"personalEmail.address",
                                 "destination":"personalEmail.address",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"personalEmail.address",
                                 "destinationXdmPath":"personalEmail.address"
                              }
                           }
                        },
                        {
                           "type":"JSON_PATH",
                           "value":{
                              "path":"segmentMembership.status",
                              "operator":"EXISTS",
                              "mapping":{
                                 "sourceType":"text/x.schema-path",
                                 "source":"segmentMembership.status",
                                 "destination":"segmentMembership.status",
                                 "identity":false,
                                 "primaryIdentity":false,
                                 "functionVersion":0,
                                 "copyModeMapping":false,
                                 "sourceAttribute":"segmentMembership.status",
                                 "destinationXdmPath":"segmentMembership.status"
                              }
                           }
                        }
                     ],
                     "mandatoryFields":[
                        "Email",
                        "person.name.firstName",
                        "person.name.lastName"
                     ],
                     "primaryFields":[
                        {
                           "identityNamespace":"Email",
                           "fieldType":"IDENTITY"
                        }
                     ]
                  },
                  "segmentSelectors":{
                     "selectors":[
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                              "name":"Interested in Mountain Biking",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"ONCE",
                                 "startDate":"2021-12-25",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"f52a3785-2e7c-40a7-8137-9be99af7794e",
                              "name":"Birth year 1970",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"DAILY_FULL_EXPORT",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"6caa79b9-39e0-4c37-892b-5061cdca2377",
                              "name":"Account Leads",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"DAILY",
                                 "startDate":"2021-12-23",
                                 "endDate":"2021-12-31",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        },
                        {
                           "type":"PLATFORM_SEGMENT",
                           "value":{
                              "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
                              "name":"Batch export for autumn campaign",
                              "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                              "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                              "schedule":{
                                 "frequency":"EVERY_6_HOURS",
                                 "startDate":"2022-01-05",
                                 "endDate":"2022-12-30",
                                 "startTime":"20:00"
                              },
                              "createTime":"1640289901",
                              "updateTime":"1640289901"
                           }
                        }
                     ]
                  }
               }
            }
         ]
      }
   ]
```

## 更新資料流名稱和說明 {#update-dataflow}

要更新資料流的名稱和說明，請向 [!DNL Flow Service] 提供流ID、版本和要使用的新值時的API。

>[!IMPORTANT]
>
>的 `If-Match` 發出PATCH請求時需要標頭。 此標題的值是要更新的資料流的唯一版本。 etag值會隨著資料流的每次成功更新而更新。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

以下請求更新資料流的名稱和說明。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/name",
                "value": "2021/2022 winter campaign"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "ACME company holiday campaign for high fidelity customers and prospects"
            }
        ]'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 |
| `path` | 定義要更新的流的部分。 |
| `value` | 要用更新參數的新值。 |

**回應**

成功的響應將返回流ID和更新的etag。 您可以通過向Web站點發出GET請求來驗證更新 [!DNL Flow Service] API，同時提供流ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 啟用或禁用資料流 {#enable-disable-dataflow}

啟用後，資料流會將配置檔案導出到目標。 預設情況下會啟用資料流，但可以禁用資料流以暫停配置檔案導出。

可以通過向Web站點發出POST請求來啟用或禁用現有目標資料流 [!DNL Flow Service] API和提供要將流更新到的狀態。

**API格式**

```http
POST /flows/{FLOW_ID}/action?op=enable or disable
```

**要求**

以下請求將資料流的狀態更新為已啟用。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=enable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

以下請求將資料流的狀態更新為禁用。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=disable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回流ID和更新的etag。 您可以通過向Web站點發出GET請求來驗證更新 [!DNL Flow Service] API，同時提供流ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 將段添加到資料流 {#add-segment}

要將段添加到目標資料流，請向 [!DNL Flow Service] 提供流ID、版本和要添加的段時使用的API。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

以下請求將新段添加到現有目標資料流。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"add",
      "path":"/transformations/0/params/segmentSelectors/selectors/-",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"2d79d0d8-724f-49fc-a09d-d1dec338c93c",
            "name":"Winter 2021/2022 campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%SEGMENT_NAME%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"DAILY_FULL_EXPORT",
            "schedule":{
               "startDate":"2022-01-05",
               "frequency":"DAILY",
               "triggerType": "AFTER_SEGMENT_EVAL",
               "endDate":"2022-03-10"
            }
         }
      }
   }
]'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 要將段添加到資料流，請使用 `add` 的下界。 |
| `path` | 定義要更新的流的部分。 將段添加到資料流時，請使用示例中指定的路徑。 |
| `value` | 要用更新參數的新值。 |
| `id` | 指定要添加到目標資料流的段的ID。 |
| `name` | **(可選)**. 指定要添加到目標資料流的段的名稱。 請注意，此欄位不是必需欄位，您可以在不提供段名稱的情況下成功將段添加到目標資料流。 |
| `filenameTemplate` | 對於 *批處理目標* 只是。 僅當將段添加到批處理檔案導出目標(如AmazonS3、SFTP或Azure Blob)中的資料流時，才需要此欄位。 <br> 此欄位確定導出到目標的檔案的檔案名格式。 <br> 提供下列選項：: <br> <ul><li>`%DESTINATION_NAME%`: 必要. 導出的檔案包含目標名稱。</li><li>`%SEGMENT_ID%`: 必要. 導出的檔案包含導出段的ID。</li><li>`%SEGMENT_NAME%`: **(選用)**. 導出的檔案包含導出段的名稱。</li><li>`DATETIME(YYYYMMdd_HHmmss)` 或 `%TIMESTAMP%`: **（可選）**。 為檔案選擇以下兩個選項之一，以包括通過Experience Platform生成檔案的時間。</li><li>`custom-text`: **(選用)**. 將此佔位符替換為要在檔案名末尾附加的任何自定義文本。</li></ul> <br> 有關配置檔案名的詳細資訊，請參閱 [配置檔案名](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) 的子目錄。 |
| `exportMode` | 對於 *批處理目標* 只是。 僅當將段添加到批處理檔案導出目標(如AmazonS3、SFTP或Azure Blob)中的資料流時，才需要此欄位。 <br> 必要. 選取「`"DAILY_FULL_EXPORT"`」或「`"FIRST_FULL_THEN_INCREMENTAL"`」。有關兩個選項的詳細資訊，請參閱 [導出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 和 [導出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 在批處理目標激活教程中。 |
| `startDate` | 選擇段應開始將配置檔案導出到目標的日期。 |
| `frequency` | 對於 *批處理目標* 只是。 僅當將段添加到批處理檔案導出目標(如AmazonS3、SFTP或Azure Blob)中的資料流時，才需要此欄位。 <br> 必要. <br> <ul><li>對於 `"DAILY_FULL_EXPORT"` 導出模式，可以選擇 `ONCE` 或 `DAILY`。</li><li>對於 `"FIRST_FULL_THEN_INCREMENTAL"` 導出模式，可以選擇 `"DAILY"`。 `"EVERY_3_HOURS"`。 `"EVERY_6_HOURS"`。 `"EVERY_8_HOURS"`。 `"EVERY_12_HOURS"`。</li></ul> |
| `triggerType` | 對於 *批處理目標* 只是。 僅當選擇 `"DAILY_FULL_EXPORT"` 的 `frequency` 選擇器。 <br> 必要. <br> <ul><li>選擇 `"AFTER_SEGMENT_EVAL"` 使激活作業在每日平台批處理分段作業完成後立即運行。 這可確保在激活作業運行時，最新的配置檔案會導出到目標。</li><li>選擇 `"SCHEDULED"` 使激活作業在固定時間運行。 這可確保每天同時導出Experience Platform配置檔案資料，但導出的配置檔案可能不是最新的，具體取決於激活作業開始前批分段作業是否已完成。 選擇此選項時，還必須添加 `startTime` 以UTC表示日導出應在何時進行。</li></ul> |
| `endDate` | 對於 *批處理目標* 只是。 僅當將段添加到批處理檔案導出目標(如AmazonS3、SFTP或Azure Blob)中的資料流時，才需要此欄位。 <br> 選擇時不適用 `"exportMode":"DAILY_FULL_EXPORT"` 和 `"frequency":"ONCE"`。 <br> 設定段成員停止導出到目標的日期。 |
| `startTime` | 對於 *批處理目標* 只是。 僅當將段添加到批處理檔案導出目標(如AmazonS3、SFTP或Azure Blob)中的資料流時，才需要此欄位。 <br> 必要. 選擇生成包含段成員的檔案並將其導出到目標的時間。 |

**回應**

成功的響應將返回流ID和更新的etag。 您可以通過向Web站點發出GET請求來驗證更新 [!DNL Flow Service] API，同時提供流ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 從資料流中刪除段 {#remove-segment}

要從現有目標資料流中刪除段，請向 [!DNL Flow Service] 提供要刪除的段的流ID、版本和索引選擇器時的API。 索引起始於 `0`。 例如，下面的示例請求從資料流中刪除第一和第二段。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

以下請求從現有目標資料流中刪除兩個段。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/0/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"transformations/0/params/segmentSelectors/selectors/1/",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
}
]'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 要從資料流中刪除段，請使用 `remove` 的下界。 |
| `path` | 根據段選擇器的索引指定應從目標資料流中刪除哪些現有段。 要檢索資料流中段的順序，請對 `/flows` 端點並檢查 `transformations.segmentSelectors` 屬性。 要刪除資料流中的第一個段，請使用 `"path":"transformations/0/params/segmentSelectors/selectors/0/"`。 |


**回應**

成功的響應將返回流ID和更新的etag。 您可以通過向Web站點發出GET請求來驗證更新 [!DNL Flow Service] API，同時提供流ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 更新資料流中段的元件 {#update-segment}

您可以更新現有目標資料流中段的元件。 例如，可以更改導出頻率或編輯檔案名模板。 為此，請執行PATCH請求 [!DNL Flow Service] 提供要更新的段的流ID、版本和索引選擇器時的API。 索引起始於 `0`。 例如，以下請求更新資料流中的第九個段。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

在更新現有目標資料流中的段時，應首先執行GET操作以檢索要更新的段的詳細資訊。 然後，提供負載中的所有段資訊，而不只是要更新的欄位。 在下面的示例中，在檔案名模板的末尾添加自定義文本，並將導出計畫頻率從6小時更新為12小時。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
   {
      "op":"replace",
      "path":"/transformations/0/params/segmentSelectors/selectors/8",
      "value":{
         "type":"PLATFORM_SEGMENT",
         "value":{
            "id":"4c41c318-9e8c-4a4f-b880-877cdd629fc7",
            "name":"Batch export for autumn campaign",
            "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_custom-text",
            "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
            "schedule":{
               "frequency":"EVERY_12_HOURS",
               "startDate":"2022-01-05",
               "endDate":"2022-01-30",
               "startTime":"20:00"
            },
            "createTime":"1640289901",
            "updateTime":"1640289901"
         }
      }
   }
]'
```

有關負載中屬性的說明，請參閱一節 [將段添加到資料流](#add-segment)。


**回應**

成功的響應將返回流ID和更新的etag。 您可以通過向Web站點發出GET請求來驗證更新 [!DNL Flow Service] API，同時提供流ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

有關可以在資料流中更新的段元件的更多示例，請參見以下示例。

## 將段的導出模式從計畫更新為段評估之後 {#update-export-mode}

+++ 按一下查看一個示例，其中段導出從在指定時間每天激活到在平台批處理分段作業完成後每天激活。

該段每天在UTC 16:00導出。

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

每日批處理分段作業完成後，每天導出該段。

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "AFTER_SEGMENT_EVAL",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## 更新檔案名模板以在檔案名中包括其他欄位 {#update-filename-template}

+++ 按一下查看更新檔案名模板以在檔案名中包括附加欄位的示例

導出的檔案包含目標名稱和Experience Platform段ID

```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

導出的檔案包含目標名稱、Experience Platform段ID、Experience Platform生成檔案的日期和時間以及檔案末尾附加的自定義文本。


```json
{
  "type": "PLATFORM_SEGMENT",
  "value": {
    "id": "b1e50e8e-a6e2-420d-99e8-a80deda2082f",
    "name": "12JAN22-AEP-NA-NTC-90D-MW",
    "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%_%this is custom text%",
    "exportMode": "DAILY_FULL_EXPORT"
    "schedule": {
      "frequency": "DAILY",
      "triggerType": "SCHEDULED",
      "startDate": "2022-01-13",
      "endDate": "2023-01-13",
      "startTime":"16:00"
    },
    "createTime": "1642041770",
    "updateTime": "1642615573"
  }
}
```

+++

## 將配置檔案屬性添加到資料流 {#add-profile-attribute}

要將配置檔案屬性添加到目標資料流，請向 [!DNL Flow Service] 提供流ID、版本和要添加的配置檔案屬性時的API。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

以下請求將新配置檔案屬性添加到現有目標資料流。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"add",
    "path":"/transformations/0/params/profileSelectors/selectors/-",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 要將配置檔案屬性添加到資料流，請使用 `add` 的下界。 |
| `path` | 定義要更新的流的部分。 將配置檔案屬性添加到資料流時，請使用示例中指定的路徑。 |
| `value.path` | 要添加到資料流的配置檔案屬性的值。 |

**回應**

成功的響應將返回流ID和更新的etag。 您可以通過向Web站點發出GET請求來驗證更新 [!DNL Flow Service] API，同時提供流ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 從資料流中刪除配置檔案屬性 {#remove-profile-attribute}

要從現有目標資料流中刪除配置檔案屬性，請向 [!DNL Flow Service] 提供要刪除的配置檔案屬性的流ID、版本和索引選擇器時的API。 索引起始於 `0`。 例如，下面的示例請求將從資料流中刪除第五個配置檔案屬性。


**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

以下請求從現有目標資料流中刪除配置檔案屬性。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
    {
    "op":"remove",
    "path":"/transformations/0/params/profileSelectors/selectors/4",
    "value":{
        "type":"JSON_PATH",
        "value":{
            "path":"mobilePhone.status"
        }
    }
    }
]'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`。 `replace`, `remove`。 要從資料流中刪除段，請使用 `remove` 的下界。 |
| `path` | 根據段選擇器的索引指定應從目標資料流中刪除哪些現有配置檔案屬性。 要檢索資料流中配置檔案屬性的順序，請對 `/flows` 端點並檢查 `transformations.profileSelectors` 屬性。 要刪除資料流中的第一個段，請使用 `"path":"transformations/0/params/segmentSelectors/selectors/0/"`。 |


**回應**

成功的響應將返回流ID和更新的etag。 您可以通過向Web站點發出GET請求來驗證更新 [!DNL Flow Service] API，同時提供流ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## API錯誤處理 {#api-error-handling}

本教程中的API端點遵循一般Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](/help/landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](/help/landing/troubleshooting.md#request-header-errors) 有關解釋錯誤響應的詳細資訊，請參閱「Platform troubleshooting guide（平台故障排除指南）」。

## 後續步驟 {#next-steps}

通過本教程，您已學習了如何更新目標資料流的各個元件，如使用添加或刪除段或配置檔案屬性 [!DNL Flow Service] API。 有關目標的詳細資訊，請參閱 [目標概述](../home.md)。
