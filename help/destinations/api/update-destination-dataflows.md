---
keywords: Experience Platform；首頁；熱門主題；流程服務；更新目標資料流
solution: Experience Platform
title: 使用流服務API更新目標資料流
type: Tutorial
description: 本教學課程涵蓋更新目標資料流的步驟。 了解如何使用流服務API啟用或禁用資料流、更新其基本資訊，或添加和刪除段和屬性。
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '2408'
ht-degree: 1%

---

# 使用流服務API更新目標資料流

本教學課程涵蓋更新目標資料流的步驟。 了解如何啟用或禁用資料流、更新其基本資訊，或使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). 有關使用Experience PlatformUI編輯目標資料流的資訊，請閱讀 [編輯啟動流程](/help/destinations/ui/edit-activation.md).

## 快速入門 {#get-started}

本教學課程需要您具備有效的流程ID。 如果您沒有有效的流ID，請從 [目的地目錄](../catalog/overview.md) 並依照 [連接到目標](../ui/connect-destination.md) 和 [啟動資料](../ui/activation-overview.md) ，再嘗試本教學課程。

>[!NOTE]
>
> 詞語 *流量* 和 *資料流* 在本教學課程中可互換使用。 在本教學課程的內容中，其含義相同。

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

更新目標資料流的第一步是使用流ID檢索資料流詳細資訊。 您可以向發出GET請求，以檢視現有資料流的目前詳細資訊 `/flows` 端點。

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

成功的響應返回資料流的當前詳細資訊，包括其版本、唯一標識符(`id`)及其他相關資訊。

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

要更新資料流的名稱和說明，請向 [!DNL Flow Service] API，同時提供您的流程ID、版本，以及您要使用的新值。

>[!IMPORTANT]
>
>此 `If-Match` 提出PATCH請求時需要標題。 此標題的值是要更新的資料流的唯一版本。 每次成功更新資料流時，etag值都會更新。

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
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`, `replace`，和 `remove`. |
| `path` | 定義要更新的流程的部分。 |
| `value` | 您要用更新參數的新值。 |

**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以向 [!DNL Flow Service] API，同時提供您的流程ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 啟用或禁用資料流 {#enable-disable-dataflow}

啟用後，資料流會將配置檔案導出到目標。 資料流預設為啟用，但可以禁用以暫停配置檔案導出。

您可以向發出POST請求，以啟用或停用現有的目標資料流 [!DNL Flow Service] API，並提供您要更新流程的狀態。

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

以下請求將資料流的狀態更新為禁用狀態。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=disable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以向 [!DNL Flow Service] API，同時提供您的流程ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 向資料流添加段 {#add-segment}

要向目標資料流添加PATCH，請向 [!DNL Flow Service] API，同時提供您要新增的流程ID、版本和區段。

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
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`, `replace`，和 `remove`. 要將段添加到資料流，請使用 `add` 操作。 |
| `path` | 定義要更新的流程的部分。 將段添加到資料流時，請使用示例中指定的路徑。 |
| `value` | 您要用更新參數的新值。 |
| `id` | 指定要添加到目標資料流的段的ID。 |
| `name` | **(可選)**. 指定要添加到目標資料流的段的名稱。 請注意，此欄位不是必填欄位，您可以在不提供其名稱的情況下成功將段添加到目標資料流。 |
| `filenameTemplate` | 針對 *批次目的地* 只有。 只有在批次檔案匯出目的地(如Amazon S3、SFTP或Azure Blob)中將區段新增至資料流時，才需要此欄位。 <br> 此欄位確定導出到目標的檔案的檔案名格式。 <br> 可使用下列選項： <br> <ul><li>`%DESTINATION_NAME%`: 必要. 匯出的檔案包含目的地名稱。</li><li>`%SEGMENT_ID%`: 必要. 匯出的檔案包含匯出區段的ID。</li><li>`%SEGMENT_NAME%`: **(選用)**. 匯出的檔案包含匯出區段的名稱。</li><li>`DATETIME(YYYYMMdd_HHmmss)` 或 `%TIMESTAMP%`: **（可選）**. 為檔案選取這兩個選項之一，以納入Experience Platform產生檔案的時間。</li><li>`custom-text`: **(選用)**. 將此佔位符替換為要在檔案名末尾附加的任何自定義文本。</li></ul> <br> 有關配置檔案名的詳細資訊，請參閱 [配置檔案名](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) 批次目的地啟動教學課程中的一節。 |
| `exportMode` | 針對 *批次目的地* 只有。 只有在批次檔案匯出目的地(如Amazon S3、SFTP或Azure Blob)中將區段新增至資料流時，才需要此欄位。 <br> 必要. 選取「`"DAILY_FULL_EXPORT"`」或「`"FIRST_FULL_THEN_INCREMENTAL"`」。如需這兩個選項的詳細資訊，請參閱 [導出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 和 [導出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 在批次目的地啟動教學課程中。 |
| `startDate` | 選取區段應開始將設定檔匯出至目的地的日期。 |
| `frequency` | 針對 *批次目的地* 只有。 只有在批次檔案匯出目的地(如Amazon S3、SFTP或Azure Blob)中將區段新增至資料流時，才需要此欄位。 <br> 必要. <br> <ul><li>若 `"DAILY_FULL_EXPORT"` 導出模式，可以選擇 `ONCE` 或 `DAILY`.</li><li>若 `"FIRST_FULL_THEN_INCREMENTAL"` 導出模式，可以選擇 `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`.</li></ul> |
| `triggerType` | 針對 *批次目的地* 只有。 只有選取 `"DAILY_FULL_EXPORT"` 模式 `frequency` 選取器。 <br> 必要. <br> <ul><li>選擇 `"AFTER_SEGMENT_EVAL"` 讓啟動工作在每日Platform批次分段工作完成後立即執行。 這可確保在啟動工作執行時，最新的設定檔會匯出至您的目的地。</li><li>選擇 `"SCHEDULED"` 以讓啟動作業在固定時間執行。 這可確保Experience Platform設定檔資料會每天同時匯出，但您匯出的設定檔可能不是最新的，具體取決於啟動工作開始前批次分段工作是否已完成。 選取此選項時，您也必須新增 `startTime` 以UTC表示每日出口應發生的時間。</li></ul> |
| `endDate` | 針對 *批次目的地* 只有。 只有在批次檔案匯出目的地(如Amazon S3、SFTP或Azure Blob)中將區段新增至資料流時，才需要此欄位。 <br> 不適用於選擇 `"exportMode":"DAILY_FULL_EXPORT"` 和 `"frequency":"ONCE"`. <br> 設定區段成員停止匯出至目的地的日期。 |
| `startTime` | 針對 *批次目的地* 只有。 只有在批次檔案匯出目的地(如Amazon S3、SFTP或Azure Blob)中將區段新增至資料流時，才需要此欄位。 <br> 必要. 選取何時應產生包含區段成員的檔案並匯出至您的目的地。 |

**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以向 [!DNL Flow Service] API，同時提供您的流程ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 從資料流中刪除段 {#remove-segment}

要從現有目標資料流中刪除段，請執行PATCH請求 [!DNL Flow Service] API，同時提供您要移除之區段的流量ID、版本和索引選取器。 索引開始於 `0`. 例如，下方的範例請求會從資料流中移除第一和第二區段。

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
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`, `replace`，和 `remove`. 要從資料流中刪除段，請使用 `remove` 操作。 |
| `path` | 根據段選擇器的索引，指定應從目標資料流中刪除的現有段。 要檢索資料流中的段順序，請對執行GET調用 `/flows` 端點並檢查 `transformations.segmentSelectors` 屬性。 要刪除資料流中的第一個段，請使用 `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以向 [!DNL Flow Service] API，同時提供您的流程ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 更新資料流中段的元件 {#update-segment}

您可以更新現有目標資料流中段的元件。 例如，您可以變更匯出頻率，或編輯檔案名稱範本。 若要這麼做，請對 [!DNL Flow Service] API，同時提供您要更新之區段的流量ID、版本和索引選取器。 索引開始於 `0`. 例如，以下請求會更新資料流中的第九個區段。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

在現有目標資料流中更新段時，應首先執行GET操作以檢索要更新的段的詳細資訊。 接著，請提供裝載中的所有區段資訊，而不只是您要更新的欄位。 在以下範例中，自訂文字會新增到檔案名稱範本的結尾，而匯出排程頻率會從6小時更新為12小時。

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

如需裝載中屬性的說明，請參閱區段 [向資料流添加段](#add-segment).


**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以向 [!DNL Flow Service] API，同時提供您的流程ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

請參閱下列範例，以取得可在資料流中更新的區段元件的更多範例。

## 將區段的匯出模式從排程更新為評估區段後的 {#update-export-mode}

+++ 按一下「 」即可查看區段匯出的範例，其中區段匯出會從每天在指定時間啟動，更新為在Platform批次分段工作完成後每天啟動。

區段會每天16:00 UTC匯出。

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

此區段會在每日批次分段作業完成後，每天匯出。

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

## 更新檔案名模板以在檔案名中包含其他欄位 {#update-filename-template}

+++ 按一下可查看更新檔案名模板以在檔案名中包括其他欄位的示例

匯出的檔案包含目的地名稱和Experience Platform區段ID

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

匯出的檔案包含目的地名稱、Experience Platform區段ID、Experience Platform產生檔案的日期和時間，以及附加在檔案結尾的自訂文字。


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

## 向資料流添加配置檔案屬性 {#add-profile-attribute}

要向目標資料流添加配置檔案屬性，請執行PATCH請求 [!DNL Flow Service] API，同時提供您要新增的流程ID、版本和設定檔屬性。

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
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`, `replace`，和 `remove`. 要將配置檔案屬性添加到資料流，請使用 `add` 操作。 |
| `path` | 定義要更新的流程的部分。 將配置檔案屬性添加到資料流時，請使用示例中指定的路徑。 |
| `value.path` | 要添加到資料流的配置檔案屬性的值。 |

**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以向 [!DNL Flow Service] API，同時提供您的流程ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 從資料流中刪除配置檔案屬性 {#remove-profile-attribute}

要從現有目標資料流中刪除配置檔案屬性，請執行PATCH請求 [!DNL Flow Service] API，同時提供您要移除之設定檔屬性的流程ID、版本和索引選取器。 索引開始於 `0`. 例如，下面的示例請求從資料流中刪除了第五個配置檔案屬性。


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
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括： `add`, `replace`，和 `remove`. 要從資料流中刪除段，請使用 `remove` 操作。 |
| `path` | 根據段選擇器的索引，指定應從目標資料流中刪除的現有配置檔案屬性。 要檢索資料流中的配置檔案屬性順序，請對執行GET調用 `/flows` 端點並檢查 `transformations.profileSelectors` 屬性。 要刪除資料流中的第一個段，請使用 `"path":"transformations/0/params/segmentSelectors/selectors/0/"`. |


**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以向 [!DNL Flow Service] API，同時提供您的流程ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](/help/landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](/help/landing/troubleshooting.md#request-header-errors) 以取得解譯錯誤回應的詳細資訊，請參閱Platform疑難排解指南。

## 後續步驟 {#next-steps}

按照本教程，您已了解如何更新目標資料流的各種元件，如使用添加或刪除段或配置檔案屬性 [!DNL Flow Service] API。 如需目的地的詳細資訊，請參閱 [目的地概述](../home.md).
