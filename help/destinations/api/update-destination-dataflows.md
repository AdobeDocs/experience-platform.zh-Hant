---
keywords: Experience Platform；首頁；熱門主題；流程服務；更新目的地資料流程
solution: Experience Platform
title: 使用流程服務API更新目的地資料流程
type: Tutorial
description: 本教學課程涵蓋更新目的地資料流的步驟。 瞭解如何使用流量服務API來啟用或停用資料流、更新其基本資訊，或新增和移除對象和屬性。
exl-id: 3f69ad12-940a-4aa1-a1ae-5ceea997a9ba
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2410'
ht-degree: 3%

---

# 使用流程服務API更新目的地資料流程

本教學課程涵蓋更新目的地資料流的步驟。 瞭解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)來啟用或停用資料流、更新其基本資訊，或新增及移除對象和屬性。 如需使用Experience Platform UI編輯目的地資料流程的資訊，請閱讀[編輯啟動流程](/help/destinations/ui/edit-activation.md)。

## 快速入門 {#get-started}

本教學課程要求您具備有效的流量ID。 如果您沒有有效的流量ID，請從[目的地目錄](../catalog/overview.md)中選取您選擇的目的地，並依照概述的步驟[連線至目的地](../ui/connect-destination.md)和[啟用資料](../ui/activation-overview.md)，然後再嘗試進行此教學課程。

>[!NOTE]
>
> 在本教學課程中，術語&#x200B;*流程*&#x200B;和&#x200B;*資料流程*&#x200B;可互換使用。 在本教學課程的上下文中，具有相同涵義。

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

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* `Content-Type: application/json`

## 查詢資料流詳細資料 {#look-up-dataflow-details}

更新目的地資料流的第一步，是使用您的流程ID擷取資料流詳細資料。 您可以對`/flows`端點發出GET要求，以檢視現有資料流的目前詳細資料。

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

成功的回應會傳回資料流的目前詳細資料，包括其版本、唯一識別碼(`id`)及其他相關資訊。

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

若要更新您的資料流名稱和說明，請對[!DNL Flow Service] API執行PATCH要求，同時提供您的資料流ID、版本以及您要使用的新值。

>[!IMPORTANT]
>
>發出PATCH請求時需要`If-Match`標頭。 此標頭的值是您要更新之資料流的唯一版本。 每次成功更新資料流時，etag值都會更新。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

以下請求會更新您的資料流名稱和說明。

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`、`replace`和`remove`。 |
| `path` | 定義要更新的流程部分。 |
| `value` | 您想要用來更新引數的新值。 |

**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 啟用或停用資料流 {#enable-disable-dataflow}

啟用時，資料流會將設定檔匯出至目的地。 資料流預設為啟用，但可以停用以暫停設定檔匯出。

您可以對[!DNL Flow Service] API發出POST要求，並提供您要更新資料流的目標狀態，藉此啟用或停用現有的目的地資料流。

**API格式**

```http
POST /flows/{FLOW_ID}/action?op=enable or disable
```

**要求**

以下請求會將您的資料流狀態更新為已啟用。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=enable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

以下請求會將您的資料流狀態更新為停用。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc/action?op=disable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 將對象新增至資料流 {#add-segment}

若要將對象新增至目的地資料流，請提供您的資料流ID、版本以及要新增的對象，同時對[!DNL Flow Service] API執行PATCH要求。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

以下請求會將新對象新增至現有的目的地資料流。

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`、`replace`和`remove`。 若要將對象新增至資料流，請使用`add`作業。 |
| `path` | 定義要更新的流程部分。 將對象新增至資料流時，請使用範例中指定的路徑。 |
| `value` | 您想要用來更新引數的新值。 |
| `id` | 指定您要新增至目的地資料流的對象ID。 |
| `name` | **（選擇性）**。 指定您要新增至目的地資料流的對象名稱。 請注意，此欄位並非必填欄位，您可以在不提供名稱的情況下成功將對象新增至目的地資料流。 |
| `filenameTemplate` | 僅適用於&#x200B;*批次目的地*。 只有在批次檔案匯出目的地(例如Amazon S3、SFTP或Azure Blob)中將對象新增至資料流時，才需要此欄位。 <br>此欄位決定匯出至目的地之檔案的檔案名稱格式。 <br>下列選項可供使用： <br> <ul><li>`%DESTINATION_NAME%`：必要。 匯出的檔案包含目的地名稱。</li><li>`%SEGMENT_ID%`：必要。 匯出的檔案包含匯出對象的ID。</li><li>`%SEGMENT_NAME%`： **（選擇性）**。 匯出的檔案包含匯出對象的名稱。</li><li>`DATETIME(YYYYMMdd_HHmmss)`或`%TIMESTAMP%`： **（選擇性）**。 選取這兩個檔案選項之一，加入Experience Platform產生檔案的時間。</li><li>`custom-text`： **（選擇性）**。 將此預留位置取代為您要在檔案名稱結尾附加的任何自訂文字。</li></ul> <br>如需設定檔案名稱的詳細資訊，請參閱批次目的地啟動教學課程中的[設定檔案名稱](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)一節。 |
| `exportMode` | 僅適用於&#x200B;*批次目的地*。 只有在批次檔案匯出目的地(例如Amazon S3、SFTP或Azure Blob)中將對象新增至資料流時，才需要此欄位。 <br>必要。 選取`"DAILY_FULL_EXPORT"`或`"FIRST_FULL_THEN_INCREMENTAL"`。 如需有關這兩個選項的詳細資訊，請參閱批次目的地啟動教學課程中的[匯出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)和[匯出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)。 |
| `startDate` | 選取對象應開始將設定檔匯出至您的目的地的日期。 |
| `frequency` | 僅適用於&#x200B;*批次目的地*。 只有在批次檔案匯出目的地(例如Amazon S3、SFTP或Azure Blob)中將對象新增至資料流時，才需要此欄位。 <br>必要。<br> <ul><li>對於`"DAILY_FULL_EXPORT"`匯出模式，您可以選取`ONCE`或`DAILY`。</li><li>對於`"FIRST_FULL_THEN_INCREMENTAL"`匯出模式，您可以選取`"DAILY"`、`"EVERY_3_HOURS"`、`"EVERY_6_HOURS"`、`"EVERY_8_HOURS"`、`"EVERY_12_HOURS"`。</li></ul> |
| `triggerType` | 僅適用於&#x200B;*批次目的地*。 只有在`frequency`選取器中選取`"DAILY_FULL_EXPORT"`模式時才需要此欄位。 <br>必要。<br> <ul><li>選取`"AFTER_SEGMENT_EVAL"`讓啟動工作在每日Experience Platform批次細分工作完成後立即執行。 這可確保在啟動工作執行時，最新的設定檔會匯出至您的目的地。</li><li>選取`"SCHEDULED"`讓啟動工作以固定時間執行。 這可確保Experience Platform設定檔資料每天在同一時間匯出，但您匯出的設定檔可能不是最新狀態，端視批次細分工作是否在啟動工作開始之前完成。 選取此選項時，您也必須新增`startTime`以指示UTC中應該進行每日匯出的時間。</li></ul> |
| `endDate` | 僅適用於&#x200B;*批次目的地*。 只有在批次檔案匯出目的地(例如Amazon S3、SFTP或Azure Blob)中將對象新增至資料流時，才需要此欄位。 <br>在選取`"exportMode":"DAILY_FULL_EXPORT"`和`"frequency":"ONCE"`時不適用。 <br>設定對象成員停止匯出至目的地的日期。 |
| `startTime` | 僅適用於&#x200B;*批次目的地*。 只有在批次檔案匯出目的地(例如Amazon S3、SFTP或Azure Blob)中將對象新增至資料流時，才需要此欄位。 <br>必要。 選取包含對象成員的檔案應該產生並匯出至您的目的地的時間。 |

**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 從資料流移除對象 {#remove-segment}

若要從現有的目的地資料流移除對象，請提供您要移除對象的資料流ID、版本和索引選取器，同時對[!DNL Flow Service] API執行PATCH要求。 索引從`0`開始。 例如，底下的範例要求會從資料流中移除第一和第二個對象。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

以下請求會從現有的目的地資料流中移除兩個對象。

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
   "path":"/transformations/0/params/segmentSelectors/selectors/0",
   "value":{
      "type":"PLATFORM_SEGMENT",
      "value":{
      }
   }
},
{
   "op":"remove",
   "path":"/transformations/0/params/segmentSelectors/selectors/1",
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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`、`replace`和`remove`。 若要從資料流移除對象，請使用`remove`作業。 |
| `path` | 根據對象選擇器的索引，指定應該從目的地資料流中移除哪些現有對象。 若要擷取資料流中的對象順序，請對`/flows`端點執行GET呼叫並檢查`transformations.segmentSelectors`屬性。 若要刪除資料流中的第一個對象，請使用`"path":"/transformations/0/params/segmentSelectors/selectors/0"`。 |


**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 更新資料流中的對象元件 {#update-segment}

您可以在現有的目的地資料流中更新對象的元件。 例如，您可以變更匯出頻率或編輯檔案名稱範本。 若要這麼做，請提供您的流量ID、版本，以及要更新之對象的索引選取器，同時對[!DNL Flow Service] API執行PATCH要求。 索引從`0`開始。 例如，以下請求會更新資料流中的第九個對象。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

在現有目的地資料流中更新對象時，您應該先執行GET作業，以擷取您要更新對象的詳細資料。 然後，提供承載中的所有對象資訊，而不僅僅是您要更新的欄位。 在以下範例中，自訂文字會新增到檔案名稱範本的結尾，而匯出排程頻率會從6小時更新為12小時。

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

如需承載中屬性的說明，請參閱[將對象新增至資料流](#add-segment)一節。


**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

如需可在資料流中更新的對象元件更多範例，請參閱下列範例。

## 在對象評估後，將對象匯出模式從已排程更新為 {#update-export-mode}

+++ 按一下以檢視對象匯出的範例，瞭解對象匯出從每天在指定時間啟動更新為在Experience Platform批次細分工作完成後每天啟動。

每日的16:00 UTC會匯出對象。

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

每日批次細分工作完成後，每日都會匯出對象。

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

## 更新檔案名稱範本以在檔案名稱中包含其他欄位 {#update-filename-template}

+++ 按一下以檢視檔案名稱範本更新以在檔案名稱中包含其他欄位的範例

匯出的檔案包含目的地名稱和Experience Platform對象ID

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

匯出的檔案包含目的地名稱、Experience Platform對象ID、Experience Platform產生檔案的日期和時間，以及在檔案結尾附加的自訂文字。


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

## 將設定檔屬性新增至資料流 {#add-profile-attribute}

若要將設定檔屬性新增至目的地資料流，請提供您的資料流ID、版本以及要新增的設定檔屬性，同時對[!DNL Flow Service] API執行PATCH要求。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

以下請求會將新的設定檔屬性新增至現有的目的地資料流。

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`、`replace`和`remove`。 若要將設定檔屬性新增至資料流，請使用`add`作業。 |
| `path` | 定義要更新的流程部分。 將設定檔屬性新增至資料流時，請使用範例中指定的路徑。 |
| `value.path` | 要新增至資料流的設定檔屬性值。 |

**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 從資料流移除設定檔屬性 {#remove-profile-attribute}

若要從現有的目的地資料流移除設定檔屬性，請提供您要移除之設定檔屬性的流量ID、版本和索引選取器，同時對[!DNL Flow Service] API執行PATCH要求。 索引從`0`開始。 例如，底下的範例要求會將第五個設定檔屬性從資料流中移除。


**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

以下請求會從現有的目的地資料流移除設定檔屬性。

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
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`、`replace`和`remove`。 若要從資料流移除對象，請使用`remove`作業。 |
| `path` | 根據對象選擇器的索引，指定應該從目的地資料流移除的現有設定檔屬性。 若要擷取資料流中的設定檔屬性順序，請對`/flows`端點執行GET呼叫並檢查`transformations.profileSelectors`屬性。 若要刪除資料流中的第一個對象，請使用`"path":"transformations/0/params/segmentSelectors/selectors/0/"`。 |


**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以透過向[!DNL Flow Service] API發出GET請求來驗證更新，同時提供您的流量ID。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點會遵循一般Experience Platform API錯誤訊息原則。 如需解譯錯誤回應的詳細資訊，請參閱Experience Platform疑難排解指南中的[API狀態碼](/help/landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](/help/landing/troubleshooting.md#request-header-errors)。

## 後續步驟 {#next-steps}

依照此教學課程，您已瞭解如何更新目的地資料流程的各種元件，例如使用[!DNL Flow Service] API新增或移除對象或設定檔屬性。 如需目的地的詳細資訊，請參閱[目的地概觀](../home.md)。
