---
description: 本頁列出並說明了所有可使用「/authoring/sample-profiles」 API端點來執行的API操作，以產生要用於目標測試的範例設定檔。
title: 設定檔產生API操作範例
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 2ed132cd16db64b5921c5632445956f750fead56
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 2%

---

# 設定檔產生API操作範例 {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API端點**:  `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

本頁列出並說明了所有可使用`/authoring/sample-profiles` API端點執行的API操作。

此API端點可讓您產生範例設定檔，以使用：
* 測試訊息轉換範本時。 閱讀[建立並測試訊息轉換範本](./create-template.md)以了解詳情。
* 測試目的地是否已正確設定時。 閱讀[測試目標配置](./test-destination.md)中的更多資訊。

您可以根據AdobeXDM來源架構或目的地支援的目標架構，產生範例設定檔。 若要了解AdobeXDM來源架構和目標架構之間的差異，請閱讀[Message format](./message-format.md)文章。

## 範例設定檔產生API操作快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](./getting-started.md)，以取得成功呼叫API所需的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 根據來源結構產生範例設定檔 {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>在[測試您的目的地](./test-destination.md)時，將此處產生的範例設定檔新增至HTTP呼叫。

您可以向`authoring/sample-profiles/`端點提出GET請求，並提供您根據要測試的目標配置建立的目標實例ID，從而根據源架構生成示例配置檔案。

>[!TIP]
>
>* 從URL取得瀏覽與目的地的連線時，您應在此處使用的目的地執行個體ID。
   >![UI影像如何取得目的地執行個體ID](./assets/get-destination-instance-id.png)


**API格式**


```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您要根據其產生範例設定檔的目的地例項ID。 |
| `{COUNT}` | *可選*. 您要產生的範例設定檔數目。 參數可採用介於`1 - 1000`之間的值。 <br> 如果未指定計數參數，則預設產生的設定檔數量由目標伺 `maxUsersPerRequest` 服器設定 [中的值決定](./destination-server-api.md#create)。如果此屬性未定義，Adobe將產生一個範例設定檔。 |

{style=&quot;table-layout:auto&quot;}


**要求**

下列請求會產生範例設定檔，由`{DESTINATION_INSTANCE_ID}`和`{COUNT}`查詢參數設定。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `segmentMembership` | 描述個人區段成員資格的映射物件。 如需`segmentMembership`的詳細資訊，請參閱[區段成員資格詳細資料](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html)。 |
| `lastQualificationTime` | 此設定檔符合區段資格的上次時間時間戳記。 |
| `xdm:status` | 指出區段成員資格是否已在目前請求中實現。 接受下列值： <ul><li>`existing`:在請求前，設定檔已是區段的一部分，並會繼續保留其成員資格。</li><li>`realized`:設定檔會在目前請求中輸入區段。</li><li>`exited`:設定檔會隨著目前請求退出區段。</li></ul> |
| `identityMap` | 一種地圖類型欄位，說明個人的各種身分值及其相關聯的命名空間。 有關`identityMap`的詳細資訊，請閱讀[架構組合基礎](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap)。 |

{style=&quot;table-layout:auto&quot;}

## 根據目標架構產生範例設定檔 {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>在[呈現模板步驟](./render-template-api.md#multiple-profiles-with-body)中，使用在建立模板時在此處生成的示例配置檔案。

您可以根據向`authoring/sample-profiles/`端點提出GET請求的目標架構生成示例配置檔案，並根據您建立模板的目標配置提供目標配置的目標ID。

>[!TIP]
>
>* 您應在此處使用的目標ID是與使用`/destinations`端點建立的目標配置對應的`instanceId`。 請參閱[目標配置API參考](./destination-configuration-api.md#retrieve-list)。


**API格式**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 您要根據其產生範例設定檔的目的地設定的ID。 |
| `{COUNT}` | *可選*. 您要產生的範例設定檔數目。 參數可採用介於`1 - 1000`之間的值。 <br> 如果未指定計數參數，則預設產生的設定檔數量由目標伺 `maxUsersPerRequest` 服器設定 [中的值決定](./destination-server-api.md#create)。如果此屬性未定義，Adobe將產生一個範例設定檔。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會產生範例設定檔，由`{DESTINATION_ID}`和`{COUNT}`查詢參數設定。

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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
                    "status": "existing"
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
                    "status": "existing"
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
                    "status": "existing"
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

目標SDK API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱平台疑難排解指南中的[API狀態代碼](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes)和[要求標題錯誤](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在知道如何產生範例設定檔，以在[測試訊息轉換範本](./create-template.md)時使用，或在[測試目的地是否已正確設定時使用](./test-destination.md)。
