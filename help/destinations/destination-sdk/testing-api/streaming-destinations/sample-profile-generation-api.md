---
description: 了解如何使用目的地測試API為串流目的地產生範例設定檔，以便用於目的地測試。
title: 根據來源結構產生範例設定檔
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 1%

---


# 根據來源結構產生範例設定檔 {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API端點**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

此頁面列出並說明您可使用 `/authoring/sample-profiles` API端點。

## 為不同的API產生不同的設定檔類型 {#different-profiles-different-apis}

>[!IMPORTANT]
>
>使用此API端點來產生兩個不同使用案例的範例設定檔。 您可以：
>* 產生設定檔時使用 [建立和測試報文轉換模板](create-template.md)  — 使用 *目的地ID* 作為查詢參數。
>* 生成配置檔案以在進行調用時使用 [測試您的目的地是否已正確設定](streaming-destination-testing-overview.md)  — 使用 *目的地執行個體ID* 作為查詢參數。


您可以根據AdobeXDM來源架構（在測試您的目的地時使用）或目的地支援的目標架構（在建立範本時使用），產生範例設定檔。 若要了解AdobeXDM來源架構與目標架構之間的差異，請參閱 [訊息格式](../../functionality/destination-server/message-format.md) 文章。

請注意，可以使用範例設定檔的用途不可互換。 根據 *目的地ID* 只能用來製作根據 *目的地執行個體ID* 只能用來測試目的地端點。

## 範例設定檔產生API操作快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 根據要在測試目的地時使用的來源結構產生範例設定檔 {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>將此處產生的範例設定檔新增至HTTP呼叫，當 [測試您的目的地](streaming-destination-testing-overview.md).

您可以向發出GET要求，以根據來源架構產生範例設定檔 `authoring/sample-profiles/` 端點，並提供您根據要測試的目的地設定所建立之目的地例項的ID。

若要取得目的地例項的ID，您必須先在Experience PlatformUI中建立與目的地的連線，才能嘗試測試目的地。 閱讀 [啟用目的地教學課程](../../../ui/activation-overview.md) 請參閱下方秘訣，了解如何取得要用於此API的目的地例項ID。

>[!IMPORTANT]
>
>* 若要使用此API，您必須在Experience PlatformUI中擁有與目的地的現有連線。 閱讀 [連接到目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 和 [將設定檔和區段啟用至目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) 以取得更多資訊。
> * 建立與目的地的連線後，取得您應在向此端點發出的API呼叫中使用的目的地執行個體ID，當 [瀏覽與目的地的連線](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en).
   >![UI影像如何取得目的地執行個體ID](../../assets/testing-api/get-destination-instance-id.png)


**API格式**

```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您要根據其產生範例設定檔的目的地例項ID。 |
| `{COUNT}` | *可選*. 您要產生的範例設定檔數目。 參數可以取用 `1 - 1000`. <br> 如果未指定count參數，則會由 `maxUsersPerRequest` 值 [目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md). 如果此屬性未定義，Adobe將產生一個範例設定檔。 |

{style="table-layout:auto"}


**要求**

下列請求會產生範例設定檔，由 `{DESTINATION_INSTANCE_ID}` 和 `{COUNT}` 查詢參數。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，包含指定數量的範例設定檔，以及對應至來源XDM架構的區段成員資格、身分和設定檔屬性。

>[!TIP]
>
> 回應只會傳回目的地例項中使用的區段成員資格、身分和設定檔屬性。 即使您的源架構有其他欄位，這些欄位也會被忽略。

```json
[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]
```

| 屬性 | 說明 |
| -------- | ----------- |
| `segmentMembership` | 描述個人區段成員資格的映射物件。 如需 `segmentMembership`，讀取 [區段成員資格詳細資料](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | 此設定檔符合區段資格的上次時間時間戳記。 |
| `xdm:status` | 字串欄位，指出區段成員資格是否已在目前請求中實現。 接受下列值： <ul><li>`realized`:設定檔是區段的一部分。</li><li>`exited`:設定檔會隨著目前請求退出區段。</li></ul> |
| `identityMap` | 一種地圖類型欄位，說明個人的各種身分值及其相關聯的命名空間。 如需 `identityMap`，讀取 [方案組合的基礎](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |

{style="table-layout:auto"}

## 根據目標架構生成示例配置檔案，以在建立消息轉換模板時使用 {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>使用在建立範本時在此處產生的範例設定檔，位於 [呈現範本步驟](render-template-api.md#multiple-profiles-with-body).

您可以根據向發出GET請求的目標架構產生範例設定檔 `authoring/sample-profiles/` 端點，並根據您建立範本的目的地設定提供目的地ID。

>[!TIP]
>
>* 您應在此處使用的目的地ID為 `instanceId` 與目標設定對應，使用 `/destinations` 端點。 請參閱 [檢索目標配置](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 以取得更多詳細資訊。


**API格式**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 您要根據其產生範例設定檔的目的地設定ID。 |
| `{COUNT}` | *可選*. 您要產生的範例設定檔數目。 參數可以取用 `1 - 1000`. <br> 如果未指定count參數，則會由 `maxUsersPerRequest` 值 [目標伺服器配置](../../authoring-api/destination-server/create-destination-server.md). 如果此屬性未定義，Adobe將產生一個範例設定檔。 |

{style="table-layout:auto"}

**要求**

下列請求會產生範例設定檔，由 `{DESTINATION_ID}` 和 `{COUNT}` 查詢參數。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定數量的範例設定檔，以及對應至目標XDM架構的區段成員資格、身分和設定檔屬性。

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]
```

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟

閱讀本檔案後，您現在知道如何產生範例設定檔，以便在 [測試消息轉換模板](create-template.md) 或 [測試您的目的地是否已正確設定](streaming-destination-testing-overview.md).
